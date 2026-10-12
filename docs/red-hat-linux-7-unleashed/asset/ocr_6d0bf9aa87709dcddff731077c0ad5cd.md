Since Red Hat Linux provides an entry in the filesystem table `/etc/fstab`, you could also mount the CD-ROM under the `/mnt/cdrom` directory by specifying your system's CD-ROM device, `/dev/cdrom` (a symbolic link to your CD-ROM's device), like this:

```
# mount /dev/cdrom
```

From the command line, use `rpm` like this:

```
# rpm -Uvh /mnt/cdrom/RedHat/RPMS/XFree86*rpM
```

If you did not install X, you can use Red Hat's `rpm` command to install the software. However, you should know that the process will involve solving many .rpm package dependencies!

# Note

You can also try using the `gnorpm` command to install the software. Select Preferences and then set the interface preference `RPM` path to the `RPMS` directory on your mounted Red Hat CD-ROM. KDE also includes a similar package manager client named `kpackage`.

Depending on the software installed, these directories can take up 40-400MB of hard drive space, and even more if you install a lot of X window managers, programming libraries, or other software. (A typical full installation of XFree86 is about 80-123MB, depending on the number of extra clients.)

# ## Choosing a Configuration Tool

The largest hurdle most new X users face after installing XFree86 is coming up with a working `XF86Config` file. This file can be initially generated during your install, but if you have a problematic graphics chipset, you may need to "tweak" your configuration after booting, or may even want to postpone configuring X11 until after you first log in. This is sometimes the safest approach; trying to log in to a Linux system configured to boot directly to X11 without a properly configured system can be confounding. Fortunately, if you run into this problem, you can simply press `Ctrl+Alt+Delete`, reboot, then either press `Ctrl+X` at the Red Hat LILO login, or pass the kernel argument `linux single` at the LILO boot prompt like this:

```
boot: linux single
```

If you already have a working setup, chances are your old XFree86 3.3.6 `XF86Config` may work, as there is some compatibility built into the new server. However, the new version of XFree86 uses a new layout and structure for the `XF86Config` file!