
## Tips for Using Your System

The following set of tips help make your everyday experience with Linux easier and more efficient.

## Reading Binary Files

If you have a binary file you want to read, you can use the strings command. This command shows you a list of all the strings inside the binary file. This command comes in very handy for developers. You can use it to see all the strings in a binary file or library. Its general format is as follows:

```
$ strings filename
```

## Viewing All Running Processes

To view all the currently running processes, you can use the ps command. This command lists your own processes by default, but to make it list all processes, type the following:

```
$ ps aux
```

If the listing seems to go beyond the edge of the screen, use the w option to cause the lines to wrap around:

```
$ ps auxw
```

## Recursive grep

You can use the grep command to search for text in a group of files. For example,

```
$ grep linux *.txt
```

searches all files with the .txt extension for the word linux. This will not search subdirectories, however. You should use rgrep if you want to search recursively.

## Easy Downloading

SuSE Linux includes a utility that is considered one of the best downloaders available for Linux, wget. You can use wget to grab whole Web sites or single files. To grab a whole Web site, use the following command:

```
$ wget -r http://www.suse.com/
```

To grab a single file, type the following:

```
$ wget ftp://ftp.somewhere.com/file.tar.gz
```

Give wget a try; you will surely find it very handy and useful.

## Using the Manual Pages

Linux has a set of manual pages that explain most of the commands and programming API available. You can access this manual using the man command. For example, to find the manual page for the ls command, type the following:

```
$ man ls
```

Manual pages are in sections. The following are the available sections:

- Section 1: User Commands
- Section 2: System Calls
- Section 3: Subroutines
- Section 4: Devices
- Section 5: File Formats
- Section 6: Games
- Section 7: Miscellaneous
- Section 8: System Administration
- Section n: Tcl/Tk

To access a section, just type its number after the man command. For example, the following searches section 1 for the command you enter after the 1:

```
$ man 1 command
```

You can use the -k option if you want man to search all the sections for the command you want.

## Changing the Priority of Your Processes

Processes in Linux get CPU time according to their priority. The higher the priority, the more CPU time the process will get. To change the priority of a process, use the nice command. Priorities are a numerical value that ranges from -20-19, with 0 as the default. The lowest priority is 19, whereas the highest priority is -20.

To change the priority of a process, type the following:

```
$ nice 10 pid of process
```

You should note that a normal user cannot change the priority of a process to a number below 0, only root can do that. You can only change the priority of a process you own.

## Viewing Files in Pieces

You can use the head command to view the top 10 lines of a file. You can do the opposite using the tail command, which will show you the last 10 lines in a file. You can use the -f option in tail to cause it to continuously list the last 10 lines of a file as it grows in size.

This is very handy when tracking your log files. For example, enter the following to continuously see the latest log messages:

```
$ tail -f /var/log/messages
```

## Killing Processes

To kill a process, use the kill command. You must know the ID of the process you want to kill; you can use ps to get it. Alternatively, you can use the killall command, which takes the name of the process you want to kill rather than its ID. For example, the following kills all the Netscape processes that belong to you:

```
$ killall netscape
```

Be very careful with this command when you are running as root. You can easily kill other users' processes by mistake!

## X Window System Tips

If you use SuSE Linux as a desktop operating system, you will be using the X Window System quite often. We will discuss several tips to enhance your X Window experience in the following sections.

## Speeding Up Your X Window System

The 2.2.x kernel uses a feature present in Pentium Pro and later processors called Memory Type Range Registers. You must enable them in your kernel configuration, in the Processor Type and Features section.

Using MTRR, you can tell the kernel to enable write combining on a block of memory, which increases the speed of data transfers. This is useful if you have a PCI or AGP display card. You can enable write combining on the card's memory, thus speeding up your graphics. This in turn will speed up your X Window System quite considerably.

To use MTRR, you need to know the beginning of your card's memory address space. You can find this information by looking at the /proc/pci file:

