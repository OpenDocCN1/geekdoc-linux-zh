# 190 Part II + The SUSE System

machine the applications we are running on; however, the network transparency of X huge benefits that we shall examine further in this chapter.

The common complaints that are often heard about X are the problems of configuration (largely but not entirely a thing of the past), problems with fonts (antialased display of fonts in all situations such a long time to become available on Linux), lack of direct support for hardware acceleration, and other performance issues. Some of these difficulties are directly related to the fact that implementations of X have to be backward-compatible and standards-compliant.

Largely through the efforts of open source operating systems such as Linux, FreeBSD, OpenBSD, NetBSD, X Window system configuration today is quite easy, resisting the ease of installing and configuring graphics on any modern operating system. The XFree86 project's generic xconfig utility is easy to use but requires some knowledge of your system's graphical capabilities. The X.org project's xconfig utility is very and has has information requirements. The vendors that support Linux and BSD distributions have stepped in to make things even easier: the saxx utility developed by SUSE and provided with all SUSE Linux distributions provide a simpler, almost automatic mechanism for configuring and fine-tuning X on a modern Linux system.

# X Window System Concepts

When using X, a user is running a graphical application, say an xterm. The xterm is the client; it communicates with an X server, which does the job of displaying it. There is no requirement that the client and the server must run on the same machine; the client and the server simply need to be able to communicate with each other. In addition, the X server needs to be willing (from a security point of view) to display the output of the client, and the client needs to be started in an environment that includes suitable information about how it will display its output (typically the DISPLAY environment variable).

In simple cases (including cases in which you are explicitly logging in remotely by ssh), you don't need to think about any of this — everything just works.

# Window Managers

The X server itself knows how to display the output of a program, but it does not know how to manage the different programs that it is displaying — that is the job of the window manager. The window manager looks after the behavior of the application windows, their "decorations," the look and feel of their borders and control widgets (such as close and maximize buttons), the way they interact with the mouse and keyboard, and so on.