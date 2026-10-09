# # RPM Components

The RPM package manager contains a number of components. Using these components, you can maintain a list of packages that are installed on the system.

![](bbox=[0.76, 0.1, 0.92, 0.15])

| Component | Description |
| :--- | :--- |
| The RPM local database | Tracks packages that are installed on the system. |
| The RPM package | Contains many executables and scripts required to install packages. |
| YUM | Acts as the front-end package installer for RPM. |
| RPM package files | Contains the source codes for the package. |

# # RPM Queries

An RPM query is a function that is used to query RPM for information on both installed and uninstalled packages. There are various options, which give distinct outputs, for the `rpm -q` command.

![](bbox=[0.77, 0.36, 0.93, 0.42])

```
```
[root@localhost ~]# rpm -qi samba
Name        : samba
Version     : 3.0.33
Release     : 3.7.el5
Install Date: Thu 25 Jun 2009 11:37:44 AM EDT
Group       : System Environment/Daemons
Size        : 31830025
Signature   : DSA/SHA1, Mon 15 Dec 2008 06:05:28 PM EST, Key ID 53266010137017180
Packager    : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
URL         : http://www.samba.org/
Summary     : The Samba SMB server.
Description :
Samba is the suite of programs by which a lot of PC-related machines
share files, printers, and other information (such as lists of
available files and printers). The Windows NT, OS/2, and Linux
operating systems support this natively, and add-ons packages can
enable the same thing for DOS, Windows, WWS, UNIX of all kinds, MVS,
and more. This package provides an SMB server that can be used to
provide network services to SMB (sometimes called "Lan Manager")
clients. Samba uses NetBIOS over TCP/IP (NetBI) protocols and does NOT
Relocations: (not relocatable)
Vendor: Red Hat, Inc.
Build Date: Tue 09 Dec 2008 11:03:42
Build Host: hs20-bcl-7.build.
redhat.com
License: GNU GPL Version 2
```
```

*Figure 7-5: Basic details of the samba package obtained using an rpm query.*

The options for the RPM query command are listed below.

| Option | Enables You To |
| :--- | :--- |
| `rpm -qa` | List all packages that are installed on your system. |
| `rpm -qc package_name` | List the configuration files of the specified package. |
| `rpm -qi package_name` | Give the basic details of the package such as installed date, size, and summary. |