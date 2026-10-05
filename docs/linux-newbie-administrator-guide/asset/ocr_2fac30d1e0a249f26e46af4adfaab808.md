# killall netscape

will kill any program with "netscape" in its name.

X-windows-based programs have no control terminals and may be the easiest to kill this (typed in an X-terminal):

xkill

to which the cursor changes into something looking like a death sentence; you point out the window of the program to press the left mouse button; the window disappears for good, and the associated program is terminated.

If your X-windows system crashes so that it cannot recover, it may be the easiest to kill the X-server by pressing \<Ctrl><Alt><Space>.\ After that, it may be a good idea to run ps axu, find any X-programs that might still be running, and kill them. If you don't, the misbehaving program that caused your X-windows to crash might cause trouble again.

If you have programs in the background, the operating systems will object your logging out, and issue a message like "There are stopped jobs". To override and logout, just repeat the logout (or exit) command immediately --the background program(s) will be automatically terminated and you will be logged out.

**Core files.** When a program crashes, it dumps a "core" into your home directory. This is accompanied by an appropriate message. A core is a memory image (plus debugging info) and is meant to be a debugging tool. If you are a user who does not intend to debug the program, you may simply delete the core:

```
rm core
```

or do nothing (the core will be overwritten if another core is dumped). You can also disable dumping the core using the command:

```
ulimit -c 0
```

Checked if it worked using:

```
ulimit -a
```

(This shows "user limits", the option "-a" stands for "all\). To make option of disabling core dumps permanent for all users, edit the file /etc/profile (as root), where ulimit is set, and adjust the setting. Re-login for the changes to /etc/profile to take effect.

If you would like to see how a core file can be used, try (in the directory where you have a core file):

```
gdb -c core
```