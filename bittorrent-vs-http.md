# bittorrent vs HTTP

Here's a comparison between the use of bittorrent vs HTTP for data transfers.

## Basic Facts

Bittorrent is a way for a client to figure out what peers that have a piece of
a particular file so that it can get pieces from those machines instead of
getting the entire thing from a single (central) place.

## Transfer Speed

With **HTTP** a file is presented in a single stream by the HTTP server. The
transfer is then typically done the fastest way the remote server, the network
and the client manage. After the initial "request", HTTP reaches max speed
pretty quickly. A typical such transfer is limited by the narrowest network
condition along the way, or by the server being overloaded by requests from
many clients. Some network operators do funny things, so a client can actually
get higher transfer performance by connecting multiple times and transferring
parts of the data in several simultaneous connections.

**Bittorrent** on the other hand requests "random" parts of the file from N
number of peers and it can typically download several parts at once from
different sources. A client will also soon start to hand out parts of the file
that it has already downloaded, to other peers that want to download that same
file. Bittorrent downloads tend to start slow, and increase in speed during
the transfer and slow down again towards the end when it only gets a few
remaining pieces to get.

## Streaming

Things that must be sent and received in a specific order, such as a live
audio or video stream, is problematic to distribute via bittorrent given the
current design.

While clients (probably) could ask for chunks in a chronological order and
then get the data in a sequential manner that is not how clients typically
work, and it would greaty defeat some of the primary purposes of bittorrent as
it will not at all distribute the load as evenly among the peers as the
"random access" method does.

## Uplink

Due to the nature of these protocols. A **bittorrent** transfer to you is very
likely to reach you over other users' uplinks. Your client also hands out data
to other users over your Internet connection. With bittorrent you're getting
each individual part limited by the uplink speed of that user who has that
part. Your client also hands out data so you use your uplink at lot (as much
as you allow it basically).

With **HTTP**, all the uplink is used for basically, is sending TCP ACKs to
the server. That's only a small fraction of the bandwidth you use in the
downlink.

## Firewalls

**Bittorrent** needs to go out and connect to multiple remote machines. For
your client to be able to hand out stuff properly it also needs to allow
remote clients to connect back to you (even on multiple inbound ports) and
that requires that you have a firewall setup that allows this.

**HTTP** is a traditional client so it only connects to a server, which
firewalls tend to be setup to allow with no extra fuzz needed.

Related, is the fact that bittorrent uses a lot more TCP connections in any
typical use case which might be troublesome for OSes or intermediate routers
etc with fixed limits.

 Bittorrent typically runs on separate TCP ports (6881-6999) which are easily
blocked by firewall admins.

## Redundancy

A bittorrent client can survive that the primary server (tracker) goes away
after it has gotten the primary torrent off it and found one or more peers to
request file parts from, while a HTTP solution is depending on the server to
stick around and to keep feeding the TCP stream. Bittorrent also has
techniques to work in "trackerless" mode (DHT and Mainline DHT being two)
which makes it even more robust.

The HTTP server can in fact go silent for a long time and the connection will
then just continue again when the server re-appears, but both HTTP and
bittorrent use TCP so that's pretty much the same for both protocols. It's
just that even if one connection stalls with bittorrent, chances are the
others still strive.

## Server Load

One of the primary purposes of bittorrent is to ease the burden to
provide data for download, and as such it is certainly way better than
HTTP as you can distribute a particular file to a very large amount of
clients with only a fraction of the load and bandwidth requirements on the
server/tracker.

## Encryption

HTTP has no encryption but the standard way is to do HTTP over TLS, called
HTTPS. That provides what is generally accepted a secure data connection.

bittorrent offers a protocol extension called Message Stream Encryption (MPE)
which provides a *"message stream obfuscation by the application of fairly
simple cryptographic techniques, not a full blown transport level security
mechanism like SSL"* ([quote referece](http://www.azureuswiki.com/index.php/Message_Stream_Encryption)).

## Protocol Standards

[HTTP](http://www.ietf.org/rfc/rfc7230.txt) is an established and formalized
protocol standard by the IETF.

[Bittorrent](http://www.bittorrent.org/beps/bep_0003.html) is a protocol
designed by the company named Bittorrent and there is a large amount of
variations and extensions in implementations and clients.

## Further Reading

The [wikipedia article on
bittorrent](http://en.wikipedia.org/wiki/BitTorrent_%28protocol%29) is very
detailed and a good read.

## Thanks

Feedback and improvements by: Austin Appel, Dave Chapman
