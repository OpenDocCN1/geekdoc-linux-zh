# Introduction and Installation SuSE Linux
PART I

nThis chapter will introduce you to the major components of the graphical interface for SuSE Linux: The X Window System. X11 is not configured during your SuSE Linux installation, this chapter will also introduce you to the software tools, such as Sax, XF86Setup, and xf86config, which you can use to set up a graphical interface for Linux. The chapter begins with a little background on X11, lists the major components of X11, and then shows how to configure X for your computer's graphics card.

# Background on the X Window System

The X Window system is a networking windowing system that provides a base set of communications protocols and functions for building graphical interfaces for computers withmapped displays. You should never refer to the X Window system as X Windows; the proper terms of reference are X, X11, X Version 11, or the X Window system, version 11.

X was first developed at the Massachusetts Institute of Technology in the early 1980s. The first commercial release of X X10 in the mid-80s, with the first X11R release in 1987. Though the original MIT consortium has since dissolved and X now falls under ownership of The Open Group (a large consortium of computer companies), X11's general client/server model of operation has remained unchanged.

X was designed from the ground up to support networking graphics. Programs or applications under X are known as clients. X clients do not directly draw or manipulate graphics on your display, but instead communicate with your X server, which in turn controls your display. Although many home users run clients and an X server on a single computer, it is also possible to run multiple servers (X sessions) on a single computer and to launch clients from remote computers—and to have them displayed locally by a local server. This also means that it is possible to run X over various types of networks or even through a dial-up line.

The X Window system used with SuSE Linux is a collection of programs from The XFree86 Project, Incorporated (see the sidebar in this chapter on “The Future of X”). The latest version of X is X11R6.4, and according to XFree86 folks, "XFree86-4.0 will be X11R6.4 based."