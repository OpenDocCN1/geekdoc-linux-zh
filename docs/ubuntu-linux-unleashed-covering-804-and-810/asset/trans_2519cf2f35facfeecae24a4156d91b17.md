

![](img/8f9e74e2b343ff525bebfb720a3d8441_52_0.png)

FIGURE 1.15 The auto-start menu gives you a gateway to Ubuntu. Click Install inside Windows to start the Wubi installation.

![](img/8f9e74e2b343ff525bebfb720a3d8441_52_1.png)

FIGURE 1.16 You can select some configuration options before you start the installation.

actually been modified, but a rather large file has been created to hold Ubuntu. When you restart your system you'll see the Ubuntu option, so press the down-arrow key and press Enter to begin booting into your new Ubuntu system.

The first time you start up a Wubi Ubuntu installation, it does some post-installation configuration before loading the GNOME desktop. You now have a fully functional Ubuntu system.

If you decide that you want to do a proper installation then you'll need to remove Ubuntu and Wubi. Fortunately, as part of the Wubi installation, an entry is added to the Add/Remove Programs tool in Windows allowing you to quickly and easily remove Wubi and the associated Ubuntu installation. Just remember to back up any files that you want to keep!

## Shutting Down

At some point, you are going to want to shut your computer down. As with most things in Linux, there are different ways to do it. You can use the Quit icon located in the upper-right corner of your screen or use the same button located in the System menu. Either way, you can choose to shut down or restart your system. You can also choose to hibernate (saves a copy of the running state to disk and shutdowns) or suspend (saves the current running state to memory). We would recommend using either shutdown or reboot to ensure you get a clean system when it comes back up.

If you are working at the command line, you can immediately shut down your system by using the shutdown command like this:

```
```bash
$ sudo shutdown -h now
```
```

You can also use the shutdown command to restart your computer, as follows:

```
```bash
$ sudo shutdown -r now
```
```

For new users, installing Ubuntu is just the beginning of a new and highly rewarding journey on the path to learning Linux. For Ubuntu system administrators, the task ahead is to fine-tune the installation and to customize the server or user environment.

## Reference

- http://www.ubuntu.com—The place to start when looking for news, information, and documentation about installing, configuring, and using Ubuntu.
- http://tinyurl.com/c2x5u—Symantec’s PartitionMagic utility includes BootMagic, which can be used to support booting of Linux or, regrettably, other less-capable operating systems, such as Windows XP.
- http://www.v-com.com/product/System_Commander_Home.html—V Communications, Inc.’s System Commander, a commercial 4.2MB download that can be used to support booting of any operating system capable of running on today’s PCs. An intelligent partitioning utility, Partition Commander, is included.
- http://www.nwc.com/columnists/1101colron.html—How to use Intel’s Pre-execution Environment (PXE) protocol to remote boot workstations.
- http://www.gnu.org/software/grub/—Home page for the GRUB boot loader.
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/BootPrompt-HOWTO.html—The Boot Prompt-HOWTO, a guide to using the boot prompt for passing kernel arguments.
- http://www.tldp.org/HOWTO/Installation-HOWTO/index.html—The Linux Installation-HOWTO, a guide to installing Linux, by Eric S. Raymond.

## CHAPTER 2

## Post-Installation Configuration

Now that the hard bit is out of the way (installing Ubuntu) you can begin to customize your new operating system. By default, Ubuntu presents you with a pretty blank canvas with which to personalize your experience. Some people choose to stick with the default look and feel, while others go for a full make over.

In this chapter, we’ll take a look at getting up and running with Ubuntu, including a quick tour around the desktop. We will also take a look at some of the ways in which you can customize your Ubuntu installation, such as ensuring that date and time settings are correct, as well as show you how to do some basic administration tasks, such as identifying any problems with hardware. By the end of this chapter, you should feel comfortable enough to move on through the rest of the book.

### NOTE

Throughout this chapter, we introduce you to several key applications relevant also to other chapters of this book. We include them here because they are essential to getting your system to work as you intend. You will find it worthwhile referring back to this chapter as you work your way through the book.

### IN THIS CHAPTER

- Troubleshooting Post-Installation Configuration Problems
- The sudo Command
- First Update
- Configuring Software Repositories
- Installing Graphics Drivers
- Changing Ubuntu's Look and Feel
- Preferred Behaviors
- Input Devices
- Detecting and Configuring a Modem
- Configuring Power Management in Ubuntu
- Setting the Date and Time
- Configuring and Using CD, DVD, and CD-RW Drives
- Configuring Wireless Networks
- Reference

