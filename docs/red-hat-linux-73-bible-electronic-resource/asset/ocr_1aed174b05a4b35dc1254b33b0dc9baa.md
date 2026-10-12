```
#bootloader --useLilo --linear --location=mbr
```

The second line that is commented out under the Boot Loader Configuration contains an example of how you would install the LILO boot loader instead of GRUB. In that example, the --linear option allows you to have the boot partition exist above cylinder 1024 on your hard disk.

Partitioning is required for a new install, optional for an upgrade. The code that follows is from the sample ks.cfg file. The zerombr yes value clears the Master Boot Record (to leave the MBR alone, set this to no). The clearpart --linux value removes existing Linux partitions (or use --all to clear all partitions). The part /boot, swap, and / lines set the sizes of those partitions (--size) to 50 MB, 256 MB, and 2000 MB, respectively. The root partition (/) can grow to a --maxsize of 3500 MB (if that much space is available).

```
### Partitioning Information
zerombr yes
clearpart --linux
part /boot --size 50
part swap --size 256
part / --size 2000 --grow --maxsize 3500
```

To indicate which packages to install, begin a section with the %packages command. (A few examples follow.) Designate whole installation groups, individual groups, or individual packages. After %packages, start an entry with an @ sign for a group of packages, and add each individual package by placing its name on a line by itself. The Package Designation example does a Server install, adds all X packages, and adds the ElectricFence package.

> **TIP:** You can find a listing of package groups and individual packages on the Red Hat installation CD. Find the comps file in the RedHat/base directory. However, if you start from the anaconda-ks.cfg file that resulted from installing Red Hat Linux, you might already have a set of packages that you want to install.

```
### Package Designation
%packages
# Use one of these whole installation groups:
@ Server
# @ KDE Workstation
# @ Gnome Workstation
# Add an individual group, such as X Window System:
@ X Window System
# Add an individual package, such as ElectricFence:
ElectricFence
```

> **NOTE:** The %packages command is not supported for upgrades.