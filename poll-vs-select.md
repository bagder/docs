# poll vs select vs event-based

 I failed to find a thorough comparison page on `poll()` vs `select()` so I
 wrote my own. If you find flaws or have additions, please let me know!

 [File issues or pull-requests](https://github.com/bagder/docs) if you find
 problems or have improvements.

 My [2010 blog post "poll vs
 select"](https://daniel.haxx.se/blog/2010/07/17/poll-vs-select/) also
 provides some background.

 Differences between `poll()` and `select()` and at the end some mentions
 about the more modern event-driven alternatives such as `epoll()`, kqueue and
 more. I recommend using a library such as
 [libev](http://software.schmorp.de/pkg/libev.html) or
 [libevent](http://www.monkey.org/~provos/libevent/).

 Those libs make it possible to write event-based programs in a portable
 manner, as the underlying technologies like
 [epoll](http://www.kernel.org/doc/man-pages/online/pages/man4/epoll.4.html)
 (Linux), [kqueue](http://en.wikipedia.org/wiki/Kqueue) (FreeBSD, NetBSD,
 OpenBSD, Darwin) and
 [/dev/poll](http://developers.sun.com/solaris/articles/polling_efficient.html)(Solaris,
 HPUX),
 [pollset](http://www.ibm.com/developerworks/aix/library/au-pollset/index.html)
 (AIX), [Event
 Completion](http://developers.sun.com/solaris/articles/event_completion.html)
 (Solaris 10) are different between platforms and aren't standard. The Windows
 solution seems to be [I/O Completion
 Ports](http://msdn.microsoft.com/en-us/library/aa365198%28VS.85%29.aspx).

## History

 select() was introduced in 4.2BSD Unix, released in August 1983.

 poll() was introduced in SVR3 Unix, released 1986. In Linux, the poll()
 system call was introduced in 2.1.23 (January 1997) while the poll() library
 call was introduced in libc 5.4.28 (May 1997)

## Functionality

 select() and poll() provide basically the same functionality. They only
 differ in the details:

 select() overwrites the `fd_set` variables whose pointers are passed in as
 arguments 2-4, telling it what to wait for. This makes a typical loop having
 to either have a backup copy of the variables, or even worse, do the loop to
 populate the bitmasks every time select() is to be called. poll() doesn't
 destroy the input data, so the same input array can be used over and over.

 poll() handles many file handles, like more than 1024 by default and without
 any particular work-arounds. Since select() uses bitmasks for file descriptor
 info with fixed size bitmasks it is much less convenient. On some operating
 systems like Solaris, you can compile for support with > 1024 file
 descriptors by changing the `FD_SETSIZE` define.

 poll offers somewhat more flavors of events to wait for, and to receive,
 although for most common networked cases they don't add a lot of value.

 Different timeout values. poll takes milliseconds, select takes a struct
 timeval pointer that offers microsecond resolution. In practice however,
 there probably isn't any difference that will matter.

 Going with an event-based function instead should provide the same
 functionality as well. They do however often force you to use a different
 approach since they're often callback-based that get triggered by events,
 instead of the loop style approach select and poll encourage.

## Speed

 poll and select are basically the same speed-wise: slow.

 They both handle file descriptors in a linear way. The more descriptors you
 ask them to check, the slower they get. As soon as you go beyond perhaps a
 hundred file descriptors or so - of course depending on your CPU and hardware
 - you will start noticing that the mere waiting for file descriptor activity
 and the following checking which file descriptor that it was, takes a
 significant time and becomes a bottle neck.

 The select() API with a "max fds" as first argument of course forces a scan
 over the bitmasks to find the exact file descriptors to check for, which the
 poll() API avoids. A small win for poll().

 select() only uses (at maximum) three bits of data per file descriptor, while
 poll() typically uses 64 bits per file descriptor. In each syscall invoke
 poll() thus needs to copy a lot more over to kernel space. A small win for
 select().

 Going with an event-based function is the only sane option if you go beyond a
 small number of file descriptors. The libev guys did a [benchmarking]
 (http://libev.schmorp.de/bench.html) of libevent against libev and their
 results say clearly that libev is the faster one.

 Compared to poll and select, any event-based system will give a performance
 boost already with a few hundred file descriptors and then the benefit just
 grows the more connections you add.

## Portability

 **select** - has existed for a great while and exists almost everywhere. A
 problem with many file descriptors is that you cannot know if you will
 overflow the bitmask as you can't check the file descriptor against
 `FD_SETSIZE` in a portable manner.
 
 Many unix versions allow `FD_SETSIZE` to be re-defined at compile time, but
 Linux does not.

 One quirk is that the include header required for the `fd_set` type
 varies between systems.

 Some - but not all - systems modify the timeout struct so that on return from
 select, the program can know how long time actually passed. If you repeat
 select() calls, you need to init the timeout struct each loop!

 **poll** - Not existing on older unixes nor in Windows before Vista. Broken
 implementation in Mac OS X at least up to 10.4 and earlier. Up to 10.3 you
 could check for a poll() that works with all arguments zeroed. The 10.4 bug
 is more obscure and I don't know of any way to detect it without checking for
 OS.

 Lots of early implementations did poll as a wrapper around select().

 poll's set of bits to return is fairly specific in the standards, but [vary a
 lot between
 implementations](http://www.greenend.org.uk/rjk/2001/06/poll.html).

## Complexity

 All event-driven functions tend to make the code more complex, harder to
 follow and require more code to be written to accomplish the same task as the
 simple select and poll approaches do.

## More Reading

 For everyhing select/poll/event-based, there's the [C10K problem
 page](http://www.kegel.com/c10k.html), which is a true goldmine.

 For great benchmarks on network scalability on a few operating systems, see
 [Felix von Leitner's work](http://bulk.fefe.de/scalability/).

## Thanks To

 The following friends helped me improve this text by pointing out flaws or
 enhancements:

 Fabian Keil, Andras Farkas

