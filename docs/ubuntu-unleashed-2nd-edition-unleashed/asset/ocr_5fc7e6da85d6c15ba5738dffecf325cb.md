# CHAPTER 6

# The X Window System

# IN THIS CHAPTER

+   - Basic X Concepts
+   - Using X11R7
+   - Starting X
+   - Selecting and Using Window Managers
+   - The GNOME and KDE Desktop Environments
+   - Reference

The X Window System, the graphical networking interface found on many Linux distributions, provides the basis for a wide range of graphical tools and window managers. More commonly known as just X, it can also be referred to as X11R7.2 and X11 (such as that found on Mac OS X). Coming from the world-renowned Massachusetts Institute of Technology, X has gone through several versions, each of which has extended and enhanced the technology. The open source implementation is managed by the X.Org foundation, the board of which is made up of several key figures from the open source world.

The version of X included with Ubuntu 7.04 is 7.2, which was released in February 2007.

The best way to think about how X works is to see it as a client/server system. The X server provides services to programs that have been developed to make the most of the graphical and networking capabilities that are available under the server and in the supported libraries. X.Org provides versions for many different platforms, including Linux and Mac OS X. Originally implemented as XFree86, X.Org was forked when a row broke out over certain restrictions that were going to be included in the XFree86 license. Taking a snapshot of code that was licensed under the previous version of the license, X.Org drove forward with its own implementation based on the code. Almost in unison, most Linux distributions turned their back on XFree86 and switched their development and efforts to X.Org. In this chapter you will learn how to work with the version of X that is included with Ubuntu. We will look at the fundamentals of X, as well as how to get X to work with any upgrades that might affect it, such as a new graphics card or that new flat panel display you just bought.