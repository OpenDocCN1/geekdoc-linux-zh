# Pulling Yourself Up by the Boot

When you're logged in as the root account, you might want to take a few minutes to create a fresh “boot diskette” or copy the diskette you already have. There are a number of reasons you should make a boot diskette: it can help you recover from a system failure, it can help you test a new kernel you've downloaded and compiled and it can help you share your computer with more than one operating system.

+   - Tip: You can always use a copy of the boot diskette to form the first half of a rescue disk set. You'll need a boot diskette and a rescue diskette to enter rescue mode. To read more about rescue mode, see later in this chapter.

You were given the opportunity to make a boot disk when you installed Red Hat Linux. If you chose not to make a boot disk at installation, here's your chance to start from scratch. For now, we'll make boot disks from the shell prompt while we're in an X session. Go to the shell prompt: In GNOME, for example, left-click on the GNOME footprint on the panel, go to Utilities in the menu and click on one of the items marked xterm or on the GNOME terminal item. Now, make sure you're logged in as root. At the shell prompt, if you see something like [billy@localhost billy], for example, type:

```
[billy@localhost billy] su
Password: yourrootpassword
[root@localhost billy]#
```

This will allow you to change from your regular user account to the root account. Please Note: when you're in the root account, you are commander in chief of everything on your system, so be careful.

+   - Tip: The command su means substitute users, which lets you log in temporarily as another user.

Briefly, we'll find the Linux kernel version; then, we'll use the mkbootdisk command to make a bootable floppy from the kernel. Put a standard diskette in the floppy drive.

+   - Tip: In Linux, the floppy drive is referred to as /dev/fd0.