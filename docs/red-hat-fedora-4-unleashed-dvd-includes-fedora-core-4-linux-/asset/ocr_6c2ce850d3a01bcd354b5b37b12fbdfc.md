As long as the superuser understands the syntax and options of the *fstab* file, she can edit the file with any text editor.

# # GUI Tools to Mount File Systems

The *usermount* graphical file system management client is available for use with Fedora Core Linux. Although Fedora Core provides *usermount* as the default file system mounting tool, it is not as feature-rich as *KDiskFree*, which is installed when you select the KDE desktop during installation.

The K Desktop Environment (KDE) provides several disk- and file system-related utilities. You might find one or more available on your Fedora Core system if you select KDE for installation. Found in the *Extras* menu under *System Tools*, the *KDiskFree* menu item (it is `kdf` from a command line) displays all the file systems noted in the `/etc/fstab` file, presents information about them, and allows you to easily mount and unmount them (see Figure 37.1). *KwikDisk* enables mounts and unmounts from a panel applet.

> **TIP**
> *KwikDisk* is the KDE panel applet for *KDiskFree*. You would normally right-click on the KDE panel and add the applet to the panel. Fedora Core has omitted *KwikDisk* from the *KDE* applet menu, but still includes it with Fedora Core. Launch it from a command line, and it will appear on the KDE panel or on the GNOME desktop. Clicking on the *KwikDisk* panel icon launches an abbreviated version of *KDiskFree*:

```
`$ kwikdisk &`
```

![](bbox=[0.23, 0.58, 0.8, 0.83])

**FIGURE 37.1** *KDiskFree* provides a graphical interface to tools used to configure custom mount options, as well as mount, or unmount, disks.

The *User Mount Tool*, accessed from the *System Tools* menu as the *Disk Management* menu item, is a convenient way to mount and unmount file systems (see Figure 37.2). It also allows you to format floppy disks.