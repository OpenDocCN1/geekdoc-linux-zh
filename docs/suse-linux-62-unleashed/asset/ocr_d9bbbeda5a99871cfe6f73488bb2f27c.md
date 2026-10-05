# Graphics, Multimedia, and Productivity Tools
PART IV

Generally, the mformat, mdir, mcopy, and mdel commands are the most often used. The mformat command formats nearly any type of floppy disk. One nice feature of this software is that you don't have to remember the specific names of floppy devices, such as /dev/fd0, and you can use the (possibly) familiar A: or B: drive designations. This is possible because of mtool's use of the /etc/mtools.conf configuration file, /etc/mtools.conf.

Entries for different disk devices are listed in the file. You can edit the file (as root) to configure mtools for your system having to rebuild the software (although if you need the source, you can readily find a copy on your favorite Linux site, or at ftp://ftp.tux.org/pub/knaff/mtools, along with numerous addons and utilities). If you examine the /etc/mtools.conf file, you'll see entries for different devices, and configurations for other operating systems. For example the floppy device entries like this:

```
drive a: file="/dev/fd0" exclusive mformat_only cylinders=80 heads=2=18
drive b: file="/dev/fd1" exclusive mformat_only cylinders=80 heads=2=18
```

These entries allow you to easily format a floppy in drive A: without mounting the disk, like this:

# mformat a:

After the mformat command has finished, you can copy files to and from the diskette the mcopy command:

# mcopy *.txt a:

This will copy all files ending in .txt to your diskette. To copy files from your diskette, just reverse the arguments (in DOS form) to the mcopy command:

# mdir a

This will copy all files ending in .txt to the current directory, or to a directory you specify. Use the mdir command to see what is on the diskette:

Volume in drive A has no label
Volume Serial Number is 4917 9EDD
Directory for A:/

```
launch gif 62835 04 09 1999 13:44 launch.gif
vmware gif 10703 04 09 1999 13:44 vm.gif
vnc gif 21487 04 09 1999 13:44 vnc.gif
3 files 95 025 bytes
1 362 432 bytes free
```