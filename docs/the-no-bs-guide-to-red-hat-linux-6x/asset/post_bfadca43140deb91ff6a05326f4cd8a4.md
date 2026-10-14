
Okay, pop a DOS disk in the machine and let's try some examples.
Here we see the mdir command in action, listing the files on a disk:

```
mdir A:

Volume in drive A has no label

Volume Serial Number is 1205-1049

Directory of A:\

COMMAND COM      54,645 05-31-94  6:22a
FORMAT  COM      22,974 05-31-94  6:22a
SYS     COM      9,432 05-31-94  6:22a
MOUSE   COM      28,949 04-02-93  4:39p
EDIT    COM        413 05-31-94  6:22a
FDISK   EXE      29,336 01-01-97 12:39a

              6 file(s)          145,749 bytes

                         1,311,915 bytes free
```

Now let's copy a file from Linux to the disk, and vice versa:

```
mcopy A:pandavu.tgz /tmp
mcopy /tmp/kornmeal.txt A:
```

The mcopy command figures out in which direction to perform the file transfer by looking for the A: in either the source or the target file name. If you have two floppy drives, you can use B: when referring to the second floppy drive.

Here's an example showing the use of the mdel command to delete a file on the disk:

```
mdel mouse.com
```

Note that we didn't prefix the name of the file to be deleted with A: this time. All of the MTOOLS commands (except mcopy) assume that you're working with the A drive, so you can omit the A: if you like, but I recommend that you don't, just for safety's sake.

would result from a `dir C:` command under DOS. You can use `cd` to see other directories under `/dos` and use any Linux command to slice and dice your DOS files.

It’s great to have the ability to copy files back and forth between Linux and DOS, but you can also do some clever things if you think creatively. I find it particularly helpful to use the `ln` (link) command to share my Netscape bookmarks file between Linux and DOS, like this:

```
`ln -s /dos/netscape/bookmark.htm $HOME/.netscape/bookmarks`
```

By linking these files together, I need to manage just one bookmark file. Of course, this trick works only if both the DOS and Linux versions of a product use the same format for the files being shared.

If you want your DOS partition to mount each time you boot Linux, add the line shown here to the `/etc/fstab` file:

```
`/dev/hda1  /dos  msdos  umask=022`
```

When Linux boots up, it looks in the `/etc/fstab` file and mounts all the file systems specified there, so you won’t have to issue the mount command manually to access your DOS partition. The line you just added to `/etc/fstab` has the same effect as the mount command shown earlier. The same caveat about FAT32 file systems applies here, so you may need to replace `msdos` with `vfat` in the previous example.

## RUNNING DOS PROGRAMS WITH DOSEMU

DOSemu (DOS Emulator) is a program that lets you run many of your favorite DOS applications under Linux. The name is a little bit misleading—it doesn’t actually emulate DOS; it boots DOS to a virtual machine using the special hardware features in Intel 80386 and higher CPUs.

A DOSemu session looks and acts like a real DOS session, with a few limitations on what can be done. Not all video and sound cards are supported under DOSemu, and some programs that require DPMI (DOS Protected-Mode Interface) will not run. The most notable example of this is Windows 3.1, although some people do report being able to run it under DOSemu.

## SETTING UP DOSEMU

Setting up DOSemu is not hard, but it does require a few steps to get a fully functional DOS session. Unfortunately, the DOSemu package is not present on the CD in this book, so you’ll have to download it from the DOSemu Web site—http://www.dosemu.org/. I recommend that you get the latest stable version (v0.98 at press time) and stay away from the developer versions, since they tend to be buggy.

After downloading the RPM file for DOSemu, issue a command like the one below while logged in as root. The filename may be slightly different, depending on the version you download. (See Chapter 14, “Updating Your Linux System,” for more about the rpm command.

```
rpm -i dosemu-0.98.6-1.i386.rpm
```

Install DOSemu v0.98

## CONFIGURING DOSEMU

The package is now installed, but we need to tweak the DOSemu configuration file before using it. Edit the /etc/dosemu.conf file and modify the $_hdimage entry so that it reads as follows:

```
$_hdimage = "hdimage.test /dev/hda1"
```

The hdimage.test file resides in your /var/lib/dosemu directory and is a hard disk image—a special Linux file that contains a complete DOS system. The line you just modified tells DOSemu to treat the hdimage.test file as the C drive when DOSemu is started. This C drive is not your beloved DOS partition; it’s a simulated bootable hard-disk partition containing the FreeDOS operating system – a freeware clone of MS-DOS. The /dev/hda1 portion of the modified line tells DOSemu to treat your real DOS partition as the next drive letter, or the D drive. (You can boot DOSemu directly from your real DOS partition, but we’ll address that later.)

## STARTING A DOSEMU SESSION

Before starting a DOSemu session, which will be accessing /dev/hda1 (your MS-DOS partition), it’s very important to unmount the partition.