```
# cat /proc/pci
```

The previous command gives you a list of all the PCI devices you have on your system. You are interested only in the part that has to do with your graphics card. The following is an example of such a section:

```
Bus 1, device 0, function 0:
VGA compatible controller: NVidia Unknown device (rev 21).
Vendor id=10de. Device id=2d.
Medium devsel. Fast back-to-back capable.
-IRQ 11. Master Capable. Latency=64. Min Gnt=5.Max Lat=1.
Non-prefetchable 32 bit memory at 0xf5000000 [0xf5000000].
Prefetchable 32 bit memory at 0xfc000000 [0xfc000000].
```

The part you are interested in is the line Prefetchable 32 bit memory at 0xfc00000 [0xfc00000]. In this example, this tells you that our card's memory starts at 0xfc00000.

To tell the kernel to enable write combining on this memory, type the following as root:

```
# echo "base=0xfc00000 size=0x2000000 type=write-combining" >> /proc/mtrr
```

The size field takes the size of the RAM on the card in hex. In the previous example, it's 0x2000000, which is 32MB. You can calculate it on any calculator.

That's it, restart your X Window System to see the difference. You should notice an overall increase in speed, especially if you are using GNOME and have a lot of themes applied.

You should enter the previous line in /sbin/init.d/boot.local if you want it to take effect when you reboot.

## More Acceleration to Your X Window System

If your graphics card and X Server support acceleration, you can turn it on using the Accel option. Just edit /etc/XF86Config and add the following option to the device section:

```
Option "accel"
```

The final section should look something like the following:

```
Section "Screen"
    Driver "svga"
    Device "RIVA TNT2"
    Monitor "DELL"
    Option "accel"
```

You will see the rest of the section, but it's not included because it's not relevant here. Restart your X Window System for the changes to take effect. Please note that this will work only if both the server and the card support acceleration.

## Using the Geometry Option

You can make an application start in a specific spot on your screen using the -geometry option, which tells the application where to position itself on the screen. The option's form is -geometry WxH+X,Y, where W is width, H is height, and X and Y are the coordinates. For example, the following causes xclock to position itself in the top left corner of the screen:

```
$ xclock -geometry 100x100+0+0
```

It will have a height of 100 pixels and width of 100 pixels.

If you replace the plus sign (+) with a hyphen (-) in the X,Y coordinates, it will start from the right side of the screen for the X and the bottom for the Y. For example, the following places xclock in the top right corner of the screen:

```
$ xclock -geometry 100x100-0+0
```

This occurs because the X coordinate -0 indicates 0 pixels from the right of the screen.

## Starting More Than One X Session

More than one instance of the X Window System can run on the same machine. To do this, type the following:

```
$ startx -- :1
```

The new X Window session will start alongside the currently running one. The first one can be accessed by pressing Ctrl+Alt+F7 and the new one by pressing Ctrl+Alt+F8. For example, you can run KDE in one and GNOME in the other.

## Getting the Most Out of a Netscape Crash

If your Netscape hangs on you, the usual solution is to kill it using the killall command:

```
$ killall -9 netscape
```

This, however, will not save your session (bookmarks, preferences, history, and so on). For Netscape to save the session, use the following:

```
$ killall -12 netscape
```

The previous command keeps you from losing any new bookmarks.

## Menus in X Terminals

You can bring up menus that configure your X terminal using the Ctrl key and a mouse button. Each of the three buttons on the mouse will bring up a different menu. Just press Ctrl+Mouse button 1 to see one of them.

## Networking Tips

The following sections discuss a few network-specific tips.

## Listing All Open Connections

If you are wondering who is connected to your machine, wonder no more. You can use the netstat command to list all the open connections to and from your machine. For example, the following shows you a detailed list of all the open connections to and from your machine:

```
$ netstat -na
```

The previous command is very useful for monitoring your network for efficiency and security reasons.
