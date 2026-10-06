# Using X for Remote Access

As noted earlier, in “The X GUI Login System,” X is a network-enabled GUI. This fact enables you to run Linux programs remotely—you can set up a Linux system with X programs and run them from other Linux (or even non-Linux) computers. Similarly, you can use a Linux computer as an access terminal for X programs that run on a non-Linux Unix computer, such as one running Solaris. To do this, you first understand something of X network model, where the client and server systems are located, how X controls access to itself, and so on. You can then proceed to perform the remote accesses.

# X Client-Server Principles

Most people think of servers as powerful computers hidden away in machine rooms, and clients as the desktops that operate ordinary people. Although this characterization is often correct, it’s very wrong when it comes to X. X is a server, meaning that the X server runs on the computer at the user sits. X clients are the users run—xterm, xfontsel, LibreOffice, and so on. In most cases, the X server and its clients reside on the same computer, but this peculiar terminology doesn’t matter when you use X for remote access, you must remember that the X server runs on the user’s computer, while the X clients run on the remote system.

To make sense of this peculiarity, think of it from the program’s point of view. For instance, consider a Web browser as Firefox. This program accesses Web pages on a Web server computer. The Web server responds to requests from Firefox to load files. Just as Firefox loads files, it displays pages on the screen and accepts input from its user. From the program’s point of view, this activity is much like retrieving Web pages, but it’s handled by an X server rather than a Web server. This relationship is illustrated in Figure 6.3.

FIGURE 6.3 From a point of view, which, the X server works like a conventional network server as a Web server.

![](bbox=[0.305, 0.706, 0.672, 0.843])