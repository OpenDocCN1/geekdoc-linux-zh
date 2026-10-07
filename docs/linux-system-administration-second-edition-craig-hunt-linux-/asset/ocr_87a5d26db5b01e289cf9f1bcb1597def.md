```
rootnoverify(hd0,0)
chainloader +1
```

# Can't Remove Boot Loader from the Master Boot Record

It's possible that you'll install Linux on a computer and then discover that you need to recycle the computer for use with Windows, DOS, or some other OS. Many new Linux administrators have problems with this, though, because after they've removed Linux, the boot loader hangs on like an albatross around the computer's neck. Fortunately, there are ways to deal with this problem. If your system still has Linux installed using LILO and you want to remove LILO from the MBR, you log in as root and use the LILO uninstall command as follows:

```
# lilo -u
```

If you use GRUB or have for some reason deleted Linux from your system and installed some version of Microsoft Windows, you can use the Windows FDISK command to rewrite the Master Boot Record and then reboot:

```
C:\> FDISK /MBR
```

# Kernel Won't Load or Loads Only Partially

There are two possibilities here. Either the kernel image has become corrupted in some way or LILO is being passed an incorrect parameter. You see this if someone adds an incorrect append line in /etc/lilo.conf.

Often this is an incorrect mem line. The mem option isn't usually needed but occasionally you'll run across a system for which LILO doesn't recognize the correct amount of memory. If you need to help LILO recognize a large amount of memory, such as 256MB, add the line mem=256M to the /etc/lilo.conf file and then run lilo. If you incorrectly add mem=2256M or some other too—large number, your kernel will not fully load. If you incorrectly add mem=256m using the lowercase m, that will also inhibit the kernel's ability to fully load.

When LILO is run, it catches some of the errors in the /etc/lilo.conf file. If you specify a kernel image that doesn't exist, the lilo program will generate an error message. If you've specified a boot device that doesn't exist, you will see a message like this:

```
Fatal: open /dev/hdb: Device not configured
```

# Login Problems

Because gaining access to your systems is so important, you must be able to diagnose and repair login problems. Knowing the login process step by step is the key to this ability. Once you've been doing Linux system administration for a while, these problems will be easy for you to fix.

# Lost Password

One of the most frustrating problems occurs when you have a system and no one seems to remember the root password. With luck this won't happen often. Sometimes, though, the root password is needed and not known and needs to be reset.

461