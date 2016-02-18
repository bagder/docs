# FTP vs HTTP

This is an attempt to document the primary differences between FTP and HTTP,
as this is commonly asked and also a lot of misconceptions (and outright lies)
are flying around. If you find any errors, or have additional stuff to add,
please email me, file an [issue](https://github.com/bagder/docs/issues/new) or
post a [pull-request](https://github.com/bagder/docs/pulls)!

Both protocols are used for uploads and downloads on the internet, for text
and for binary, both over TCP/IP. But there are a lot of differences in the
details:

## Transfer Speed

Possibly the most common question: which is faster for transfers?

Given all details on this page. What makes FTP faster:

 - No added meta-data in the sent files, just the raw binary
 - Never chunked encoding "overhead"

What makes HTTP faster:

 - reusing existing persistent connections make better TCP performance
 - pipelining makes asking for multiple files from the same server faster
 - (automatic) compression makes less data get sent
 - no command/response flow minimizes extra round-trips

Ultimately the net outcome of course differ depending on specific details, but
I would say that for single-shot static files, you won't be able to measure a
difference. For a single shot small file, you might get it faster with FTP
(unless the server is at a long round-trip distance). When getting multiple
files, HTTP should be the faster one.

## Age

FTP ([RFC959](http://www.ietf.org/rfc/rfc959.txt)) appeared roughly ten years
before HTTP was invented. FTP was the one and only protocol back then. The
initial traces of what become RFC 959 can be found already as early as [1971](
http://www.ietf.org/rfc/rfc114.txt).

## Upload

Both protocols offer uploads. FTP has an "append" command, where HTTP is more
of a "here's data coming now you deal with it" approach.

It could be worth noticing that WebDAV is a protocol on top of HTTP that
provides "filesystem-like" abilities

## ASCII/binary/EBCDIC

FTP has a notion of file format so it can transfer data as ASCII or binary
(and more) where HTTP always sends things binary. FTP thus also allows text
conversions when files are sent between systems of different sorts:

If the destination uses a different scheme for encoding End-Of-Line characters
ftp will correct it for the destination. For example unix uses only a NL
(newLine x'0A') character and MS windows uses CR and LF (CarriageReturn and
LineFeed x'0D0A'). MS windows includes a CTRL-Z (x'1A') as an end of file
character, unix does not. EBCDIC specifies that a translation be performed
from ASCII to EBCDIC (used on old mainframes).

HTTP provides meta-data with files, Content-Type, which clients use but FTP
has no such thing. The meta data can thus be used by clients to interpret the
contents accordingly.

## Headers

Transfers with HTTP always also include a set of headers that send meta
data. FTP does not send such headers. When sending small files, the headers
can be a significant part of the amount of actual data transfered. HTTP
headers contain info about things such as last modified date, character
encoding, server name and version and more.

## Pipelining

HTTP supports pipelining. It means that a client can ask for the next transfer
already before the previous one has ended, which thus allows multiple
documents to get sent without a round-trip delay between the documents, and
TCP packets are thus optimized for transfer speed.

Something related, although not similar, is FTP's support for requesting
multiple files to get transferred in parallel using the same control
connection. That's of course using new TCP connections for each transfer so
it'll get different performance metrics.

## FTP Command/Response

FTP involves the client sending commands to which the server responds. A
single transfer can involve quite a series of commands. This of course has a
negative impact since there's a round-trip delay for each command. HTTP
transfers are primarily just one request and one response (for each
document). Retrieving a single FTP file can easily get up to 10 round-trips.

## Two Connections

One of the biggest hurdles about FTP in real life is its use of two
connections. It uses a first primary connection to send control commands on,
and when it sends or receives data, it opens a second TCP stream for that
purpose.

## Firewalls and NATs

FTP's use of two connections, where the second one use dynamic port numbers
and can go in either direction, gives the firewall admins grief and firewalls
really have to "understand" FTP at the application protocol layer to work
really well.

This also means that if both parties are behind [NATs](
http://en.wikipedia.org/wiki/Network_address_translation), you cannot use FTP!

Additionally, as NATs often are setup to kill idle connections and the nature
of FTP makes the control channel remain quiet during long and slow FTP
transfers, we often end up with the control channel getting cut off by the NAT
due to idleness.

## Active and Passive

FTP opens the second connection in an active or passive mode, which basically
says which end that initiates it. It's a client decision to try either way.

## Encrypted Control Connections

Since firewalls need to understand FTP to be able to open ports for the
secondary connection etc, there's a huge problem with encrypted FTP (FTP-SSL
or FTPS) since then the control connection is sent encrypted and the
firewall(s) cannot interpret the commands that deal with creating the second
connection. Also, the FTPS standard took a very long time to "hit it" so there
exists a range of hybrid versions out in the wild.

## Authentications

FTP and HTTP have a different set of authentication methods documented. While
both protocols offer basically plain-text user and password by default, there
are several commonly used authentication methods for HTTP that isn't sending
the password as plain text, but there aren't as many (non-kerberos) options
available for FTP.

## Download

Both protocols offer support for download. Both protocols used to have
problems with file sizes larger than 2GB but those are history for modern
clients and servers on modern operating systems.

## Ranges/resume

Both FTP and HTTP support resumed transfers in both directions, but HTTP
supports more advanced byte ranges.

Resumed transfers for FTP that start beyond the 2GB position has been known to
cause trouble in the past but should be better these days.

## Persistent Connections

For HTTP communication, a client can maintain a single connection to a server
and just keep using that for any amount of transfers. FTP must create a new
one for each new data transfer. Repeatedly doing new connections are bad for
performance due to having to do new handshakes/connections all the time and
redoing the TCP slow start period and more.

## HTTP Chunked Encoding

To avoid having to close down the data connection in order to signal the end
of a transfer - when the size of the transfer wasn't known when the transfer
started, chunked encoding was introduced in HTTP.

During a "chunked encoding" transfer, the sending party sends a stream of
[size-of-data][data] blocks over the wire until there is no more data to send
and then it sends a zero-size chunk to signal the end of it.

Another obvious benefit (apart from having to re-open the connection again for
next transfer) with chunked encoding compared to plain closing of the
connection is the ability to detect premature connection shutdowns.

## Compression

HTTP provides a way for the client and server to negotiate and choose among
sevel compression algorithms. The gzip algorithm being the perhaps most widely
used one, with brotli being a recent addition that often compresses data even
better.

FTP offers an official "built-in" run length encoding that compresses the
amount of data to send, but not by a great deal on ordinary binary data. It
has also traditionally been done for FTP using various "hackish" approaches
that were never in any FTP spec.

## FXP

FTP supports "third party transfers", often called "FXP". It allows a client
to ask a server to send data to a third host, a host that isn't the same as
the client. This is often disabled in modern FTP servers though due to the
security implications.

## IPv6

HTTP and FTP both support ipv6 fine, but the original FTP spec had no such
support and still today many FTP servers don't have support for the necessary
commands that would enable it. This also goes for the firewalls in between
that need to understand FTP.

## Name based virtual hosting

Using HTTP 1.1, you can easily host many sites on the same server and they are
all differentiated by their names.

In FTP, you cannot do name based virtual hosting at all until the
[HOST](http://tools.ietf.org/html/rfc7151) command gets implemented in the
server you talk to and in the ftp client you use... It is a recent spec
without many implementations.

## Dir Listing

One area in which FTP stands out somewhat is that it is a protocol that is
directly on file level. It means that FTP has for example commands for listing
dir contents of the remote server, while HTTP has no such concept.

However, the FTP spec authors lived in a different age so the commands for
listing directory contents (LIST and NLST) don't have a specified output
format so it's a pain to write programs to parse the output. Latter specs
(RFC3659) have addressed this with new commands like MLSD, but they are not
widely implemented or supported by neither servers nor clients.

## Proxy Support

One of the biggest selling points for HTTP over FTP is its support for
proxies, already built-in into the protocol from day 1. The support is so
successful and well used that lots of other protocols can be sent over HTTP
these days just for its ability to go through proxies.

FTP has always been used over proxies as well, but that was never standardized
and was always done in lots of different ad-hoc approaches.

## Further

There are further differences, like the HTTP ability to do conditional
requests, negotiate content language and much more but those are not big
enough to be specified in this document.

## Thanks

Feedback and improvements by: Micah Cowan, Joe Touch, Austin Appel, Dennis
German, Josh Hillman
