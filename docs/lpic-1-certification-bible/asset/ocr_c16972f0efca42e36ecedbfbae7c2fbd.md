If you want to display this information about a package you have not yet installed, use the -p option.

```
rpm -qp `package_file.rpm`
```

# **Printing package scripts**

Some packages include scripts that run before or after they are installed. To display these scripts use the following command:

```
rpm -qp --scripts `package_file.rpm`
```

For example, to show the scripts that run when the package `kernel-2.2.14-5.0.i686.rpm` is installed, you would execute the following:

```
[root@redhat /root]# rpm -qp --scripts
/mnt/cdrom/RedHat/RPMS/kernel-2.2.14-5.0.i686.rpm
preinstall script (through /bin/sh):
/sbin/modprobe loop 2>/dev/null >/dev/null
exit 0
postinstall script (through /bin/sh):
cd /boot
ln -sf vmlinuz-2.2.14-5.0 vmlinuz
ln -sf System.map-2.2.14-5.0 System.map
ln -sf module-info-2.2.14-5.0 module-info

# Allow clean removal of modules directory
preuninstall script (through /bin/sh):
rm -f /lib/modules/2.2.14-5.0/modules.dep
```

# **Verifying package files**

You sometimes need to check if a file has changed since a package was installed. You may have made a change to some configuration file and now need to know which were modified. The rpm tool provides this functionality with the -V verification option.

```
rpm -V `package_name`
```

When a verify is performed, rpm checks the files that were installed for a number of characteristics and displays those that have changed, and the items that have changed. Each file has an entry in the RPM database that stores its MD5 checksum, file size, symbolic link pointer, modification time, user and group owners, and permissions and file types. If the file is a device, the major and minor device numbers are checked as well. Table 3-1 shows the output given by the verification for any file that has changed.