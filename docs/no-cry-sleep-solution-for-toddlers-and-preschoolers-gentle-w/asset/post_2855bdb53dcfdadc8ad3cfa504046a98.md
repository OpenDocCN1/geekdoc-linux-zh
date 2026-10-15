
The syntax for the mkfs command is as follows. You can add options for a particular file system after the type and before the device. The block size is used for file builders that do not detect the disk size.

```
mkfs options [-t type] file-system options device size
```

> Tip Once you have formatted your disk, you can label it with the e2label command as described earlier in the chapter.

The same procedure works for floppy disk. In this case, the mkfs command takes as its argument the device name. It uses the ext2 file system (the default for mkfs), because a floppy is too small to support a journaling file system.

```
# mkfs /dev/fd0
```

> Tip On the desktop, you can use the Floppy Formatter tool listed in the System Tools menu to format your floppy disks. The formatter enables you to choose an MS-DOS or Linux file system type.

## mkswap

If you want to create a swap partition, you first use fdisk or parted to create the partition, if it does not already exist, and then you use the mkswap command to format it as a swap partition. mkswap formats the entire partition unless otherwise instructed. It takes as its argument the device name for the swap partition.

```
mkswap /dev/hdb2
```

You then need to create an entry for it in the /etc/fstab file so that it will be automatically mounted when your system boots.

## CD-ROM and DVD ROM Recording

Recording data to CD-ROM disks on Linux involves creating a CD image file of the CD-ROM, and then writing that image file to a CD-R or CD-RW disc in your CD-R/RW drive. With the mkisofs command, you can create a CD image file, which you can then write to a CD-R/RW write device. Once you create your CD image file, you can write it to a CD-write device, using the cdrecord or cdwrite application. The cdrecord application is a more powerful application with many options. You can also use GNOME and KDE CD recording applications such as K3b and GNOME Toaster to create your CDs easily. Most are front ends to the mkisofs and cdrecord tools. To record DVD disks on DVD writers, you can use dvdrrecord (the counterpart to cdrecord) for DVD-R/RW drives and the dvd+rw tools for DVD+R/R drives. If you want to record CD-ROMs on a DVD writer, you can just use cdrecord.

The dvdrtools application currently works only on DVD-R/RW drives; it is part of the dvdrtools package. If you want to use DVD+RW/R drives, you would use the dvd+rw tools such as growisofs and dvd+rw-format. dvd+rw tools are included on Red Hat in the dvd+rw-tools package. Check the DVD+R/W tools Web site for more information, http://fy.chalmers.se/~appro/linux/DVD+RW.

## mkisofs

To create a CD image, you first select the files you want on your CD. Then you can use mkisofs to create an ISO CD image of them.

### mkisofs Options

You may need to include several important options with mkisofs to create a data CD properly. The -o option is used to specify the name of the CD image file. This can be any name you want to give it. The -R option specifies RockRidge CD protocols, and the -J option provides for long Windows 95/98/ME or XP names. The -r option, in addition to the RockRidge protocols (-R), sets standard global permissions for your files, such as read access for all users and no write access because the CD-ROM is read-only. The -T option creates translation tables for filenames for use on systems that are not RockRidge-compliant.

The -U option provides for relaxed filenames that are not standard ISO-compliant, such as long filenames, those with more than one period in their name, those that begin with a period such as shell configuration files, and ones that use lowercase characters (there are also separate options for each of these features if you just want to use a few of them). Most RPM and source code package names fall in this category. The -iso-level option lets you remove ISO restrictions such as the length of a filename. The -V option sets the volume label (name) for the CD. Finally, the -v option displays the progress of the image creation.

### Disk Image Creation

The last argument is the directory that contains the files for which you want to make the CD image. For this, you can specify a directory. For example, if you are creating a CD-ROM to contain the data files in the mydocs directory, you would specify that directory. This top directory will not be included, just the files and subdirectories in it. You can also change to that directory and then use . to indicate the current directory.

If you were creating a simple CD to use on Linux, you would use mkisofs to first create the CD image. Here the verbose option will show the creation progress, and the -V option lets you specify the CD label. A CD image called songs.iso is created using the file located in the newsong directory:

```
mkisofs -v -V "Goodsongs" -o moresongs.iso newsongs
```

If you also wanted to use the CD on a Windows system, you would add the -r (RockRidge with standard global file access) and -J (Joliet) options:

```
mkisofs -v -r -J -V "Goodsongs" -o moresongs.iso newsongs
```

You need to include certain options if you are using filenames that are not ISO compliant, such as ones with more than 31 characters or ones that use lowercase characters. The -U option lets you use completely unrestricted filenames, whereas certain options like -L for the unrestricted length will release specific restrictions only. The following example creates a CD image called mydoc.iso using the files and subdirectories located in the mdoc directory and labels the CD image with the name "doc":

```
mkisofs -v -r -T -J -U -V "Greatdocs" -o mydocuments.iso mydocs
```
