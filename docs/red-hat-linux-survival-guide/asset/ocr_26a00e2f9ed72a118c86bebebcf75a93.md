This command produces the following information about the named package:

```
Name          : vlock          Relocations: (not relocateable)
Version       : 1.3            Vendor: Red Hat, Inc.
Release       : 5              Build Date: Thu 13 Jul 2000 11:25:38 AM BDT
Install date: (not installed) Build Host: porky.devel.redhat.com
Group         : Applications/System Source RPM: vlock-1.3-5.src.rpm
Size          : 8857           License: GPL
Packager      : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
Summary       : A program which locks one or more virtual consoles.
Description :
The vlock program locks one or more sessions on the console. Vlock can lock the current terminal (local or remote) or the entire virtual console system, which completely disables all console access. The vlock program unlocks when either the password of the user who started vlock or the root password is typed.
```

![](bbox=[0.07, 0.55, 0.18, 0.62])

If you wish to know what files this package will install, run the rpm -qlp package_name command. For example:

```
rpm -qlp vlock-1.3-5.i386.rpm
```

This command shows the following output:

```
/etc/pam.d/vlock
/usr/bin/vlock
/usr/share/man/man1/vlock.1.gz
```

# Finding out which package a file belongs to

To find out which package a particular file belongs to, run the following command:

```
rpm -qf path_to_file
```