
You can use Netscape Communicator to read the newsgroups. For a newsgroup, use a URL of the form `news://newsserver/newsgroup` in which `newsserver` is the fully qualified domain name (FQDN) of your news server (your Internet Service Provider should give you this name) and `newsgroup` is the name of the newsgroup you want to read. For example, assuming that your news server is `news.mysp.net`, you can browse the `comp.os.linux.setup` newsgroup by typing the following URL in the Location field of the Netscape Web browser:

`news://news.mysp.net/comp.os.linux.setup`

## FTP archive sites

You can download Red Hat Linux and other Linux distributions from one of several FTP sites around the world. In addition to the Linux distribution itself, these sites also contain many other software packages that can run under Linux.

For the latest list of Red Hat Linux FTP sites worldwide, visit the Web page maintained by Red Hat at `http://www.redhat.com/mirrors.html`. This page displays a table of URLs of sites that maintain the Red Hat distribution for downloading. In that table, the **Updates** column lists the URLs for downloading specific Red Hat Package Manager (RPM) files for the latest Red Hat Linux version (for Intel-based PCs).

Red Hat provides many fixes and improvements as updates in the form of Red Hat Packages distributed from Red Hat's FTP server. Try `ftp://ftp.redhat.com/pub/redhat/updates`; if it's busy, consult `http://www.redhat.com/mirrors.html` for a mirror site near you. To install these packages, you have to use the Red Hat Package Manager (RPM).

See Session 20 to learn how to use the Red Hat Network to keep your Red Hat Linux system current with the latest updates and security patches.

![](img/5fe8f856723cde0b366f73584b9e64b8_331_0.png)

## Magazines

*Linux Journal* is a monthly magazine devoted entirely to Linux. On the Web, the magazine home page is at `http://www.linuxjournal.com`. There, you can find information on how to subscribe to this magazine.

*Linux Magazine* is another monthly magazine that covers everything Linux. Visit their home page at `http://www.linux-mag.com/` to learn more about *Linux Magazine* and to subscribe to it.

## REVIEW

This session showed you how to get help on various aspects of Red Hat Linux. You learned how to use the GNOME Help Browser and also how to use several helpful commands such as `man`, `whatis`, and `apropos`. Finally, you familiarized yourself with a number of Internet-based Linux resources from Web pages, to FTP archives, to two popular Linux magazines.

![](img/5fe8f856723cde0b366f73584b9e64b8_331_1.png)

Session 30—Getting Help from Available Resources

311

## QUIZ YOURSELF

- What types of help information can you view with the GNOME Help Browser? (See “Using the Help Viewers.”)
- What is `man` and what can you do with it? (See “Using the Help Viewers.”)
- How can you view a brief description of a command? (See “Using the Linux Commands to Get Help.”)
- How do you access the HOWTO files? (See “Looking Up Online HOWTO Files.”)
- What are some of the Linux newsgroups? (See “Internet newsgroups.”)

# PART VI

## Sunday Afternoon

1. Why should you learn how to build software from source code?
2. What is the most common format for source code distributed on the Internet? How do you download and unpack it?
3. After downloading a source code package from the Internet, what should you do next?
4. Briefly outline the steps to take, without giving specific command lines, to unpack, configure, build, and install a typical source code package.
5. What is the XMMS package? How would you build and install it after downloading and unpacking it?
6. Name some of the factors to which you should pay attention when monitoring your system's performance.
7. Name two tools that you can use to monitor system performance.
8. Give a short definition of "system load average."
9. Show the `vmstat` command line that displays its output 10 times in 60-second intervals.
10. What is the purpose of the `/proc` file system?
11. What is the purpose of a security policy and what are some of the areas that a security policy should address?
12. Briefly describe the procedure for securing your system.
13. Identify two ways Red Hat Linux helps you make your system more secure.
14. What command line forces the user named `marys` to change her password every 30 days?
15. What is `xinetd` and what purpose does it serve?
16. What package makes `xinetd` more secure?
17. Name the help-system viewers for the GNOME and KDE desktops and explain how to start them.
18. How do you view a one-line description of what the `tr` command does? How would you view the complete online help for the `tr` command?
19. What command can you use to search for commands that match a keyword?
20. What are HOWTO files and how can you access them from the GNOME desktop?

![](img/5fe8f856723cde0b366f73584b9e64b8_336_0.png)

# APPENDIX A

## Answers to Part Reviews

