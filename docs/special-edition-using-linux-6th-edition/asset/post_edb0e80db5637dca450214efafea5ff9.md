
Unlike most other window systems, the base window system of the X Window System doesn't provide user interface objects such as scrollbars, command buttons, or menus. The user interface items are left to the higher-layer components and the window manager. Therefore, users have much greater flexibility in how things appear and what interface they prefer.

X applications include not only window managers, but also games, graphics utilities, programming tools, office applications, and many other tidbits. Just about any application that you need has either been written for or ported to the X Window System.

The X Window System implements a window manager to handle the task of creating and controlling the interface that makes up the visual portion of the X Window System. It isn't to be confused with the OS/2 Presentation Manager or the old Microsoft Windows Program Manager. Both of them are closer to the idea of a desktop than a window manager.

For the not-so-faint-of-heart, XFree86 also includes programming libraries and files for programmers who want to develop their own applications under XFree86 or compile X applications available on the Internet. Although the topic of creating X applications is beyond the scope of this book, ample documentation is available on any number of Internet distribution sites, such as www.xfree86.org, and on many CD-ROM distributions to help you gain the foothold necessary to create applications for XFree86. Today many programmers, however, prefer to write applications targeted at GNOME or KDE rather than pure X applications. These environments provide helpful abstraction layers for programmers; these greatly simplify writing graphical applications.

## WHAT IS A CLIENT/SERVER SYSTEM?

The X Window System is a client/server system controlled by two individual pieces of software. One piece runs on the client and the other runs on the server. The client and server pieces of this puzzle can be on different systems or, as is the case with most personal computers, both pieces can reside on the same machine.

*Client/server* is one of the major buzzwords used in the computer industry today. Like most basic concepts in the industry, client/server has been overplayed and overused to the point of confusing the average computer user. In the traditional sense, a *server* is a machine that just provides resources—disk drive space, printers, modems, and so on—to other computers over a network. A *client* is the consumer of these services; in other words, a client uses the disk space, printer, or modems provided by a server.

In the X Window System, the relationship of client and server is quite different, and might appear backward to many users. Under the X Window System, the server displays the output of the client. This concept might seem a bit confusing at first, but it will make sense when you become more familiar with the X Window System.

An X client is made up of the programs and resources necessary to run an application. The resources reside on the client's system (remember that the client and server systems can be on the same machine), whereas the application is displayed and interacted with on the server system. For example, if you run xcalc on your Linux system using XFree86, then XFree86 (specifically a program such as `/usr/X11R6/bin/X`) is the *X server*, and xcalc is the *X client*. The X server must be running on your local machine (so that it can display your information), but the X client can be on any machine that you can connect to.

The capability of an X application, which is the client, to run under a server located on either the same computer or on another computer is called *network transparency*. Thus, it doesn't matter whether an X application runs on a local or remote machine. This capability can be used to run time-consuming tasks on another machine, leaving the local machine unencumbered to perform other tasks. It can also be used to run applications on other operating systems. Using a non-UNIX X server such as WRQ's Reflection X (http://www.wrq.com/products/reflection/rxinfo.html), you can run your favorite X clients on your Linux workstation but display them on a connected machine running Microsoft NT. The reverse is not true, however, because NT does not know how to run X clients and cannot easily display its own clients on remote servers.

> **Tip**
>
> > It is possible to display applications running on a Microsoft Windows machine to your Linux workstation using VNC (http://www.uk.research.att.com/vnc/), a free product currently maintained by AT&T. VNC includes many remote display features for Windows, Macintosh, Linux, and other systems.

## OUTPUT CAPABILITIES

The base window system provides the X Window System with plenty of bit-mapped graphical operations. The X Window System and X applications use these operations to present information graphically to the users. XFree86 offers overlapping windows, immediate graphics drawings, high-resolution bit-mapped graphics and images, and high-quality text. Whereas early implementations of the X Window System were mostly monochrome-based, modern implementations like XFree86 support a wide range of color systems.

The X Window System also supports the multiprocessing capabilities of Linux. Each window displayed under the X Window System can be a separate task running under Linux.

## USER INTERFACE CAPABILITIES

The X Consortium did not define standards for user interfaces. At the time very little research had been done on user interface technology, so no clear interface was considered the best. In fact, even today, unilaterally declaring one interface the best can alienate many people. The preferred look and feel presented by the user interface is a very personal decision.

The X Consortium wanted to make the X Window System a standard across UNIX and UNIX-like workstations, which is one reason it is available freely on the Internet. Making the X Window System freely available fosters interoperability, which is the cornerstone of open systems. Had the X Consortium dictated a user interface, the X Window System might not have gained its current level of popularity.

## Input Capabilities

Systems running the X Window System typically have some form of pointing device, usually a mouse. XFree86 requires a mouse or a device such as a trackball that emulates a mouse. If you don't have such a device, you can't use the XFree86 system with Linux. The X Window System converts signals from the pointing device and from the keyboard into events. The X Window System then responds to these events, performing appropriate actions.

## Installing the XFree86 System

You probably installed the XFree86 system while installing the entire Linux package from your particular distribution's CD-ROM. An implementation of the X Window System is contained in the XFree86-* RPMs or deb packages. If you didn't install XFree86 at that time, you can use RPM or deselect to install it later. First, however, you must verify that you have the appropriate hardware for XFree86.

## Choosing a Version of XFree86

Before installing XFree86, you should decide which version to use. Two versions are currently available: 4.0.1 and 3.3.6. Some distributions even allow you to choose which one you would like during install.

Version 4 represents a major re-design in XFree86. It provides several new features and much simpler configuration (Modelines are no longer needed for normal setups). Because of the massive re-design, however, the version 4 line is not nearly as well tested as the venerable 3.X line.

If you have fairly standard hardware and are unfamiliar with configuring XFree86, you should probably choose 4.0.1.

If, however, you have a working 3.3.X XF86Config, or you have a card that is not supported well under 4.X (see http://www.xfree86.org/4.0.1/Status.html), then you should probably stay with 3.3.6.

Because most development will go into the 4.X line, this book will focus on 4.0.1.

> **Note**
>
> > Other implementations of the X Window System are available for Linux, such as the commercial Metro-X (http://www.metrolink.com/metro/ess.html) and Accelerated-X (http://www.xig.com). Commercial solutions are worth considering if you have hardware that XFree86 doesn't support, are interested in some of its special features, or if you need better performance than XFree86 can provide.

## Ensuring Hardware Support for XFree86

You must make sure that you have the proper hardware to run X Window System, the proper amount of memory, and the necessary disk space.
