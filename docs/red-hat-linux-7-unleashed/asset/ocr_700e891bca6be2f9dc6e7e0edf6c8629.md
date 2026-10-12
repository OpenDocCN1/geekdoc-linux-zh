# # What Is X11?

The X Window System is a networking windowing system that provides a base set of communications protocols and functions for building graphical interface clients for computers with bitmapped displays. You should never refer to the X Window System as X Windows; the proper terms of reference are X, X11, X Version 11, or the X Window System, version 11.

X was first developed at the Massachusetts Institute of Technology in the early 1980s. The first commercial release of X was X10 in the mid-80s, with the first X11R1 release in 1987. Though the original MIT consortium has since disbanded, and X now falls under ownership of non-profit X.Org, a consortium whose executive membership includes Compaq, Hewlett Packard, Hummingbird, IBM, SGI, and Sun Microsystems, X11's general client/server model of operation has remained unchanged.

X was designed from the ground up to support networking graphics. Programs or applications under X are known as *clients*. X clients do not directly draw or manipulate graphics on your display, but instead communicate with your X server, which in turn controls your display. Although many home users will run clients and an X server on a single computer, it is also possible to run multiple X servers (and X sessions) on a single computer and to launch clients from remote computers—and to then have them displayed locally by a local server. This also means that it is possible to run X over various types of networks or even through a serial dial-up line!

# # XFree86 or Another X11?

The X Window System used with most Linux distributions, including Red Hat's, is the collection of programs from The XFree86 Project, Inc. The version of X11 included with Red Hat Linux is XFree86 4.0.19, and is based on X11R6.4, or X11, revision 6.4.

> You can verify the version of XFree86 in use, even during an X session, by using the *-version* command-line option with the XFree86 command like this:
> 
> ```
> # XFree86 -version
> XFree86 Version 4.0.1 / X Window System
> (protocol Version 11, revision 0, vendor release 6400)
> Release Date: 2 August 2000
> ```
> 
> If the above is older than 6-12 months, or if your card is newer than the above list, look for a newer version before reporting problems. (see http://www.XFree86.Org/FAQ)
> 
> Operating System: Linux 2.2.5-22smp 1686 [ELF]
> Module Loader present