# wcurl vs Wget

The main differences.

* [wcurl](https://curl.se/wcurl) 
* [Wget](http://www.gnu.org/software/wget/)

[File issues or pull-requests](https://github.com/bagder/docs) if you find
problems or have improvements to this comparison.

## What both commands do/are

- command line tools that can download URLs from FTP, HTTP(S)
- work without user interaction
- fully open source and free software
- portable and run on many operating systems
- follow redirects automatically
- get the remote file's time and set it locally
- retry on transient errors

# How they differ

## wcurl

- a shell script that invokes **curl**

- downloads URLs in parallel

- curl licensed

- supports all the URL schemes curl does, many more than wget

- happy eyeballs connections

- is a little complicated to run on Windows

## Wget

- a stand-alone executable

- downloads URLs serially

- *Recursive!*: Wget's major strong side compared to wcurl is its ability to
  download recursively, or even just download everything that is referred to
  from a remote resource, be it a HTML page or a FTP directory listing.

- *GPL*: Wget is *GPL v3*

- enables cookies by default

- works on Windows

# When to use which

Primarily: use the one that gets the job done for you.
