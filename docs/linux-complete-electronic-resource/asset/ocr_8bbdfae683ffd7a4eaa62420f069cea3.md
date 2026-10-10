# NOTE

It is important that these components are installed in the order listed and that they are installed before any other KDE component.

If you are upgrading from a previous release, try:
```
rpm -Uvh kde-component.arch.rpm
```

Once again, the order given above should be preserved, and the given components should be installed before any other KDE components.

This will unpack the base distribution and install it in */opt/kde*. If the installation of the base packages has been successful, you can install the remaining packages (use *-Uvh* instead of *-i* once again to update an existing version) the same way.

# Linux: Installing on Top of a Debian/GNU Linux Distribution

An important note before you start: Due to various problems arising from the Linux filesystem standard, building *.deb* packages is very complex. Therefore, you will probably not find the most current version. If you want to see the newest in KDE development, we recommend you get the source distribution (see the following section on “Using TGZ to Install on Top of Other Systems” for details).

Retrieve the following files in order to get KDE installed on your Debian/GNU Linux system. You can find them in */pub/kde/unstable/distribution/dpkg*.

+   ► *libgif22.3-1i386.deb*
+   ► *libkde00.10.01-1i386.deb*
+   ► *kdeapps0.10.01-2i386.deb*

In addition, KDE requires components from the following packages. Make sure they are installed before beginning the KDE installation:

+   ► *qt1.42*
+   ► *libjpeg6*
+   ► *libg++27*