To install a package with apt-get, simply type apt-get install *packagename*, where *packagename* is the name of the package that you want to install. For example, to install the vsftpd package, type apt-get install vsftpd.

Removing a package is equally simple. Type apt-get remove *packagename*, where *packagename* is the name of the package you want to remove.

If you want to find the name of a package and you know some terms associated with the package, you can look for it with the apt-cache utility. For example, to look for a CD/DVD burner package, I type apt-cache search burn 1 more to search through the APT's package cache (which is the list of Debian packages that APT downloads from the servers listed in the /etc/apt/sources.list file). Here are some lines of output from that command:

```
arson - KDE frontend for burning CDs
burn - Command line Data-CD, Audio-CD, ISO-CD, Copy-CD writing tool
caca-utils - text mode graphics utilities
cdcontrol - A parallel burner that allow you to write to one or more CD-Writers at once
cdlabelgen - generates front cards and tray cards for CDs and DVDs
cdtoastster - Tcl/Tk front-end for burning cdrom
cdw - Tool for burning CD's - console version
cdw-common - Tool for burning CD's - common files
cdphum - a collection of programs to put heavy load on CPU
cdxdr - Chez Wam CD Ripper
dvd-rw-tools - DVD+RW/R tools
dvdbackup - tool to rip DVD's from the command line
edcmath.app - Scientific calculator for GNUstep
gcdr - Tool for burning CD's - graphical version
gscdumst - GTX based CD mastering and burning program
... lines deleted ...
```

The output shows several potential CD/DVD burning programs that I could install. To discover more about any of the packages, I type apt-cache show *packagename*, where *packagename* is the name of the package for which I want information. For example, to find out more about the dvd-rw-tools package, I type apt-cache show dvd-rw-tools and the output shows me a description of the package. I can then install the package with apt-get install.

![](bbox=[0.15, 0.75, 0.22, 0.83])

To search for a keyword that appears in the package's name only, use the --names-only option like this: apt-cache search --names-only *keyword*, where *keyword* is something that appears in the package's name. For example, if I want to find packages that contain selinux in their names, I type apt-cache search --names-only selinux.