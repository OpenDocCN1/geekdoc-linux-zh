![](bbox=[0.55, 0.02, 0.95, 0.35])

# Hour 7

# System Configuration and Startup Scripts

Every computer is different; each machine in use in the world today has its own customized behavior set by its owner, which controls how it behaves, what services or programs it runs, and what it should do automatically when it's booted up. In the case of FreeBSD and other UNIX operating systems that have the capacity to be used as servers on the Internet, it's exceptionally important to be able to tune your system so that it's optimized either for serving clients over the network or for running as a desktop workstation.

For most users, the process by which FreeBSD starts up—probing for installed devices, bootstrapping its various disk partitions, launching the kernel, mounting filesystems, and doing all the little housecleaning duties necessary for an efficient multiuser operating system—is of little interest. However, if you want to configure your system to your taste, it's a good idea to have some understanding of what FreeBSD is doing when it spews all those mysterious lines onto your screen after you turn on the computer.