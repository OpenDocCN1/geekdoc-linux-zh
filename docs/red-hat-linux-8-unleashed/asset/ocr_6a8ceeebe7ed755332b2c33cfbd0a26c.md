# CHAPTER 7 Managing Services

> TIP
Linux is full of shortcuts: If you exit the single-user shell, you'll go back to the default runlevel without worrying about using telinit.

> TIP
nYou might find yourself confronting a nonfunctioning X server. If that happens, you might seem doomed to a never-ending series of respawning X server attempts while in runlevel 5—but there is a way out. Use Alt+Ctrl+F2 to access a virtual terminal, log in as root, and use the telinit 3 command to change runlevel 3. Fix the X configuration and start X with

# startx

until you get it fixed and can safely return to runlevel 5.

If remote login is available, you can also use the secure shell, ssh, to log in to the system from another computer to the network to change runlevels.

# Using Service Management to Troubleshoot Problems in Red Hat Linux

Reordering or changing system services during a particular runlevel is rarely necessary when using Red Hat Linux unless some disaster occurs. But system administrators should have a basic understanding of how Linux boots and how services are controlled in order to perform troubleshooting or to diagnose problems. By using additional utilities such as the dmesg | less command to read kernel output after booting or by examining system logging with cat /var/log/messages | less, it is possible to gain a bit more detail about what is going on when faced with troublesome drivers or service failure.

To better understand how to troubleshoot service problems in Red Hat Linux, take a look at the diagnosis and resolution of a typical service-related issue.

In this example, X won't start: You don't see a desktop displayed, nor does the computer seem to respond to keyboard input. The X server might either be hung in a loop, repeatedly failing, or might exit to a shell prompt with or without an error message.

The X server only attempts to restart itself in runlevel 5, so to determine whether the X server is hung in a loop, try switching to runlevel 3.

> TIP
If you're working on a multiuser system and might inadvertently interrupt the work of other users, ask them to save their current work; then change to a safer runlevel, such as single user mode.