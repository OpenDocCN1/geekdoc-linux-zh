# Chapter 4: Trying Out Fedora Core

# In This Chapter

+   * Booting Fedora Core
+   * Logging in
+   * Checking out the GUI desktops
+   * Playing with the shell
+   * Shutting down

ou’re sitting in front of your PC about to turn it on. You know that the PC has Fedora Core installed (maybe you did the installing yourself, but who’s keeping track?). You’re wondering what to expect when you turn it on and what to do afterward. Not to worry. If you’re using Fedora Core for the first time, this chapter shows you how to log in, check out the graphical desktops, try out some cryptic Linux commands, and finally, shut down the PC.

Those of you who already know something about Fedora Core, flip through the pages to see if anything here looks new. You never know what you may not know!

# Booting Fedora Core

When you power up the PC, it goes through the normal power-up sequence and loads the boot loader — GRUB or LILo, depending on which one you selected during Fedora Core installation. The boot loader (once known as bootstrap loader) is a tiny computer program that loads the rest of the operating system from disk into the computer’s memory. The whole process of starting up a computer is called booting.

Whether the boot loader is LILo or GRUB doesn’t matter much. In either case, a graphical screen appears with the names of operating systems that the boot loader can load. For example, if your PC has Windows and Fedora Core, you see both names listed. You can then use the Up and Down arrow keys to select the operating system you want to use. If the PC is set up to load Fedora Core by default, wait a few seconds and then the boot loader starts Fedora Core. To be more precise, the boot loader loads the Linux kernel — the core of the Linux operating system — into the PC’s memory.