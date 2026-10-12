# ## Preparing for a Kernel Upgrade

The official FTP site for the Red Hat Linux updates is `ftp://updates.redhat.com/`. Accessing this busy site can be difficult at times. Your best choice is to locate a mirror site near you, by visiting `http://www.redhat.com/mirrors.html`.

After you locate a mirror site for the updated kernel RPM packages, connect to the site and compare the latest packages with the versions of the packages already stored in your `/current-kernel-pkgs.txt` file. Download the newer packages. If you do not see a newer package for one of the packages listed in the `/current-kernel-pkgs.txt` file, just ignore it, because a newer package is not yet available.

After you have the new packages for your kernel upgrade, create an emergency boot floppy, just in case something goes wrong with the kernel upgrade. Also, keeping a copy of the old kernel in a directory within the root partition is a good idea.

To create a standalone boot floppy, insert a formatted floppy disk into your floppy drive and run

```
```
mkbootdisk 2.x.x.x-x
```
```

replacing `2.x.x.x` with your current kernel version that you identified earlier. Also, if you have multiple floppy drives and do not want to use the default floppy device (`/dev/fd0`), use the `--device` option to specify your floppy device of choice. For example,

```
```
mkbootdisk --device /dev/fd1 2.0.36-0.7
```
```

creates the emergency boot floppy on `/dev/fd1` using kernel image version `2.0.36-0.7`. After you create the boot disk, reboot your system using this floppy to ensure that the emergency boot disk actually works.

# ## Installing the New Kernel

After you test the emergency boot disk, you are ready to install a new kernel. Using `rpm`, install all the packages you have downloaded. I typically download all the new packages to a new directory in a temporary space, such as `/tmp/new-kernel-pkgs`, and run the following:

```
```
rpm -ivh /tmp/new-kernel-pkgs/*.rpm
```
```