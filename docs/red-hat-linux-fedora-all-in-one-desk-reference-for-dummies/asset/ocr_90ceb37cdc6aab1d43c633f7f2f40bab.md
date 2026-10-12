+   - `smbmount`: This program unmounts a currently mounted Samba share directory.
+   - `testparm`: This program ensures that the Samba configuration file is correct.
+   - `winbindd`: This server resolves names from Windows NT servers.

In the following sections, I describe how to install Samba from the companion CD-ROM and how to print from the Red Hat Linux PC to a shared printer on a Windows PC.

# Checking whether Samba is installed

Check whether Samba is installed by typing the following command in a terminal window:

```
rpm -q samba
```

If you see an output similar to the following, Samba is already installed on your system:

```
samba-3.0.0-5rc1
```

If you get a message saying that the package isn't installed, follow these steps to install Samba from this book's companion CD-ROM:

+   1. **Log in as root and insert the first DVD into the drive. If you're using GNOME or KDE, the DVD should automatically be mounted. If not, type the following command to mount the DVD:**
+      `mount /mnt/cdrom`
+   2. **Change the directory to the DVD — specifically to the directory where the Red Hat Package Manager (RPM) packages are located — with the following command:**
+      `cd /mnt/cdrom/RedHat/RPMS`
+   3. **Use the following rpm command to install Samba:**
+      `rpm -ivh samba*`
+      If Samba is already installed, this command returns an error message. Otherwise, the rpm command installs Samba on your system by copying various files to their appropriate locations.

After installing the Samba software you have to configure Samba before you can use it.