This appendix contains the answers to the part review questions at the end of each part in this Weekend Crash Course. Think of these reviews as mini-tests that are designed to help you prepare for the final — the Skills Assessment Test on the CD.

### Friday Evening Review Answers

1. It is important to review the Red Hat Linux compatibility lists in order to make sure that your PC’s hardware will work with it. At a bare minimum, you must have a Linux-compatible CPU, bus type, disk drive, video adapter, monitor, keyboard, mouse, and CD-ROM drive to install Red Hat Linux from the companion CD-ROMs. If you want to run the X Window System and graphical desktops such as GNOME or KDE, you also must ensure that XFree86 (the X Window System for Linux) supports the mouse, the video card, and the monitor.

2. It is not necessary to create a Red Hat boot floppy if your system is capable of booting from a CD-ROM because the installation CD-ROM has a bootable file system on it.

3. Usually a PC’s hard disk has a single partition that is used by Windows 95/98. If you decide to keep Windows on your PC, you have to repartition the hard disk to create room for the Linux file system. It’s possible to repartition in two ways: by backing up everything and destructively repartitioning the disk with the `FDISK` command or by using the `FIPS` program to non-destructively create room for a new partition. You probably want to use the `FIPS` program because it is easier than destructive repartitioning. You could also use tools such as PartitionMagic to create a new partition non-destructively for Linux.

4. The Linux `fdisk` utility is a text-mode disk partitioning utility that enables you to partition or repartition your hard disk during and after the Red Hat Linux installation program.

5. Linux uses the swap partition, or space, as virtual memory where disk storage is used as an extension of physical memory (RAM). When the Linux kernel runs out of physical memory to run a program, it can move (or swap out) the contents of currently unneeded parts of RAM to make room for a program that needs more memory. As soon as the time comes to access anything in the swapped-out data, the Linux kernel has to find something else to swap out and then it swaps in the required data from disk into physical memory. You should set aside at least twice the amount of RAM in your PC, if possible.

6. You can add one or more normal users during Red Hat Linux installation. To add a user account, enter the user information in the **Account Configuration** screen and click the **Add** button to add the user.

7. A *package group* is a collection of several Red Hat packages. You can select individual packages from a package group by selecting the item labeled **Select individual packages**, that appears below the list of package groups in the **Package Group Selection** screen.

8. The Red Hat Linux installation program supports NFS installations and a Kickstart installation. NFS installation is ideal for allowing machines on a network to install Red Hat Linux without needing the CD-ROMs. The Kickstart installation makes it easy to install the same configuration on multiple machines without needing to intervene or monitor the installation.

9. The X Window configuration tool described in Session 2 is named **Xconfigtool**.

10. A monitor's vertical and horizontal refresh rates, or *synchronization frequencies*, are important because they define the maximum performance capabilities of the monitor. The *horizontal refresh rate* is the number of times per second that the monitor can display a horizontal raster line, usually expressed in kilohertz (kHz). The *vertical refresh rate* specifies how many times a second the monitor can display the entire screen. You can find the value of these parameters in your monitor's manual.

11. You could type `dmesg | grep par` and look for any indication of parallel port information in the output.

12. Installation help is available in *The Official Red Hat Linux x86 Installation Guide*, *The Official Red Hat Linux Getting Started Guide*, the x86 Knowledge Base (<http://www.redhat.com/apps/support/>), and the Red Hat mailing list archives (<http://www.redhat.com/apps/support/updates.html>).

13. X Window handles the mechanics of drawing windows and communicating between an X client and the X server or another X client. It does nothing to decorate a window with pretty title bars, scrollbars, interpret mouse movement, keystrokes, and the like. However, X Window does provide a *protocol*, the rules or the general framework, that window managers must follow. *Window manager* creates title bars, scrollbars, menus, and so on, on the unadorned windows that X creates.

14. To log out of a GNOME session, select **Main Menu** > **System** > **Log Out**. To log out of a KDE session, select **K** > **Log Out** and then click the **Log Out** button in the resulting dialog box.

15. If you forget the root password, reboot the system and then, at the **LILo** boot: prompt, type `1` then `s` `n` `l` and press **Enter**. Then, at the `#` prompt, type `passwd root`, and follow the prompts to reset root's password. Finally, type `shutdown -r now` and the system will reboot and recognize the new password.

16. The applet that switches your desktop from GNOME to KDE and back is called **Desktop Switcher** or `switchdesks`.

17. To undo a change in the GNOME Control Center, click the **Revert** or **Cancel** button.
