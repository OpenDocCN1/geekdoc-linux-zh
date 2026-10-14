+   5. Watch as the system boots. Note that the system takes less time to boot because it starts fewer services than normal. After a few moments, you see a text-mode command line at the bottom of the screen. You can now work in Linux, though neither multiple virtual terminals nor networking are available. Note that you never entered a password.

+   6. Enter whoami to discover which user account you are working as.

+   7. Enter the passwd command to change the root password.

+   8. Enter a new password for root as prompted. Repeat the entry as prompted. The root password has now been changed.

+   9. Enter exit to exit from single-user mode. You immediately see messages as the system changes to run level 5. After a few moments, the graphical login screen appears.

# CASE PROJECTS

![](bbox=[0.08, 0.66, 0.15, 0.78])

# Booting the System and Managing Services

+   1. Reboot your computer several times and make a list of all the setup menus that you see mentioned. Enter each one and explore the options that it permits you to set up. Note the order in which different hardware components have their turn at initialization. Do you see any configuration options that you might want to change? Do you see any that you think might affect the performance or security of your Linux system?

+   2. In Hands-On Project 9-4, you started the system in single-user mode to reset the root password. Summarize in a one-page report what single-user mode does, what security hazards it presents in a Linux lab, and how you might use what you have learned about hardware configuration to safeguard against those hazards. Review the man page for the boot loader you have installed (LILO or GRUB) and add comments about how the boot loader can be configured to protect against these or similar security problems.

+   3. The method of starting and managing services using multiple scripts in /etc/rc.d/init.d (or a similarly named directory) is called System V initialization, after the System V UNIX systems in which the model was first used. What advantages and disadvantages do you see in using this method? Use the Internet or other sources to research other UNIX-related operating systems that use different methods to control daemons. In particular, you might look at the BSD version of UNIX (you can start with www.freebsd.org or www.netbsd.org). What other methods do you see and how do they compare in your eyes?