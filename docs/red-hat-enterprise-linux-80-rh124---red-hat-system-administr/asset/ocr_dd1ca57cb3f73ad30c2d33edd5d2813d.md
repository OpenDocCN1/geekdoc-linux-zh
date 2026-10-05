# NOTE

Use yum list kernel to list all installed and available kernels. To view the currently running kernel, use the uname command. The -r option only shows the kernel version and release, and the -a option shows the kernel release and additional information.

```
[user@host ~]$ yum list kernel
Installed Packages
kernel.x86_64         4.18.0-60.el8 @anaconda
kernel.x86_64         4.18.0-67.el8 @rhel-8-for-x86_64-baseos-htb-rpms
[user@host ~]$ uname -r
4.18.0-60.el8.x86_64
[user@host ~]$ uname -a
linux host.lab.example.com 4.18.0-60.el8.x86_64 #1 SMP Fri Jan 11 19:08:11 UTC 2019 x86_64 x86_64 GNU/Linux
```

+   * yum remove PACKENAME removes an installed software package, including any supported packages.

```
[user@host ~]$ sudo yum remove httpd
```

> WARNING
The yum remove command removes the packages listed and any package that requires the packages being removed (and packages which require those packages, and so on). This can lead to unexpected removal of packages, carefully review the list of packages to be removed.

# Installing and removing software with yum

+   * yum has the concept of groups, which are collections of related software installed together for a particular purpose. In Red Hat Enterprise Linux 8, there are two kinds of groups. Regular groups are collections of packages. Environment groups are collections of regular groups. The packages or groups provided by a group may be mandatory (they must be installed if the group is installed), default (not installed if the group is installed), or optional (not installed unless specifically requested).

Like yum list, the yum group command shows the names of installed and available groups.

```
[user@host ~]$ yum group list
Available Environment Groups:
Server with GUI
Minimal Install
Server
...output omitted...
Available Groups:
Container Management
.NET Core Development
```