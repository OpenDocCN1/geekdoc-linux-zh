# # **UPGRADING TO A BETTER SERVER**

If you have a server, an upgrade may be all it needs to run better

You may already have a server, in which case instead of actually building a better server from scratch, you may want to just upgrade your server to be more efficiently than it was before. There are several ways of doing this depending on how you want to improve your server, and most of them require a hardware upgrade. If you decide to go down the hardware upgrade route, refer overleaf to see the kind of hardware we recommend and learn some quick tips on how to install it if you're new to system building.

The easiest upgrade is storage space, especially for file servers. For Linux systems you can quite simply just add an extra hard drive into the case, as long as you have room in terms of spare SATA cables and power. Once installed, reboot your system and you can start adding the hard drive under /etc/fstab so that it automatically mounts to a specific location – in this case, the location on the filesystem which needs a bit more storage. Otherwise, you can create a clone of the system using Clonezilla (clonezilla.org) and then restore it to a larger hard drive with almost no change in the way it works.

![](bbox=[0.51, 0.51, 0.91, 0.61])

**Above** RAM is much more important in a server than a desktop PC, as you need to serve several people

For other system hardware, you need to ask yourself which section is slow and perhaps needs upgrading. If it's a little slow for certain operations and computational tasks, your first port of call should be upgrading the CPU. Depending on how forward-thinking you were when building or buying the original system, the motherboard may support newer processors than the one inside it. Find out the socket information and start a search for a new CPU. While you'll need enough RAM to support the CPU and whatever the server is being used for, you'll always need more for one handling web services than file-serving. You can easily replace this kind of parts without having to reinstall Linux.

If you're doing heavy computational tasks and can use hardware acceleration for it, look at getting a new video card to support it – although not many servers will even require one, let alone a good one.

If you've reached the limit of your current motherboard, it's time to gut the system and get a new mobo, CPU, RAM and GPU if you need it – backing up important files and settings is a good idea before you attempt this as Linux may not be able to work with completely new hardware without a reinstall.

Otherwise, if you need a software upgrade then refer to whatever guide is relevant to you in this feature on how to install and setup a new distro.