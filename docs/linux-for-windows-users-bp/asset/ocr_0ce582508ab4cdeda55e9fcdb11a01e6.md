Disounting 
Once a floppy drive or CD-ROM drive has been mounted you should use the correct Linum term, or unmount to "dismount" the media until it has been dismounted. In the case of the CD-ROM drive it is unlikely to be the eject button on the drive will be operational until the drive has been unmounted. The unmount command follows the same format as the mount command, but the command word unmount (not umount) is used instead of mount. These two commands would therefore unmount the floppy and CD-ROM drives:


```

unmount /dev/fd0

unmount /mnt/cdrom

```

Note that you can not unmount a drive if you are actually in that drive at the time, as it is being used in any way by the system. Trying to do so will simply produce an error message indicating that the device is busy.

Navigating
Navigating your way around the file system by way of the command line interpleter is never going to be as easy as using a desktop system such as KDE. However, it is probably better to experiment with a program such as KDE only after you have become familiar with the basic of moving around the file system via the command line interpreter, and navigating the directories by their alternate structure. Apart from some convenience of the graphical interface such as drag-and-drop of files between two or more directories, the basic commands that you need to use are all in the system's pwd(man8) command. 
You can use pwd to move from one directory to another. The cd (change directory) command is used. If you try this command it should respond with details of the current directory:

```
pwd
```
To move from one directory to another: the cd (change directory) command is used, and this is similar to the MSDOS command of the same name. This command will move from the current directory, regardless of which directory it is, to the /usr directory:

```
cd /usr
```
It is not necessary to give the full path to the new directory; it is sufficient to tell one that the system is currently in, for example, in the /usr directory, and you what you to move to the /usr/lib directory, so we would write cd lib.

The desired effect:

```
cd /root/Desktop
cd Desktop
cd Desktop
```
in /msdos, / "." can be used as an abbreviation for the current directory, and ". ." can be used as an abbreviation for its parent directory. This command can therefore move one directory higher:

```
cd ..
```
For example, if the system was in /root/Desktop when this command was used, it would be in /root afterwards.

Listing
In MSDOS the dir (directory) command is used to list the contents of a directory, and the same command also works with Linux. There is an alternative available in Linux in the form of ls, the list command, which seems to be the preferred command for obtaining directory information. Either of these commands will list the contents of the current directory:

```
ls
dir
```
The system does not have to be in a directory in order to list its contents. This example will list the contents of the /usr directory regardless of which directory the system happens to be in at the time:

```
ls /usr
```
Colour
There is a slight problem with the basic ls command in that the information displayed on the screen is rather ambiguous. There is no way of distinguishing between files and subdirectories. But the Linux version of ls it is possible to get around this by using the color option, as in this example:

```
ls --color
```
Note that the word "color" must be spelt the American way, and that using "colour" instead will not work. If you try this on a directory containing a good selection of files the result should be a colourful display using a different colour for each file type. This list shows the colours used for several common file types.