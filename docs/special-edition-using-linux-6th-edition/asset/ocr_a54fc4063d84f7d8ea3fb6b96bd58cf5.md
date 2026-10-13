By following the instructions at this site (or at one of its many mirrors), you can see the contents of several thousand different package files located at various sites on the Internet.

The Freshmeat Web site is another online resource for tracking recent updates to software. You can access it at http://www.freshmeat.net/. Freshmeat is a fairly definitive guide to current releases of software available for Linux. Much of the software referred to on Freshmeat is provided as tar files. Often, however, when a new release of software is mentioned on Freshmeat, the software is made available as a package soon after.

> **Caution**
> 
> When downloading RPM packages from the Internet, be sure to check which distribution of Linux they are intended to run with. Although many packages built for one vendor's distribution of Linux run perfectly fine on another, it is wise to check the package information, file lists, and dependencies to ensure that the package will operate correctly with your system.
> 
> The section "Library Compatibility" in Chapter 17, "Building/Rebuilding a Package," discusses how to resolve some issues with programs that have been compiled for a Linux system with different shared libraries.
> 
> If you can find the software you need in a package specifically built for your distribution, use it. However, you also can use packages built for other distributions of Linux. When in doubt, try to find out by searching or participating in mailing lists or newsgroups related to that software; alternatively, you can check to see whether others have already tried the package with OpenLinux and find out what success they have had with it.

# DECIDING WHICH UTILITY TO USE

As with many operations in Linux, more than one way exists to manage packages. The three preferred utilities are rpm for command-line use and kpackage for graphical use under KDE and GnoRPM for graphical use under GNOME. rpm offers the capability to perform more complex operations, whereas kpackage and GnoRPM are easier to use. The descriptions in this chapter focus on the rpm command.

# SECURITY CONCERNS

With the large amount of software available for your Linux system, and with it coming from a variety of sources, you might wonder if all of it is harmless. When you add any piece of software to your system, you want to be sure that it will do what you expect it to, and no more. You can be quite certain that software packages directly from a commercial vendor or other major distributor can be trusted because they were built and signed by developers who have their reputation to protect. If the site you downloaded your package from is public and widely used, you also have some degree of assurance that the package is safe. However, if you are ever unsure of the software in a package, RPM includes two features that enable you to protect yourself.

First, you can verify that the installation itself will not do funny things to your system. You can use RPM to examine the exact scripts that will be executed to install the software. Because you install a package as the root user on your system, it is crucial that the scripts used during installation don't do strange things (such as installing trapdoors or Trojan Horses).

# PART III
CH 16