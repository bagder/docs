# curl vs Wget

The main differences as I (Daniel Stenberg) see them. Please consider my bias
towards [curl](http://curl.haxx.se) since after all, curl is my baby - but I
contribute to [Wget](http://www.gnu.org/software/wget/) as well.

Please let me know if you have other thoughts or comments on this document.

[File issues or pull-requests](https://github.com/bagder/docs) if you find
problems or have improvements.

## What both commands do

- both are command line tools that can download contents from FTP, HTTP and
  HTTPS
- both can send HTTP POST requests
- both support HTTP cookies
- both are designed to work without user interaction, like from within scripts
- both are fully open source and free software
- both projects were started in the 90s
- both support *metalink*

## How they differ

### curl

- *library*. curl is powered by *libcurl* - a cross-platform library with a
  stable API that can be used by each and everyone. This difference is major
  since it creates a completely different attitude on how to do things
  internally. It is also slightly harder to make a library than a "mere"
  command line tool.

- *pipes*. curl works more like the traditional unix cat command, it sends
  more stuff to stdout, and reads more from stdin in a "everything is a pipe"
  manner. Wget is more like cp, using the same analogue.

- *Single shot*. curl is basically made to do single-shot transfers of
  data. It transfers just the URLs that the user specifies, and does not
  contain any recursive downloading logic nor any sort of HTML parser.

- *More protocols*. curl supports FTP, FTPS, Gopher, HTTP, HTTPS, SCP,
  SFTP, TFTP, TELNET, DICT, LDAP, LDAPS, FILE, POP3, IMAP, SMB/CIFS, SMTP, RTMP
  and RTSP. Wget only supports HTTP, HTTPS and FTP.
 
- *More portable*. curl builds and runs on lots of more platforms than
  wget. For example: OS/400, TPF and other more "exotic" platforms that aren't
  straight-forward unix clones.

- *More SSL libraries* and SSL support. curl can be built with one out
  of eleven (11!) different SSL/TLS libraries, and it offers more control and
  wider support for protocol details.

- *HTTP auth*. curl supports more HTTP authentication methods,
  especially over HTTP proxies: Basic, Digest, NTLM and Negotiate

- *SOCKS*. curl supports several SOCKS protocol versions for proxy access

- *Bidirectional*. curl offers upload and sending capabilities. Wget
  only offers plain HTTP POST support.

- *HTTP multipart/form-data* sending, which allows users to do HTTP
  "upload" and in general emulate browsers and do HTTP automation to a wider
  extent

- curl supports gzip and deflate Content-Encoding and does *automatic decompression*

- curl offers and performs decompression of *Transfer-Encoded HTTP*, wget doesn't

- curl supports *HTTP/2* and it does dual-stack connects using *Happy Eyeballs*

- *Much more developer activity*. While this can be debated, I consider three
  metrics here: mailing list activity, source code commit frequency and
  release frequency. Anyone following these two projects can see that the curl
  project has a lot higher pace in all these areas, and it has been so for 10+
  years. [Compare on openhub](https://www.openhub.net/p/_compare?project_0=cURL&project_1=Wget)

### Wget

- Wget is *command line only*. There's no library.

- *Recursive!* Wget's major strong side compared to curl is its ability to
  download recursively, or even just download everything that is referred to
  from a remote resource, be it a HTML page or a FTP directory listing.

- *Older*. Wget has traces back to
  [1995](http://en.wikipedia.org/wiki/Wget#History), while curl can be
tracked back no earlier than the end of
  [1996](http://curl.haxx.se/docs/history.html).

- *GPL*. Wget is 100% *GPL v3*. curl is *MIT licensed*.

- *GNU*. Wget is part of the *GNU* project and all copyrights are assigned to
  *FSF*. The curl project is entirely stand-alone and independent with no
  organization parenting at all with almost all copyrights owned by
  *Daniel*.

- Wget requires *no extra options* to simply download a remote URL to a local
  file, while curl requires -o or -O.

- Wget supports only *GnuTLS or OpenSSL* for SSL/TLS support

- Wget supports only *Basic* auth as the only auth type over HTTP proxy

- Wget has no SOCKS support

- Its ability to recover from a prematurely broken transfer and *continue
  downloading* has no counterpart in curl.

- Wget enables more features by default: cookies, redirect-following, time
  stamping from the remote resource etc. With curl most of those features need
  to be explicitly enabled.

- Wget can be typed in using only the left hand on a qwerty keyboard!

## Additional Stuff

Some have argued that I should compare uploading capabilities with
[wput](http://wput.sourceforge.net), but that's a separate tool/project and I
don't include that in this comparison.

Two other capable tools with similar feature set include
[aria2](http://aria2.sourceforge.net/) and
[axel](http://axel.alioth.debian.org) (dead project?) - try them out!

For a stricter feature by feature comparison (that also compares other similar
tools), see the [curl comparison
table](http://curl.haxx.se/docs/comparison-table.html)

## Thanks

  Feedback and improvements by: Micah Cowan, Olemis Lang
