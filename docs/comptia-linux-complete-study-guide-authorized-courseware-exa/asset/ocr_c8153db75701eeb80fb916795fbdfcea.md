+   The initial program gets the process ID (PID) of 1 because it’s the first program to run on the system. Assuming that /sbin/init is the initial program, it reads a file called /etc/inittab to determine what other programs to run. Other programs usually include getty programs for console logins, system initialization scripts for mounting more partitions or starting up system services, and an X Display Manager (XDM) program to give you a graphical login.

How the init program and the initialization scripts work is covered next, in “Dealing with Runlevels and the Initialization Process.”

![](bbox=[0.15, 0.29, 0.22, 0.37])

> If you would like more details about this boot process, read <http://www.linuxdexter.com/pub/a/linux/kernel/linux_kernel/ how-computer_boots.html>. This page describes the process from the computer being powered up to the kernel being loaded and launching /sbin/init.

# Dealing with Runlevels and the Initialization Process

Linux relies on runlevels to determine what features are available. Runlevels are numbered from 0 to 6, and each one is assigned a set of services that should be active. Upon booting, Linux enters a predetermined runlevel, which you can set. Knowing what these functions are, and how to manage runlevels, is important if you’re to control the Linux boot process and ongoing operations. Toward that end, you must understand the purpose of runlevels, be able to identify the services that are active in a runlevel, be able to adjust those services, be able to check your default and current runlevels, and be able to change the default and current runlevels.

# Runlevel Functions

Earlier in this chapter, I described single-user mode. To get to this mode when booting Linux, you use the number 1, the letter S or s, or the word single as an option passed to the kernel by the boot loader. Single-user mode is simply an available runlevel for your system. The available runlevels on most systems are the numbers 0 through 6. The letters S and s are synonymous with runlevel 1 as far as many utilities are concerned.

Runlevels 0, 1, and 6 are reserved for special purposes; the remaining runlevels are available for whatever purpose you or your Linux distribution provider decide. Table 5.1 summarizes the conventional uses of the runlevels. Other assignments—and even runlevels outside the range of 0 to 6—are possible, but such configurations are rare. (Gentoo uses an unusual