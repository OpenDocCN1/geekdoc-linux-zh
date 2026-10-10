Linux, unlike some other operating systems, allows you to pick and choose the features you want in the kernel. (You'll learn about this process in Chapter 10.) The default kernel will already be reasonably well tuned, so you won't have to worry about it, but if you do need to change a feature or upgrade the kernel, be picky about what you add and what you don't. Make sure you really need a feature before adding it.

> **NOTE:** You may hear an old recommendation that you recompile your kernel to make the most effective use of your system resources. This is no longer true. The only reason to recompile your kernel is to upgrade or add support for a new device. Remember - don't sweat around (fighity) with what's stable and performs reasonably.

# Uptime

All of this chapter about taking care of servers and making sure silly things don't cause them to crash stems from a long-time UNIX philosophy: **Uptime is good. More uptime is better.** The UNIX `Uplime` command utility tells the user how long the system has been running. Since it is last boot, many users are currently logged in, and how much load the system is experiencing. The latter two are useful measures that are necessary for day-to-day system health and long-term planning. For example, the server load has been staying high lately, so maybe it's time to buy a faster / bigger / better server . . .

But the all-important number is how long the server has been running since its last reboot. Long uptimes are a sign of proper care, maintenance, and, from a practical standpoint, system stability. You'll often find UNIX administrators boasting about their server's uptime the way you hear car buffs boast about horsepower. This is also why you'll hear UNIX administrators cursing at Windows installations that require a reboot for every little change. In contrast, you'll be pressed to find any changes to a UNIX system that require a reboot to take effect.

You'll dare caring about it now. In six months you'll probably scream at anyone who reboots the system unnecessarily. Don't bother trying to explain this phenomenon to a nonadmin because they'll just look at you oddly. You'll just know in your heart that your uptime is better than theirs.

# Dual-Bootins Issues

If you are new to Linux, you may not be ready to commit a complete system when you just want a test drive. All distributions of Linux can be installed on only certain partitions of your hard disk while leaving others alone. Typically, this means allowing Microsoft Windows to coexist with Linux.

Because we are focusing on server installations, we will not cover the details of building a dual-booting system; however, anyone with a little experience in creating partitions on a disk should be able to figure this out. If you are having difficulty, you may want to refer to the installation guide that comes with your distribution or another one of the many available beginner's guides to Linux.