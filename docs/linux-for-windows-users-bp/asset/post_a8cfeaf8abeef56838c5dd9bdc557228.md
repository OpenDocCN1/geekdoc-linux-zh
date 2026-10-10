
Everything is case sensitive. “You must be careful to do things not just ‘to the letter’, but ‘to the case’. If you get it right, this command will run the name of the file that is providing the shell. It provides the name of the file and the subdirectory (folder) in which it is located. This should produce a result something like this:

```
/bin/bash
```

As pointed out previously, Linux uses the forward slash character rather than the backslash to indicate changes from one subdirectory to another. “Remember that to specify from one subdirectory to another, the slash is used to say ‘from here’, and it is you that provides the shell the correct ‘where from’.”

The shell is called “bash”, and the top-level directory called “bin”. If the shell you are running is not bash, typing this command should run the bash shell:

```
bash
```

Again, make sure that you use letters of the correct case when typing this command. Once into the shell, the command line prompt you see will depend on whether you have logged in as the supervisor (i.e. logged in as “root”) or as a normal user. It also depends on the name of the system. On one of my systems, it is obtained when I login as “root”:

```
[root@robert /]#
```

Logging in as an ordinary user called (say) fred would give the following prompt:

```
[fred@robert /fred]$
```

In addition to the change in name, note that the hash (#) sign has been replaced by a dollar ($) character. The hash sign is displayed only for the system supervisor, and indicates that the user can make changes to the system settings. It is effectively a warning that you have to be careful what you do, as you have access to files that govern the way the system operates. Careless use of these files could prevent the system from operating properly.

The first part of the prompt is simply the name of the user and the system. The second section indicates the current position in the file system. MS DOS was set up in a similar fashion, and the prompt you see currently on the subdirectory called “DOS”, on drive C, the prompt would look something like this:

```
C:\DOS>
```

## Roots

For those who have been using Windows and MS-DOS for years, the Linux file system can take a little time getting used to. In Windows and MS-DOS, things tend to be rather more compartmentalised, with each user having his or her own directory, drive, or examine its directory structure, but any one into a particular disc can only be examined by changing over to that drive. With MS-DOS, you can copy a file from a disc drive to a port, but the ports are again separate entities and not part of the file structure.

Ties things together. The recent versions of Windows, with “My Computer” representing the “overall system”, icon on the Windows desktop is also an attempt to unify things with the Linux file system.

With separate parts of the file structure, it is truly unified with everything based on the top. Do not confront this root directory actually called “/”, which is a subdirectory of the root (“/” is always followed by the name in square brackets, and the directory called “root” will have the name in quotation marks.

In Linux, the root directory is truly that and everything else grows out of this. Separate thoughts, as in example directory system, 2.1. Most of these directories are present on an example from which the Linux system is installed. Some of them can actually have other drives or places or hardware thoughts. In the floppy disc structure. In fact, they usually appear in other places. Normally in the file structure. The files in the /dev directory are devices in the file system. The /dev directory into the system. If you want to make it impossible to use the floppy or CD-ROM drive, leave this directory alone, and do not experiment with the files it contains. The /mnt directory is where the floppy will be mounted by the system when you are using the floppy drive. Linux terminology: Items of hardware such as modems and the printer are all merged into the file system.

## Mounting

Initially, the CD-ROM and floppy drives will not be mounted, and this is an area where MS-DOS and floppy work in a much more free and easy manner than Linux. With Windows, and MS-DOS, you can mount or unmount discs as and when you please. The system may occasionally complain with an error message when it fails to find the expected disc in the drive, but in general, there is unrestricted access to the drives. Linux has not actually made the drive part of the system a logical mount since it is not actually necessary to contain any files. The commands used to mount drives are easy to remember; since it is called mount, it is not mounted until you type it. Before you can use a drive, it must be mounted, and disc drives do not actually have to contain any files. The command used to mount a disc has to be typed at /mnt/floppy or /mnt/cdrom. On the system I am using for these examples, the floppy drive is mounted at /mnt/floppy. If you type the `mount` command, you will list all the mounts in the system. The equivalent of the “dir” command in Linux is the “ls” command. Type this instruction to view more /etc/fstab file which lists the mounts:

There should be a couple of lines in the file that are similar to these two:

| Device | Mount Point | Options |
| :--- | :--- | :--- |
| /dev/hda | /mnt/floppy | auto,user,iso9660,ro,defaults,noauto |
| /dev/hdd | /mnt/cdrom | auto,user,iso9660,ro,defaults,noauto |

The first line is the one for the floppy drive and the first two entries on this line show where the floppy device appears in the file system. Either of these can be used when mounting the drive, so either of these will do the job:

```
mount /mnt/floppy
mount /dev/fd0
```

Things operate in a similar manner for the CD-ROM drive, and the first two entries in its section show where it appears in the file system. To mount the CD-ROM drive either of these commands could be used:

```
mount /mnt/cdrom
mount /dev/hdd
```

![](img/147f057d2f063d8c60ee616870537a94_30_0.png)

## Unmounting

Once a floppy drive or CD-ROM drive has been mounted, you should use the correct Linux term, or unmount, to “dismount” the media until it has been dismounted. In the case of the CD-ROM drive, it is unlikely that the eject button on the drive will be operational until the drive has been unmounted. The unmount command follows the same format as the mount command, but the command word unmount (not umount) is used instead of mount. These two commands would therefore unmount the floppy and CD-ROM drives:

```
umount /dev/fd0
umount /mnt/cdrom
```

Note that you cannot unmount a drive if you are actually in that directory at the time, as it is being used in any way by the system. Trying to do so will simply produce an error message indicating that the device is busy.

## Navigating

Navigating your way around the file system by way of the command line interpreter is never going to be as easy as using a desktop system such as KDE. However, it is probably better to experiment with a program such as KDE only after you have become familiar with the basics of moving around the file system via the command line interpreter, and navigating the directories by their alternate structure. Apart from some convenience of the graphical interface such as drag-and-drop of files between two or more directories, the basic commands that you need to use are all in the system's `pwd` (man 8) command.

You can use `pwd` to move from one directory to another. The `cd` (change directory) command is used. If you try this command, it should respond with details of the current directory:

```
pwd
```

To move from one directory to another, the `cd` (change directory) command is used, and this is similar to the MSDOS command of the same name. This command will move from the current directory, regardless of which directory it is, to the /usr directory:

```
cd /usr
```

It is not necessary to give the full path to the new directory; it is sufficient to tell one that the system is currently in, for example, in the /usr directory, and you what you want to move to the /usr/lib directory, so we would write `cd lib`.

The desired effect:

```
cd /root/Desktop
cd Desktop
```

In /msdos, “.” can be used as an abbreviation for the current directory, and “..” can be used as an abbreviation for its parent directory. This command can therefore move one directory higher:

```
cd ..
```

For example, if the system was in /root/Desktop when this command was used, it would be in /root afterwards.

## Listing

In MSDOS, the `dir` (directory) command is used to list the contents of a directory, and the same command also works with Linux. There is an alternative available in Linux in the form of `ls`, the list command, which seems to be the preferred command for obtaining directory information. Either of these commands will list the contents of the current directory:

```
ls
dir
```

The system does not have to be in a directory in order to list its contents. This example will list the contents of the /usr directory regardless of which directory the system happens to be in at the time:

```
ls /usr
```

## Colour

There is a slight problem with the basic `ls` command in that the information displayed on the screen is rather ambiguous. There is no way of distinguishing between files and subdirectories. But with the Linux version of `ls`, it is possible to get around this by using the color option, as in this example:

```
ls --color
```

Note that the word “color” must be spelled the American way, and that using “colour” instead will not work. If you try this on a directory containing a good selection of files, the result should be a colourful display using a different color for each file type. This list shows the colors used for several common file types.
