Now that you have installed Linux on your Power Mac, you may want to perform some additional configuration, adjust settings, and begin exploring the Linux operating system. This chapter provides some additional tips and hints on modifying various settings and configuring your hardware.

Linux works well on nearly any hardware platform and CPU. Your job as system administrator is to get Linux working with all your system's hardware. For many users, just getting Linux installed is enough. Savvy Linux users will want to enable all their available hardware.

The biggest hurdles in installing and configuring Linux are:

+   - Partitioning the hard drive.
+   - Booting to the install.
+   - Navigating through the install.
+   - Configuring X11 for your computer's graphics card.
+   - Configuring Linux sound to work with your system's sound card.
+   - Configuring your modem and getting connected to the Internet.
+   - Setting up Linux to work with your printer.
+   - Getting Linux to work with other hardware devices, such as a scanner.

You have probably already accomplished at least three or four of these tasks!

# Taking Your First Steps with Linux

If you are the only person using your computer, then there are at least two users on your system: you, as a normal user; and the root operator, or system administrator. It is up to you to take care of your system, monitor its health, install new software, and configure new hardware.

# What Is root?

The root operator has a different home directory than normal users. Most users' directories reside under /home in a directory with the user's login name. For example, Fred Smith will usually be the user named “fsmith,” and will have a home directory of /home/fsmith. On the other hand, the root operator has a home directory of /root.

Linux is organized into a simple set of directories. A typical system will look like this:

```
/
├─ bin
```