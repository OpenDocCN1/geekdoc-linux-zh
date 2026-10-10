PPC, you will be using a unique but proven brand of Linux. If you use Debian PPC Linux at this point, you are a true hacker and a budding high priest of the GNU generation.

Many tasks covered in this chapter require root permission. While some tasks are universal, and apply to all Linux distributions, this book concentrates on using Red Hat-based Linux distributions for the PowerPC or SuSE Linux PPC on Power Macs.

# ## Configuring X

Chances are very good that the installation software included with your PPC Linux distribution has successfully configured the X Window System to work with your system. However, if you need to make changes or reconfigure X to get a bit better performance, make sure to read Chapter 7, "X11 and Window Managers." That chapter’s section "Configuring X11" is chock full of details about using at least three different software configuration tools to get X working optimally with your computer.

Configuring X involves creating an accurate configuration file named *XF86Config*. This file is simply a text file containing directions for a software program called a *server*. When you use Linux without a graphical interface, you are using Linux in a text-based, or *console* mode. But when you use a graphical interface with Linux, you will use the X Window System and its server named *xfsess*.

X works very well with Apple’s Power Mac hardware. No major problems have been reported in getting X to work correctly on any model in the currently supported Power Mac model lines. This means that if you have an iBook, TiBook, or Apple G4 Cube, you can expect to configure a working graphical interface for Linux using X. If you do have problems, then check with your Linux distribution’s vendor for up-dates, errata, or bug fixes. You are sure to find an answer for any problem related to X.

# ## Keyboard and Mouse Issues

When you use Linux in the *console* mode, mouse support is provided by the general-purpose mouse driver, *gpm*. This is a *daemon*, or program that runs in the background while you use Linux, and gives support for highlighting, copying, and pasting of information. When you use X during an X session, your mouse cursor is known as a *pointer*, and is supported by the XFree86 server.

You can change the fonts and the font color while you work at the console by using the *setfont* and *echo* commands. Linux comes with nearly 100 fonts installed under