# CAUTION

The Livna repository is home to not only a wide range of kernel modules and drivers for many popular items of hardware, but also contains a number of legally question-able packages that are not enabled in Fedora by default, including native MP3 support. If you are using Fedora for personal use, you should not have any real problems, but make sure to check before you start installing packages from Livna onto a corporate workstation or server!

To get the NVIDIA driver using yum, you need to have enabled the Livna repository (see Chapter 34, “Advanced Software Management,” for more information on setting up repositories). At the command line, type

```
```bash
#yum install kmod-nvidia
```
```

and press Enter. After a few seconds, yum retrieves and downloads the latest NVIDIA driver that is appropriate for your current kernel version. After it finishes installing the packages, you have to restart your machine to take advantage of the improvements.

Installing the ATI driver is much the same because Livna.org also has a set of drivers available for ATI hardware. As with the NVIDIA driver, you need to be a super user and enter the following command:

```
```bash
#yum install kmod-fglrx
```
```

A restart of the system is necessary before you can make full use of the 3D capabilities of your card.

# CAUTION

Both sets of graphics card drivers are very dependent on the kernel version you are running. Every time you update your kernel, you also have to update your driver. If you have used the kmod-* package from Livna, it should automatically update when you run yum upgrade.

# # Installing Popular Games in Fedora

It’s a common misconception that Linux doesn’t do games. In fact, that assumption is very wrong, as you are about to see. In this section, we walk through how to install five popular games that you can play within Fedora. Make sure that you have followed the earlier instructions on how to install graphics drivers for your graphics card; otherwise, you are likely to struggle with the likes of Doom 3, Unreal Tournament 2004, and Quake 4.