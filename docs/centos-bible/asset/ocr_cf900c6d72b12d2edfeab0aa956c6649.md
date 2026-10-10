```
#part /boot --fstype ext3 --size=100 --ondisk=sda
#part / --fstype ext3 --size=700 --grow --ondisk=sda
#part swap --size=128 --grow --maxsize=256 --ondisk=sda
```

To indicate which packages to install, begin a section with the `%packages` command. (A few examples follow.) Designate whole installation groups, individual groups, or individual packages. On the `%packages` line, you can indicate whether or not to resolve dependencies by installing those packages needed by the ones you selected (--resolvedeps). After `%packages`, start an entry with an @ sign for a group of packages, and add each individual package by placing its name on a line by itself. Here is an example:

```
%packages --resolvedeps
@base
@editors
@games
@graphical-internet
@kde-desktop
@office
@sound-and-video
...
```

> **NOTE** The `%packages` command is not *supported* for upgrades. To install everything, you can remove the package names shown. Then, after the `%packages` line, you can add an `@everything` line.

The `%post` command starts the post-installation section. After it, you can add any shell commands you want to run after installation is completed. A useful thing to do is to add `useradd` commands for users you want to add during installation. You can also use the `usermod` command to add the user's password. Note that there is no `%post` section by default.

```
%post
/usr/sbin/useradd jake
chfn -f 'John W. Jones' jake
/usr/sbin/usermod -p '$1kOUMyBFOh79wECxnTuah.' Jake
```

At this point, you should have a working ks.cfg file.

# Installing the Kickstart File

Once the ks.cfg file is created, you need to put it somewhere accessible to the computer doing the installation. Typically, you will place the file on a floppy disk. However, you can also put the file on a computer that is reachable on the network or on a hard disk.

To copy the file to a floppy disk, create a DOS floppy and copy the file as follows:

```
# mcopy ks.cfg a:
```