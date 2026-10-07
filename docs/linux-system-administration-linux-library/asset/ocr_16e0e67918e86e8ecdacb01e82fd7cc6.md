to use a Linux terminal program on one computer, as described later in this chapter, in
“Calling a Remote Text-Mode System.",

> NOTE uses virtual terminals to provide text-mode access to a Linux sys-
tfrom its main keyboard and monitor (which are collectively referred to as the
console). To configure Linux to use "real" terminals, you extend this configura-
to support serial devices as well as the console, as described shortly.

# Configuring a getty Program

In most cases, the goal when using a terminal (either dumb terminal hardware or a ter-
minal emulator) is to have the terminal display a Linux login: prompt when the user
starts the terminal. Linux normally presents these prompts using a program called getty,
or some variant of that, such as minetty, mgetty, or agetty.

> NOTE The original getty program goes by that name. Various replacements
use similar names and similar things. The word getty can therefore refer to
either the original getty program or the class of similar programs that fill basi-
cally the same role. For the most part, the word is used in the latter sense in this
chapter.

Linux runs getty programs from the /etc/inittab file. In Red Hat 7.0, the default
/etc/inittab file contains the following lines:

```
# Run getty in standard runlevels
1:2345:respawn:/sbin/mintty tty1
2:2345:respawn:/sbin/mintty tty2
3:2345:respawn:/sbin/mintty tty3
4:2345:respawn:/sbin/mintty tty4
5:2345:respawn:/sbin/mintty tty5
6:2345:respawn:/sbin/mintty tty6
```

Each line in the /etc/inittab file contains colon-delimited entries that tell the system
about certain types of services to be run. The preceding entries tell Linux to
 /sbin/mintty program for each of the first six virtual consoles in run levels 2
through 5. The result of these entries is that you can use Alt+1 through Alt+6 (in com-
ination with Ctrl, if you're currently running X) to shift to any of six virtual consoles.
You can log in to any of these to run programs, even under different usernames.

![](bbox=[0.873, 0.574, 0.953, 0.706])