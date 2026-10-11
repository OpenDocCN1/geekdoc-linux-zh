the group. However, for this program, we know there are members, or `print_group()` wouldn’t have been called! Here’s what happens when the program is run:

```
$ ch06-groupInfo arnold
mail:x:12:mail,postfix,arnold
uucp:x:14:uucp,arnold
floppy:x:19:arnold
devel:x:42:miriam,arnold
arnold:x:2076:arnold
```

# 6.4 Terminals: `isatty()`

The Linux/Unix standard input, standard output, standard error model discourages the special treatment of input and output devices. Programs generally should not need to know, or care, whether their output is a terminal, a file, a pipe, a physical device, or whatever.

However, there are times when a program really does need to know what kind of a file a file descriptor is associated with. The `stat()` family of calls often provides enough information: regular file, directory, device, and so on. Sometimes though, even that is not enough, and for interactive programs in particular, you may need to know if a file descriptor represents a tty

A tty (short for Teletype, one of the early manufacturers of computer terminals) is any device that represents a terminal, that is, something that a human would use to interact with the computer. This may be either a hardware device, such as the keyboard and monitor of a personal computer, an old-fashioned video display terminal connected to a computer by a serial line or modem, or a software *pseudoterminal*, such as is used for windowing systems and network logins.

The discrimination can be made with `isatty()`:

```
#include <unistd.h>
int isatty(int desc);
```

This function returns 1 if the file descriptor `desc` represents a terminal, 0 otherwise. According to POSIX, `isatty()` may set `errno` to indicate an error; thus you should set `errno` to 0 before calling `isatty()` and then check its value if the return is 0. (The GNU/Linux `isatty(3)` manpage doesn’t mention the use of `errno`.) The POSIX standard also points out that just because `isatty()` returns 1 doesn’t mean there’s a human at the other end of the file descriptor!