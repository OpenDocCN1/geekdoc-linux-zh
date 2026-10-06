file to determine what other programs to run. On systems that use the newer Upstart or systemd startup, /sbin/init reads other configuration files.

How the init program and the initialization scripts work is covered, in "Dealing Runlevels and the Initialization Process."

> If you would like more details about this boot process, read http://www.linuxdevcenter.com/pub/a/linux/excerpts/linux_kernel1/how_computer_boots.html This page describes the process from the computer being powered up to the kernel being loaded and launching /sbin/init.

# Dealing with Runlevels and the Initialization Process

Linux relies on runlevels to determine what features are available. From 0 to 6, and each one is assigned a set of services that should be active. Upon booting, Linux enters a predetermined runlevel which you can set. Knowing what these functions are, and how to manage runlevels, is important if you are to control the Linux boot process and ongoing operations. To this end, you must understand the purpose of runlevels, be able to identify the services that are active in a runlevel, be able to adjust these services, be able to check your default and current runlevels, and be able to change the default and current runlevels.

> The next few pages describe the traditional System V (SysV) initialization system. Upstart and systemd differ from this, although they provide enough compatibility features that many of the tools and concepts described with respect to SysV also apply to newer systems. Upstart and systemd provide their own additional tools, though.

# Runlevel Functions

Earlier in this chapter, I described single-user mode. To get to this when booting Linux, you use the number 1, the letter S or s, and the system single=is an option passed to the kernel by the boot loader. Single-user mode is an available runlevel for your system. Available runlevels on most systems are the 0 through 6. The letters S and s are synchronous with runlevel 1 as far as many utilities are concerned. Runlevels 0, 1, and 6 are reserved for special purposes; the remaining runlevels are available for whatever purpose you or your Linux distribution prefer. Table 5.1 summarizes the conventional uses of the runlevels. Other assignments—even runlevels outside the range of 0 to 6—are possible systems, but such configurations are rare. If you enter peculiar runlevel numbers, consult /etc/initab—it defines them and often contains comments explaining the various runlevels.