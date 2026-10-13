This will copy your new kernel and system.map to the boot directory, /boot, with the version and all the correct names, and it will change the respective links. It will also back up your old files with a .old extension and run lilo to fix it for your new kernel. If you want to, you can use linuxconf later to set up lilo to boot either the new or the old kernel when you choose, if that is desired.

That's it! You're finished! Well, almost... Pour yourself a stiff drink, assume a praying-like posture in front of your computer, and reboot. You will be enjoying the fruits of your labors, with the new kernel working just as you envisioned and everything running perfectly, in minutes. Anyway, if it doesn't work, you still have the old kernel that you can boot back into and try it again.

# Summary

During the past hour, you followed the long and involved process of upgrading the Linux kernel. Remember that it isn't always necessary to upgrade every piece of software, utility, command, kernel, library, and programming language every time a new version comes out. Think before you upgrade. Will the upgrade be beneficial to you and your system? If you don't see the added value, don't do it. But, if you need the new kernel to support the fancy new piece of hardware that you just purchased, carefully read this chapter again and read the other sources of information listed in this hour so that you are well prepared.

# Q&A

Q Is there an easier way to upgrade my system? This kernel stuff is more than I can deal with and I'm afraid of wrecking my system.
A You might want to wait until the next version of your favorite Linux distribution comes out. When you install the new version, you can select the Upgrade option when the installation starts. Not only will the kernel be updated, but all your favorite applications will be upgraded as well.

Q How do I find out which version of the Linux kernel is installed on my system?
A That's an easy one! Just type `uname -a` and press Enter at the command line. Not only will you see the kernel version, but you'll also see the hostname of the computer, the number of times the kernel has been compiled, the date on which the kernel was compiled, and the model of the computer's processor.