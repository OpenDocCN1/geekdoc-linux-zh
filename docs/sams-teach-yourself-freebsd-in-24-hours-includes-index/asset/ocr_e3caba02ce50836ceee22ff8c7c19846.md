+   - You can administer FreeBSD from the command line remotely through any system that has a terminal emulator, even if it is not a UNIX system. With Windows, you need special software to do remote administration, and that software generally only runs on Windows.

The argument can also be made that FreeBSD is much more stable and secure than Windows. A properly designed graphical user interface can make system administration much more straightforward than in a command-line-based system; but because of the arcane nature of the Windows' system layout, its interface is hardly any more intuitive than that of FreeBSD. The really nasty part, too, is that the Windows' graphical interface leads people to believe that it's easier—with the result that a great many Windows servers in the world are configured improperly and insecurely, as well as administered by people who think it's still better than if they'd used Linux or FreeBSD.

# System Requirements

The system requirements for FreeBSD depend on what you intend to do with the system. For a typical workstation setup that will run the X Window System (a graphical interface system similar to Windows or Macintosh, also referred to as X or X11), the following minimum system requirements are recommended:

+   - Pentium class processor
+   - 64MB of RAM
+   - At least 300MB of free hard disk space
+   - SVGA or better video card compatible with the X Window System (see Appendix A, "Resources for FreeBSD Users")
+   - Three-button mouse

It is possible to use the X Window System with a two-button mouse. However, unlike Microsoft Windows, X relies a great deal on the third mouse button. It is much easier to work in X with a three-button mouse.

If you have no intention of running a graphical environment, you can often get by with a lot less. In fact, if all you want is to set up an email server, router, or low end Web server, you can get by with even a 486.

# Deciding How and Where to Install FreeBSD

There are two primary ways you can install FreeBSD on your system. Most people new to the operating system will probably want to opt for the dual boot method. With a dual