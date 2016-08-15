# [curl](https://curl.haxx.se/) vs [HTTPie](https://github.com/jkbrzt/httpie)

## What both commands do

- Performs HTTP(S) operations specified as URLs
- Need an option to follow redirects
- Support `-v` to show sent request headers
- Support HTTP and SOCKS proxies
- Can do HTTP Range requests

## curl

- Written in C and uses libcurl
- supports many other protocols as well apart from HTTP(S)
- supports any amount of URLs on the command line
- can send binary POSTs
- Allows invalid letters in custom headers, like Höst:
- Allow users to replace Content-Length: in a POST
- Supports multiple HTTP methods in a single command line for different URLs
- Is documented in a man page for non-web documentation
- supports HTTP/1.0 requests

## HTTPie "cURL-like tool for humans"

- Written in Python and uses Requests
- Only supports a single URL on the command line
- Has JSON support
- Colored output
- Assumes "name=value" for POSTS (name:value or just "data" is hard/impossible
  to send, not to mention POSTing "Connection:" - which instead will be
  intepreted as remove that header please)
- Can you do multipart a POST with two text-only fields?
- Forbids UTF-8 symbols in HTTP request headers
- Doesn't allow a user to change the Content-Length: header
- Has an "Auth plugin" system that supports many more auth types than curl
- Has no official man page
- HTTP/2 ?
