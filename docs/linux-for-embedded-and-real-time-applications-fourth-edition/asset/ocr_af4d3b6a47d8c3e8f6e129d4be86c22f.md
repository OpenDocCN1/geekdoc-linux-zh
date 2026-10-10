# **Introducing BusyBox**

Even if your embedded device is “headless,” that is it has no screen and/or keyboard in the usual sense for user interaction, you still need a minimal set of command line utilities. You will no doubt need *mount*, *ifconfig*, and probably several others to get the system up and running. Remember that every shell command line utility is a separate program, with its own executable file.

The idea behind BusyBox is brilliantly simple. Rather than have every utility be a separate program with its attendant overhead, why not simply write one program that implements *all* the utilities? Well, perhaps not all, but a very large number of the most common utilities. Most utilities require the same set of “helper” functionality, such as parsing command lines and converting ASCII to binary. Rather than duplicating these functions in hundreds of files, BusyBox implements them exactly once.

The BusyBox project began in 1996, with the goal of putting a complete Linux system on a single floppy disk that could serve as a *rescue disk* or an installer for the Debian Linux distribution. A rescue disk is used to repair a Linux system that has become unbootable. This means the rescue disk must be able to boot the system and mount the hard disk file systems, and it must provide sufficient command line tools to bring the hard disk root file system back to a bootable state.

Subsequently, embedded developers figured out that this was an obvious way to reduce the Linux footprint in resource-constrained embedded environments. So the project grew well beyond its Debian roots, and today BusyBox is a part of almost every commercial embedded Linux offering, and is found in a wide array of Linux-based products, including numerous routers, and media players.

BusyBox calls itself the “Swiss army knife” of embedded Linux because, like the knife, it is an all-purpose tool. Technically, the developers refer to it as a “multi-call binary,” meaning that the program is invoked in multiple ways to execute different commands. This is done with symbolic links named for the various utilities. These links then all point to the BusyBox executable.

# **Configuring and Installing BusyBox**

The version of BusyBox running on my BBB is 1.20.2. Go to the website in the “Resources” section and download that version, or any other one that matches your board or strikes your fancy. Oddly, even though the BBB incorporates BusyBox, it appears there are only two links to it. This may be because we are running a Debian distro, and Debian itself does not use BusyBox.