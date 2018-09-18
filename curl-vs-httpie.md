# [curl](https://curl.haxx.se/) vs [HTTPie](https://github.com/jkbrzt/httpie)

The main differences as I (Daniel Stenberg) see them. Please consider my bias towards curl since after all, curl is my baby.

Please let me know if you have other thoughts or comments on this document. File [issues](https://github.com/bagder/docs/issues) or [pull-requests](https://github.com/bagder/docs/pulls) if you find problems or have improvements.

## What both commands do

- Perform HTTP(S) operations specified as URLs
- Require an option to follow redirects
- Support `-v` to show sent request headers
- Support HTTP and SOCKS proxies
- HTTP Range requests
- netrc support

## Transfer performance comparsion

Tranfering 80GB from a localhost Apache HTTP server to /dev/null on Linux.

httpie 0.9.8 needed 153 seconds. **535 MB/sec**

curl 7.51.0 needed 25 seconds. **3276 MB/sec**

## curl

- Written in C and uses libcurl
- supports many other protocols as well apart from HTTP(S)
- supports any amount of URLs on the command line
- can send binary POSTs
- Supports multiple HTTP methods in a single command line for different URLs
- Documented in a [man page](https://curl.haxx.se/docs/manpage.html) for offline documentation
- supports HTTP/1.0 requests
- features URL "globbing" for ranges and sequences
- Allows more invasive header modifications, like passing in invalid letters
  in custom headers (`Höst:`), replacing `Content-Length:` in a POST and removing
  the `Host:`  header from a request. Or just adding a header *without* a space
  after the colon.
- Supports happy eyeballs or explicit ipv4/ipv6 use
- Supports custom connection tricks like with [--resolve
  ](https://curl.haxx.se/docs/manpage.html#--resolve) and
  [--connect-to](https://curl.haxx.se/docs/manpage.html#--connect-to)
- HTTP/2 support (for both HTTP:// and HTTPS:// URLs)

## HTTPie "cURL-like tool for humans"

- Written in Python and uses Requests
- Only supports a single URL on the command line
- Has JSON support
- Colored output
- Assumes "name=value" for POSTS (name:value or just "data" is hard/impossible
  to send, not to mention POSTing `Connection:` - which instead will be
  intepreted as remove that header please)
- Can you do a multipart POST with two text-only fields?
- Forbids UTF-8 symbols in HTTP request headers
- Doesn't allow a user to change the Content-Length: header
- Has an "Auth plugin" system that supports many more auth types than curl
- Can't send the same header field name multiple times in a request.
- Has no official man page
- HTTP/2 ?
- Happy eyeballs?
- HTTPS proxy support (HTTPS to the proxy, independently of the server's protocol) ?
- brotli support?
