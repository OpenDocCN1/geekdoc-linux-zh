# GNU GRUB version 1.99-21ubuntu3

```
Ubuntu, with Linux 3.2.0-24-generic-pae
Ubuntu, with Linux 3.2.0-24-generic-pae (recovery mode)
Previous Linux versions
Memory test (memtest86+)
Memory test (memtest86+), serial console 115200
Windows F (loader) (on /dev/sda2)
```

Use the F and keys to select which entry is highlighted.
Press enter to boot the selected OS, 'e' to edit the commands
before booting or 'c' for a command-line.

Figure 22-5: The GRUB boot menu

# Reinstall Ubuntu

It pains me to say it, but if you just can't fix the problem no matter what
try, it might be better reinstalling Ubuntu. To do this, follow the instructions
in Chapter 2. You might need some of the advice on manual partitioning
from Appendix C too.

Before reinstall, remember to back up any files that you want to keep.
You can do this by copying them to an external hard disk or USB memory
stick while you're running the live CD—all you need to do is access the files
is mount your hard disk as described in "Project 19A: Accessing Files on
Windows Partition (for Dual-Booters)" on page 322 (but mount your Ubuntu
partition than your Windows one).

# Windows Won't Boot

If you installed Ubuntu in a dual-boot setup, you may find that the computer
starts or displays an error message when you try to boot Windows instead of
Ubuntu. Dual-boot Windows setups sometimes have a problem with hiberna-
tion and disk checking, try the following steps to see whether you can get
it working again:

+   1. Boot into Ubuntu and mount your Windows partition (see Chapter 19
for details on how to do this).
2. Find hiberfil.sys (it should be in the top-level folder of your Windows par-
tition, as shown in Figure 22-6) and rename it something like old_hiberfil.sys.
This will cause Windows to ignore all of the hibernation it
has stored.