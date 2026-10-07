while trying to do two things at the same time.) Although many people ignore the rule about using root only when necessary, most of them eventually find out why this rule is important!

# # Starting and Stopping the System

There are several ways of booting the Linux operating system, as well as a few ways to safely shut it down. Some were mentioned earlier in this book. Because Linux can be installed in many different ways, there is no single "right" method of booting the operating system, so we must look at both hard-disk–based and floppy-disk–based boot procedures.

# ## Booting from a Floppy

A boot floppy, as its name implies, is a floppy disk that boots the Linux kernel. A boot floppy has the root partition installed on the floppy itself instead of the hard drive (although both may coexist). Without the root partition, Linux would be unable to find the hard drives for the rest of the operating system.

You can create Linux boot floppies with the setup routine included in most distributions of the operating system. Check the documentation or information files that came with your Linux distribution, if there are any. Alternatively, most Linux setup utilities have a menu-driven interface that prompts you for a boot floppy setup when you rebuild or reconfigure the kernel. You should use this procedure to make a boot floppy, which is also useful for emergencies.

In most cases, a boot floppy is used only in emergencies when your system won’t start up normally. The boot floppy enables you to load Linux and then mount the hard drives that are causing the problem to check for damage. Luckily, this is not required very often. If you haven’t used LILO to choose the partition to boot or set your boot sequence to Linux by default, you may need the boot floppy to start up Linux. In this case, the boot floppy is much like a DOS boot floppy.

You can create a boot floppy from scratch by copying over the kernel image from the hard drive. The kernel image is usually in the file `vmlinuz`, `vmlinux`, `Image`, or `/etc/Image`, depending on the distribution of Linux. The Slackware distribution uses `vmlinuz`, which is a compressed kernel (hence the z in the name). Compressed kernels uncompress themselves as they are loaded into memory at boot time. The `vmlinuz` image expands to `vmlinux`. (Compressed kernels take up less disk space; that’s why they are used.)