# Chapter 4: Trying Out Linux

# In This Chapter

+   - Starting Linux
+   - Logging in
+   - Checking out the GUI desktops
+   - Playing with the shell
+   - Shutting down

![](bbox=[0.1, 0.49, 0.2, 0.58])

You're sitting in front of your PC about to turn it on. You know that the PC has Linux installed. (Maybe you did the installing yourself, but who's keeping track?) You're wondering what to expect when you turn it on and what you do afterward. Not to worry. If you're using Linux for the first time, this chapter shows you how to log in, check out the graphical desktops, try out some cryptic Linux commands, and, finally, shut down the PC.

If you try out the Knoppix Live CD, all you have to do is boot from the Knoppix Live CD (as explained in Book I, Chapter 2), and you can try it just like any other Linux distribution.

For those of you who already know something about Linux, flip through this chapter to see if anything looks new. You never know what you may not know!

# Starting Linux

When you power up the PC, it goes through the normal power-up sequence and loads the boot loader — GRUB or LILO, depending on your Linux distribution and what you select during installation. The boot loader (once known as the bootstrap loader) is a tiny computer program that loads the rest of the operating system from the hard drive into the computer's memory. The whole process of starting up a computer is called booting.

![](bbox=[0.1, 0.84, 0.2, 0.92])

For Live CDs (such as Knoppix) that boot from a CD, the boot loader is typically ISOLINUX, a boot loader designed to work from an ISO 9660 CD-ROM.

The LILO and GRUB boot loaders display a graphical screen with the names of the operating systems that the boot loader can load. For example, if your