# Note

You might occasionally see references to “Linux 6.0” or some similar high number. Unless you’re reading this book several years into the 21st century, such references are incorrect, and are probably mangled references to a specific Linux distribution, such as Red Hat Linux 6.0. The distributions, as well as all Linux programs, have their own numbering schemes that are completely independent of the kernel’s—and each other’s—numbering schemes.

All other things being equal, you probably want to run the latest kernel in the latest release series that you can. I don’t recommend updating every time you see a new kernel appear on the FTP sites, though—chances are that the change from, say, 2.2.9 to 2.2.10 won’t be substantial enough to warrant the time and effort it takes to obtain it, compile it, and reboot your system. There’s always a chance that an upgrade will break something, too.

If you want to live on the edge, or if you need a particularly new feature, you might want to consider using a development kernel. I recommend this only if you’re already experienced with Linux, though, or if you absolutely must have some feature that’s not supported in a release kernel. Even if you need a new feature, you might be able to patch it into a release kernel, thus avoiding the possibility of destabilizing some other component of your system.

# Obtaining a Kernel

Most Linux FTP sites have an archive of Linux kernels. You can obtain a kernel in either Red Hat Package Manager (RPM) form or as a “tarball”—a file whose name ends in .tgz or .tar.gz. I generally prefer to get tarballs, but some people prefer RPM files. Pick whichever you like.

If you get a tarball, you’ll need to extract it with the tar command. Follow these steps:

+   1. Change to the /usr/src directory by typing
+      `cd /usr/src`
+   2. Create a new subdirectory for the new kernel. For instance, if you’re installing kernel 2.2.9, type
+      `mkdir linux-2.2.9`
+   3. If you already have Linux kernel source, there will probably be a symbolic link from its directory to linux. Remove that link by typing
+      `rm linux`