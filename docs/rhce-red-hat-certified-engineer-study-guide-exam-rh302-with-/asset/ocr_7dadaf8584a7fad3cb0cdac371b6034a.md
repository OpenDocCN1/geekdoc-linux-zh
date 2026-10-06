# Summary 653

Now complete Exercise 26.5, which asks you to study the main X configuration file.

# EXERCISE 26.5
Examining the /etc/X11/XF86Config

Because of variation in video characteristics, the X configuration is likely to vary significantly from system to system. Compare the XF86Config file of a properly configured X installation with the configuration shown in this subsection. What similarities and differences do you find?

# Summary

In this chapter, you learned about the installation and configuration of X. The most important topics covered are:

**The X Window System (X)** provides the graphical user interface used with Red Hat Linux. Implementations of X are available for a variety of Unix and non-Unix platforms. The version of X distributed with Red Hat Linux is published by the XFree86 Project.

**Servers and Clients** The X program that manages a user interface is called an X server. An application or other program that uses an interface is called an X client.

**Installing X** Installing X involves installing several packages. One of the most important is the package containing the X server, which must be chosen to suit the type of video adapter installed in a system.

**Configuring X** You can configure X using a variety of tools, the following:

+   - Xconfigurator
- XF86Setup
- xf86config
- SuperProbe
- xvidtune