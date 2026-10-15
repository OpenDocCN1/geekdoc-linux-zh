
## GETTING INFORMATION ABOUT THE SYSTEM
7

Now is your chance to nose around in everyone else's business! In this chapter, we'll show you how to get information about the system, about other users, and about your own userid.

## Chapter Contents

- Finding out system information
- Viewing file systems
- Determining disk usage
- Finding out file types
- Finding out about other users
- Learning who else is logged in
- Getting information about your userid

## Getting System Information with uname

Information about your Unix system might come in handy if you're planning to try some new software or need to figure out system idiosyncrasies. Some systems tell you this information when you log in. Sometimes, however, especially if you're using an ISP, you may not have been told any particulars about the Unix system. You can easily find out what kind of Unix system you're using with uname, as shown in Code Listings 7.1 and 7.2.

### To find out about the system using uname:

- 1. uname

To begin, type uname to find out what kind of a system you're on. The Unix system in Code Listings 7.1 and 7.2 is Solaris (aka, SunOS). Other common systems (not an exhaustive list, by any means) are Linux, AIX, BSD, and HP/UX.

- 2. uname -sr

Add the -sr flags to the command, yielding uname -sr, to find out both the operating system type and the release level. This is useful to find out whether specific software is compatible with the operating system.

- 3. uname -a

For the whole nine yards, use uname -a to print all information, including the operating system type, host name, version, and hardware. The specifics you get here will vary a bit from system to system.

```
ejroy@home $ ssh frizzy

Last login: Wed Oct 10 09:59:09 from frozz
Sun Microsystems Inc. SunOS 5.9 Generic
+ May 2002

ejroy@frizzy $ uname
SunOS
ejroy@frizzy $ uname -sr
SunOS 5.9
ejroy@frizzy $ uname -a
SunOS Frizzy 5.9 Generic_112233-01 sun4u sparc
+ SUNW,Ultra-5_10
```

Code Listing 7.1 Variants on the uname command provide all kinds of interesting or useful information about the system.

```
ejroy@frizzy $ uname
Linux
ejroy@frizzy $ uname -sr
Linux 2.4.19-16mdk
ejroy@frizzy $ uname -a
Linux frazz. raycomm.com 2.4.19-16mdk #1 Fri
Sep 20 18:15:05 CEST 2002 i686 unknown
* unknown GNU/Linux
ejroy@frizzy $
```

Code Listing 7.2 On a different system, the same commands provide slightly different details, although the basic information remains the same.

## Viewing File Systems
with df

If you're used to Windows or Macintosh (prior to OS X) operating systems, you're probably accustomed to having separate hard drives (C:, D:, E:, for Windows users, or real names for Macs), which are just different storage spaces. In Unix systems, different storage spaces are grafted onto the overall tree structure—tacked onto what already exists without any clear distinction indicating where actual disk drives are located. For example, if you have a folder on a Windows computer, you know that all of the subfolders and files within it are located on the same hard drive. In Unix, everything resides within the root directory, but any different directory could be located on a different physical hard drive. You might think of it as tacking a new branch onto your artificial Christmas tree.

These tacked-on storage spaces are called file systems. Particularly if you're running a Unix system (as opposed to just using one), you might need to find out what file systems are in use (or mounted in the system, in technical terms), how much space they have, and where they attach to the Unix system (or where their mountpoints are). You can find out this information using df, as shown in Code Listings 7.3 and 7.4.

If you're a system administrator, you can use this information to help diagnose problems occurring in the system. If you're an average user (of above-average curiosity), you can use this information to satisfy your inquisitive inclinations or to tip off a system administrator to problems. For example, if you're getting odd errors or unpredictable results with a specific program, using df might reveal that the /home file system is full or maybe that you don't have the /dev/cdrom file system that you thought was installed and mounted. Hmmm!

### Tips

- Use df -k /home to make sure that the usage is reported in 1 Kbyte blocks, not in 512 byte blocks. Adding the -k flag will also ensure that you get output like that shown in Code Listing 7.3.

- Use df -h to get "human readable" output. This works with most commands (like ls, for example) that output marginally readable file information.

- You can use df with a specific directory to get a report on the status of the file system containing that directory. For example, you might use df /usr/local/src to find out where that directory is mounted and how much space is available on it.

```
xmision- df
/               (/dev/dsk/c0t0d0s0): 154632 blocks      71721 files
/usr            (/dev/dsk/c0t3d0s0): 225886 blocks      144820 files
/proc           (/proc          ): 0 blocks             7830 files
/dev/fd         (fd             ): 0 blocks             0 files
/var            (/dev/dsk/c0t1d0s0): 1001142 blocks      962598 files
/tmp            (swap           ): 123682             95277 files
/usr/local      (/dev/dsk/c0t1d0s5): 630636 blocks      457211 files
/archive        (/dev/dsk/c0t1d0s3): 1180362 blocks      1789487 files
/var/mail       (mail.xmission.com:/var/mail): 2776576 blocks 143385 files
/home           (krunk1.xmission.com:/home): 20091072 blocks 13066932 files
/.web           (krunk1.xmission.com:/.web): 1019408 blocks 470095 files
/var/mail/lists (lists.xmission.com:/var/mail/lists): 293744 blocks 89732s
xmision-
```

Code Listing 7.4 This large ISP's file systems are considerably more complex.
