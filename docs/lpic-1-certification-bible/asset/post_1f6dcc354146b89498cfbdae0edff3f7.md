
The RPM database stored in /var/lib/rpm holds information about every package installed on the system. You can expose this data to gather information to help maintain your systems. All of the query options are done using the `rpm` command with the `-q` option.

### Listing installed packages

The most basic query is to check the version of an installed package:

```
rpm -q package_name
```

or:

```
rpm --query package_name
```

For example:

```
[root@redhat /root]# rpm -q kernel
kernel-2.2.14-5.0
```

To list every package installed on your system use the `-a` option:

```
rpm -qa
```

Combine this with `grep` to see which groups of packages you have installed. The `grep` command searches for specific text patterns in a file, and the pipe symbol (`|`) redirects the output from one command to another command. The following example uses `rpm -qa` to find all the packages, and `grep` searches that list for the packages that contain the word `kernel`.

```
[root@redhat /root]# rpm -qa | grep kernel
kernel-headers-2.2.14-5.0
kernel-2.2.14-5.0
kernel-pcmcia-cs-2.2.14-5.0
kernel-utils-2.2.14-5.0
```

![](img/96d9ccd181675a8ae8b6a1146c919d2b_145_0.png)

The `grep` command and pipes are discussed in detail in Chapter 4.

### Checking the package that installed a file

There may be a time when you are not sure which package installed a file and you need to know. The `-f` option provides this information.

```
rpm -qf filename
```

For example:

```
[root@redhat /root]# rpm -qf /etc/bashrc
bash-1.14.7-22
```

This tells you that the `bashrc` file was installed by the package `bash-1.14.7-22`.

### Listing files in a package

To list all the files installed by a package use the `-l` option.

```
rpm -ql package_name
```

For example, to list all files in the `openssh-clients` package you would use the following:

```
[root@redhat /root]# rpm -ql openssh-clients
/etc/ssh/ssh_config
/usr/bin/slogin
/usr/bin/ssh
/usr/bin/ssh-add
/usr/bin/ssh-agent
/usr/man/man1/slogin.1.gz
/usr/man/man1/ssh-add.1.gz
/usr/man/man1/ssh-agent.1.gz
/usr/man/man1/ssh.1.gz
```

To list the files that will be installed with a package use the additional `-p` option.

```
rpm -qlp package_file.rpm
```

### Displaying package information

To print the description and other information about a package use the `-i` option.

```
rpm -qi package_name
```

For example, to display the information about the installed Linux kernel you would do the following:

```
[root@redhat /etc]# rpm -qi kernel
Name     : kernel
Version    : 2.2.14
Release    : 5.0
Install date: Wed 01 Nov 2000 06:58:30 PM EST
Group      : System Environment/Kernel
Size       : 11973135
Packager   : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
Summary    : The Linux kernel (the core of the Linux operating system).
Description :
The kernel package contains the Linux kernel (vmlinuz), the core of your
Red Hat Linux operating system.  The kernel handles the basic functions of
the operating system: memory allocation, process allocation, device
input and output, etc.
Relocations: (not relocatable)
Vendor: Red Hat, Inc.
Build Date: Tue 07 Mar 2000 09:13:08 PM EST
Build Host: porky.devel.redhat.com
Source RPM: kernel-2.2.14-5.0.src.rpm
License: GPL
```

If you want to display this information about a package you have not yet installed, use the `-p` option.

```
rpm -qp package_file.rpm
```

### Printing package scripts

Some packages include scripts that run before or after they are installed. To display these scripts use the following command:

```
rpm -qp --scripts package_file.rpm
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

### Verifying package files

You sometimes need to check if a file has changed since a package was installed. You may have made a change to some configuration file and now need to know which were modified. The `rpm` tool provides this functionality with the `-V` verification option.

```
rpm -V package_name
```

When a verify is performed, `rpm` checks the files that were installed for a number of characteristics and displays those that have changed, and the items that have changed. Each file has an entry in the RPM database that stores its MD5 checksum, file size, symbolic link pointer, modification time, user and group owners, and permissions and file types. If the file is a device, the major and minor device numbers are checked as well. Table 3-1 shows the output given by the verification for any file that has changed.

#### Table 3-1
Package Verification Characteristics

| Item | Meaning |
|---|---|
| . | No change for this characteristic |
| S | The MD5 checksum has changed |
| L | File size has changed |
| D | Symbolic link has changed |
| D | The device major and/or minor number has changed |
| U | User owner has changed |
| G | Group owner has changed |
| M | Permission and/or file type has changed |

For example, to see which configuration files installed by the `setup` package have changed you would enter the following:

```
[root@redhat /etc]# rpm -V setup
S.5....T c /etc/hosts.allow
......G c /etc/profile
S.5....T c /etc/services
```

This output shows that for the `hosts.allow` file and the `services` file, the file size, MD5 checksum, and modification time have changed. For the `profile` file, the group owner has changed, but nothing else.

To verify a package by using the package filename, use the `-p` option.

```
rpm -Vp package_file.rpm
```

To verify every package installed on the system use the `-a` option. This is a fast way to see which files have changed since the system was installed.

```
rpm -Va
```

### Creating binary packages from source packages

Not all RPM packages distribute binary files. Some distribute the source code and install scripts that let you build your own binary RPMs. These are useful when you want to optimize or change a package. These packages have a slightly different naming scheme, since they are not dependent on a particular system architecture.

```
package-version-patch.src.rpm
```

Source RPMs are installed just like binary packages, with the `rpm -i` command. This places the different pieces into the `/usr/src/redhat` hierarchy of directories. Table 3-2 shows the purpose of the directories in this tree.

**Exam Tip**  
For the exam you should know how to build a binary package from a source package, including how to modify the `spec` file.

#### Table 3-2
Subdirectories in the /usr/src/redhat Tree

| Directory | Purpose |
| :--- | :--- |
| `/usr/src/redhat/SOURCES` | Contains the application source code |
| `/usr/src/redhat/SPECS` | Contains the RPM `spec` file |
| `/usr/src/redhat/BUILD` | Where source code is built |
| `/usr/src/redhat/RPMS` | Contains the final binary RPM |
| `/usr/src/redhat/SRPMs` | Contains the source RPM built by the process |

The `spec` file for a package controls how the package is compiled and the scripts that run when it is installed or removed. This file is named `/usr/src/redhat/SPECS/package_name.spec`. The `spec` file has eight sections, as shown in Table 3-3.

#### Table 3-3
`spec` File Sections

| `spec` File Section | Description |
| :--- | :--- |
| Header | General information such as summary, name, version, and so on |
| Prep | Shell scripts that do any work needed before the compile process |
| Build | Commands to build the `spec` file and compile the source code |
| Install | Commands needed to install the software on a system |
| Clean | Optional commands to clean up the build environment, in case this package is rebuilt again |
| Optional Install and Uninstall Scripts | Scripts that may be run during install or uninstall of the package |
| File List | List of files in the package |
| Changelog | Log of any changes you make to the package |
