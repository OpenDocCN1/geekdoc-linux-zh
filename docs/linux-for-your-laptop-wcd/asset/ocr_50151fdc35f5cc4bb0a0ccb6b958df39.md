two main varieties of the latter type: mice with a switch to select the protocol, and mice that default to 1 and require a button to be held at boot-time to select protocol 2. Some mice can be convinced to do 2 by sending a special sequence to the serial port (see the ClearDR/ClearRTS options).

Enter a protocol number: 4

In the first section, you're asked what type of mouse you use on your notebook. Type a number (such as 4 for PS/2) and press Enter. Continue through the prompts, answering questions to configure X11.

# ## Installing XFree86 4.0

While this book was being developed, The XFree86 Project, Inc. released a new version of X11 for Linux named XFree86 4.0. This release provides a number of changes and new features that make it a radical departure from previous versions of XFree86. One of the biggest changes involves the number of X11 servers included in the distribution. XFree86 releases before 4.0 included one server for each “family” of graphics chipsets, such as XF86_Mono, XF86_VGA16, XF86_SVGA, XF86_Mach64, XF86_S3, and so on. The new XFree86 4.0 includes one server! The single XFree86 4.0 server uses loadable modules, each representing a type of graphics card. This new modular approach makes the job of creating, maintaining, and updating XFree86 much easier to accommodate new graphics cards, because support can be rolled into a new, separate module instead of writing an entirely new server.

The XFree86 software is included with nearly every Linux distribution. Under Red Hat, Mandrake, and Yellow Dog Linux, the XFree86 files, including servers, fonts, clients, and documentation, are bundled in Red Hat Package Manager (.rpm) files. These files are then decompressed and installed on your notebook during installation.

To install the new XFree86 4.0 as distributed by The XFree86 Project, Inc., you must download a series of archives in a compressed tar format. These types of archives, usually ending in .tar.gz or .tgz, are known as compressed *tarballs*. They are usually decompressed manually or by a shell script or installation program. Point your browser to ftp://ftp.Xfree86.org or a Web page with similar content (known as a *mirror*) and download the minimal set of files listed in Table 6.1.