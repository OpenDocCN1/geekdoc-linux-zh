I won’t cover any more of *Curses* in this book, as it’s not a kernel service.$^{10}$

*Curses* is part of SUS2 and SUS3, so you can read the specification online at the SUS2 site at www.unix-systems.org/version2/online.html. On most systems you can also type `man curses` or `man ncurses` (a free version of *Curses*).

# ## 4.9 STREAMS I/O

STREAMS are a mechanism on some implementations of UNIX that allow character device drivers to be implemented in a modular fashion. Applications can, to some extent, chain various STREAMS modules together to get the kind of driver capabilities they want. It’s somewhat analogous to the way UNIX filters work at the shell level; for example, the `who` command may not have an option to sort its output, but you can pipe it into `sort` if that’s what you want.

I’ll show an example of STREAMS-based pseudo terminals in the next section. What I’ll do there is `open` a device file to get a pseudo terminal and then use `ioctl` to “push” two STREAMS modules onto it (`ldterm` and `ptem`) to make it behave like a terminal. Unlike with shell pipelines, where you have dozens of filters to choose from that can be combined hundreds of creative ways, STREAMS modules are usually used in cookbook fashion—you push the modules the documentation tells you to push, and, as with cooking, you won’t get anything delicious if you just push things willy-nilly. (STREAMS should not be confused with the standard I/O concept of streams, used by `fopen`, `fwrite`, etc.. The two are totally unrelated.)

The STREAMS feature was required by SUS1 and SUS2, but not by SUS3. Linux, which sets `_XOPEN_VERSION` to 500 (indicating it’s SUS2), doesn’t provide STREAMS, which makes it nonconforming in that sense.

Aside from my use of STREAMS for pseudo terminals in the next section and a few other mentions in this book, I won’t provide a full treatment of STREAMS. The easiest way to find out more about them is from the SUS or from Sun’s site at www.sun.com, where you can find the *STREAMS Programming Guide*.

> 10. Besides, if we included *Curses*, we’d have to include X, and that would kill us. (In this context, “us” means “you and me.”)