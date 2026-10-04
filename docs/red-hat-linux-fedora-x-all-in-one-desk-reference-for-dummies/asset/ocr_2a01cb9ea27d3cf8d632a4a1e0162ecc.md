# Determining Whether You Have Perl 781

Now, try which perl command again. If you still get an error, you may not have installed Perl. You can install Perl from the companion DVD-ROM by performing the following steps:

+   Log as root.

+   Insert the companion DVD-ROM in the DVD-ROM drive. If you are working in the GNOME or KDE graphical environment, the DVD-ROM mounts atomically. Otherwise, mount the DVD-ROM by typing the following command:
mount /mnt/cdrom

```
mount /mnt/cdrom
```

+   Type the following command to change the directory to the location of the Red Hat packages:
cd /mnt/cdrom/Fedora/RPMS

```
cd /mnt/cdrom/Fedora/RPMS
```

+   Type the following rpm (Red Hat Package Manager) command to install Perl:
-ivh perl*

```
-ivh perl*
```

After you install Perl on your system, the following command to see its version number:

```
perl -v
```

Here is typical output from command:

This is perl, v5.8.3 built for i386-linux-thread-multi

Copyright 1987-2003, Larry Wall

Perl may be copied only under the terms of either the Artistic License or the GNU General Public License, which may be found in the Perl 5 source kit.

Complete documentation for Perl, including FAQ lists, can be found on this system using 'man perl' or 'perldoc perl'. If you have access to the Internet, point your browser at http://www.perl.com/. the Perl Home Page.

This tells you that you have Perl Version 5.8, patch Level 3, and Larry Wall, the originator of Perl, holds the copyright (Remember, however, Perl is distributed freely under the General Public License).

You can get the latest version of Perl by pointing your World Wide Web browser to the Comprehensive Perl Archive Network (CPAN). The following address connects you to the CPAN site nearest to you:

![](bbox=[0.125, 0.768, 0.196, 0.843])

```
www.perl.com/CPAN/
```