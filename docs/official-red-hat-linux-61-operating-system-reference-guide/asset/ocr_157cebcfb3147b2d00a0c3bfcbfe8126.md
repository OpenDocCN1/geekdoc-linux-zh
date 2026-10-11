management program will start automatically (depending on you GUI environment) and can be used to install PowerTools. See Chapter 7, *Gnome-RPM* for specific instructions on how to use Gnome-RPM. See http://www.general.uwa.edu.au/~toivo/kpackage/ for more information on how to use Kpackage.

If you're not using GNOME or KDE, you'll need to use the shell prompt to install PowerTools. See Section 4.3.2, *Installing PowerTools from the Shell Prompt* for more information.

# 4.3.2 Installing PowerTools from the Shell Prompt

First, mount the PowerTools CD-ROM on your CD-ROM drive.

Place the PowerTools CD in your CD-ROM drive. As root, type the following:

```
```shell
# mount -t iso9660 /dev/cdrom /mnt/cdrom
```
```

> **Please note**
> On your system, you or the system administrator may already allow users (instead of only root) to mount the CD-ROM drive. Users have this privilege if the user option is included in the /dev/cdrom line in the /etc/fstab file. However, keep in mind that you must be logged in as root to install any PowerTools RPMs.

After you've mounted the drive, cd to the mounted CD-ROM directory with the following command:

```
```shell
# cd /mnt/cdrom
```
```

When you list the contents of the CD with ls, you'll see the following directories: SRPMS, alpha, i386, i586, i686, noarch, nosrc, sparc, and sparc64. The SRPMS directory contains the PowerTools source RPMs. The alpha, i386,