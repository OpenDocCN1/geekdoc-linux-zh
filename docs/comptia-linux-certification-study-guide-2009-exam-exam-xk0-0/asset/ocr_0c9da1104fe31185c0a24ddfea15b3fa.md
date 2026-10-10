# Accessing Kernel and Architecture Information

What is commonly referred to as “Linux” is actually an amalgam of different components. Only the central core – the *kernel* – is “true” Linux. Much of the rest, including the all-important C compiler *gcc* and most of the user programs, have been provided through the GNU project and the Free Software Foundation. Because of this, many people prefer the more technically accurate (but hopelessly clunky) name “GNU/Linux.”

So, what is this Linux kernel? *The kernel* is a program that is started when a computer boots. It handles the coordination of all the system resources – allocation of memory, determining when to allow which program to be run by the processor, and managing communications between all the peripheral devices that are attached with the help of device drivers.<sup>7</sup>

Linux uses a *virtual file system* located at `/proc` to represent activity within the computer, and allow communication with various kernel and driver components. If you compare `ps -A` with `ls /proc`, you’ll notice that every process has its own subdirectory under `/proc`. There are also files for system hardware: `cat /proc/cpuinfo` will tell you anything you could ever want to know about your processor, and `/proc/version` knows all about your installed version of Linux. A slightly different way to check on your installed version is `uname -a`. Note that `/proc/version` will show the actual distribution name, whereas `uname -a` will show if you have a 32- or 64-bit processor.

> **Note**
> The `cat` command is short for “concatenate,” which is intended to join two files into one. However, if you only give it one file name, it will “concatenate” it onto the screen so you can read the contents.

One of the benefits of the Linux kernel and `/proc` filesystem is the ability to make adjustments while the system is *running*. All the settings in the `/proc/sys` subdirectory tree can be adjusted. While you can adjust them just as though there were files, the *sysctl* command provides an easier interface. Changes made within the `/proc/sys` virtual file structure are lost when the system reboots, though. To make them permanent, add them to the `/etc/sysctl.conf` file, which gets loaded each time Linux starts up. Use `sysctl -p` to get the system to re-read the sysctl.conf file without having to reboot.

A common example of using this mechanism is to enable packet forwarding. This turns a Linux PC with two (or more) interfaces into a router, allowing it to pass traffic between two networks. The virtual file is