# 18.5 Modules or Compiled In?

# 18.5 Modules or Compiled In?

One thing to note here is that not all drivers behave the same as a module when compiled into the kernel. This can range from slight differences in functionality to its simply not working at all.

The choice of when to make a particular feature available as a module or to compile it is usually fairly straightforward. In general, if it is infrequently used and performs as needed as a module, you should compile it as a module. This often includes things like floppy disk drivers (in this day of networking), how often do you use the thing anyhow?, drivers for other filesystem types (Cary uses DOS fs driver as often as he uses his floppy disk), CD-ROM drivers, for sound cards, or networking drivers on a machine that uses dial-in PPP for access.

If the feature is used frequently or continually, then really isn't much point in compiling it as a module since it will be loaded all the time anyway. This includes items such as your hard disk controller or SCSI controller, network drivers on a machine permanently networked, AppleTalk drivers on a fileserver for your Mac network, and so forth.

In cases where functionality between the compiled version and the module differs, it is usually noted in the help pop-up for that option and in any related HOWTOs.

It should be noted that these are for the most part just guidelines. Ultimately you need not compile in your kernel only what you need to boot your machine.

# 18.6 Dive On In!

Let's go and outline how you might roll a kernel for a networked Linux machine you're using as desktop machine and a file server for a network of Windows and Mac machines. You also have a sound card (they're cheap and you have a hundred CDs at home you could also be listening to at). The machine has a SCSI controller with a CD-ROM and hard drives attached to it.

First, make sure you have the kernel sources installed. If you do, you may decide you want to get a more recent version. The default location is in /usr/src/linux which may be a link to linux-x.y.z, where x.y.z is a kernel revision. Once you are in x, highly recommended), type “usr/src/linux, typemake config” (assuming this will do some preliminary work and then bring up a window with buttons that take you to various sections of the kernel configuration.

As you may have guessed, the first time through it's best to start at the top and go through all the menus.