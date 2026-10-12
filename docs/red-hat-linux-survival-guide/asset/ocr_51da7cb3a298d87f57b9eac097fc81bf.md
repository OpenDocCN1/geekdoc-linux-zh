# What Is XFree86?

XFree86 is a freely distributable implementation of the X Window System. It is developed by the XFree86 Project, Inc., a nonprofit organization. Although XFree86 is based on the Open Group’s X Window System, it has its own development goals. Traditionally, XFree86 was developed for the Intel x86 family of processors, but it now runs on other platforms, such as Compaq/Digital Alpha processors as well. The official Xfree86 Web site is located at http://www.xfree86.org/. The official Red Hat Linux comes with the latest XFree86 distribution, and so that’s the version of X discussed in this chapter.

# Preparing Your System for X

The XFree86 X Window package requires a lot of system resources to be comfortably usable. Although you can run XFree86 on an Intel 486 with a mere 4MB of RAM, the uses of such a system would be limited. The following sections discuss the system requirements that you need to consider before you install XFree86 on any system.

# RAM requirements

RAM is a resource you can never have enough of. Having plenty of RAM helps just about everything you do on a multiuser system such as Red Hat Linux. My personal experience shows that having 64MB of RAM with 128MB of swap space provides a very comfortable user experience on a Red Hat Linux system running XFree86 on a regular basis. However, if you would like to run XFree86 while serving Web pages with the Apache Web server and providing NFS or Samba file sharing services, the amount of RAM you need depends on how loaded your server gets at peak hours. At the low end, I recommend that you install 128MB of RAM with 256MB of swap space; as your load increases, you can always add more and more RAM to improve your server performance.

# Video card requirements

Not all video cards are supported by XFree86, so don’t forget to check the XFree86 Web site for a list of supported video cards. I recommend a brand-name PCI video card with at least 4MB of video memory. In this