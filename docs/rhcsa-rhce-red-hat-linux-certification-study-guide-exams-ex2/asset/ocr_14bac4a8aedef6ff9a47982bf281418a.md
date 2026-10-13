Once the file is saved, run the following commands, to first clear out databases from previously accessed repositories, and then to update the local database from the repository newly configured in the /etc/yum.repos.d/whatever.repo file.

```
```bash
# yum clean all
# yum update
```
```

For a system not registered with the RHN, it'll lead to the following output:

```
```
Loaded plugins: refresh-packagekit, rhnplugin
This system is not registered with RHN.
RHN support will be disabled.
test                          | 3.7 kB     00:00
test/primary_db               | 2.9 MB     00:00
Setting up Update Process
No Packages marked for Update
```
```

The system is now ready for the installation of new packages. Try running the following command:

```
```bash
# yum install system-config-printer
```
```

Given the virtual machines configured earlier in this book, you might see the result shown in Figure 7-9. If confirmed, the yum command would download and then install not only the system-config-printer RPM, but also the four dependent packages shown in the figure to make sure the system-config-printer package is fully supported.

# FIGURE 7-9

Installation of one package can include dependencies.

```
```
Dependencies Resolved

Package                     Arch     Version          Repository   Size
================================================================================
Installing:
system-config-printer       x86_64   1.1.16-17.el6    test         444 k
Installing for dependencies:
gnome-python2-gnomekeyring  x86_64   2.28.0-4.el6     test         24 k
libbonoboi                  x86_64   3.5.4-68.el6     test         1.7 M
notify-python               x86_64   0.1.1-10.el6     test         26 k
system-config-printer-libs  x86_64   1.1.16-17.el6    test         651 k

Transaction Summary
================================================================================
Install       5 Package(s)
Upgrade       0 Package(s)

Total download size: 2.8 M
Installed size: 12 M
Is this ok [y/N]:
```
```