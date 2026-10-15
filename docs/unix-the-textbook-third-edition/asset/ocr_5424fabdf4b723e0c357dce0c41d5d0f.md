capable device) connected to a server. It is connected by a high-speed communications link to another single computer or multiple computers that are all interconnected with a LAN or the Internet. At the terminal, and the console or command window that appears on its screen, your interface with the operating system runs on a single, or even multiple, other computer(s). This is a shared resource method, where several users on many different terminals can share a single UNIX system.

+   b. You sit at a stand-alone computer, and via software such as PuTTY, Secure Shell (SSH), or SSH X Windows forwarding (a variant of TCP port forwarding), you connect to another system over a high-speed telecommunications link. The PuTTY or SSH software then becomes your graphical connection, allowing you to log on and use a remote computer or system that is running UNIX. This is usually a shared resource method, where several users on many different remote computers can share a single UNIX system.

+   3. Virtual: You have a UNIX or NIX-like operating system such as LINUX, OS X, or another operating system installed and running the computer you are sitting in front of, and you have installed a virtual environment such as VirtualBox or VMware on that computer. Then, when you want to use a UNIX system, you simply switch environments so that the UNIX system in the virtual environment is what you are using to interface with the computer hardware.

We do not cover virtual connections in this chapter, but in Chapter 25, “Virtualization Methodologies,” we cover virtual environments such as VirtualBox.

In the following subsections, we present three practical, useful, easy, and popular ways of connecting and logging on and off a computer running the UNIX system, as outlined in Section 2.3.

The three ways we show are:

+   1. Stand-alone login and logout for PC-BSD and Solaris.
+   2. Remote login via the PuTTY program from a computer running Microsoft Windows to a UNIX computer running PC-BSD.
+   3. Remote login via an SSH client from a UNIX client computer running PC-BSD UNIX to another remote UNIX host computer.

What is common to all three of these ways is that your first task is to identify yourself correctly as a valid and autonomous user to the UNIX system. Doing so involves typing in a valid username, or login name, consisting of a string of valid characters. You then have to type in a valid password for that username.