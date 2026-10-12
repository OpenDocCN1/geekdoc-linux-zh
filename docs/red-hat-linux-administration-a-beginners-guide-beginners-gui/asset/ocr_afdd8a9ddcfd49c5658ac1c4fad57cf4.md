![](bbox=[0.17, 0.12, 0.79, 0.47])

**Figure 2-23** Create a boot disk to simplify system recovery.

> **WARNING**
> 
> If you chose not to install a boot loader, *you must create a boot diskette, or you won't be able to boot Linux.*

# Configuring the X Window System

The X Window System is the basis for the graphical user interface in Linux. It is what communicates with the actual video hardware. Programs such as KDE and GNOME (which you are more likely to have heard about; if not, read the next module) use the X Window System as a standard mechanism for communicating with the hardware.

What makes the X Window System interesting is that it is not coupled with the base operating system. In fact, the version of X that Linux uses, *Xfree86*, is also available for many other UNIX-based systems, such as those from Sun. This means it is possible to run a server *without* ever starting the graphical environment, and it is often a good idea to do so. By having the GUI turned off, you save memory and system resources that can instead be used for the actual server processes.