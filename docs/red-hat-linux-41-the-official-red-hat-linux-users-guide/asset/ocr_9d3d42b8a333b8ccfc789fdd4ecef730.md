Since upgrading is really a combination of uninstalling and installing, you can encounter any errors from those modes, plus one more: If RPM thinks you are trying to upgrade to a package with an *older* version number, you will see:

```
$ rpm -Uvh foo-1.0-1.i386.rpm
foo              package foo-2.0-1 (which is never) is already installed
error: foo-1.0-1.i386.rpm cannot be installed
```

To cause RPM to “upgrade” anyway, use *--oldpackage* on the command line.

# 7.2.4 Querying

Querying the database of installed packages is accomplished with *rpm -q*. A simple use is *rpm -q foo* which will print the package name, version, and release number of the installed package foo:

```
$ rpm -q foo
rpm-2.0-1
```

Instead of specifying the package name, you can use the following options with *rpm -q* to specify what package(s) you want to query. These are called *Package Specification Options*.

+   - *-a* queries all currently installed packages.
+   - *-f <file>*** will query the package owning <file>.
+   - *-F* is the same as *-f* except it takes filenames via stdin (e.g. *find /usr/bin | rpm -qF*).

+   - *-p <packagefile>*** queries the package <packagefile>.
+   - *-P* is like *-p* except it takes package filenames from stdin (e.g. *find /mnt/cdrom/RedHat/RPMS | rpm -qP*).

There are a number of ways to specify what information to display about queried packages. The following options are used to select the information you are interested in. These are called *Information Selection Options*.