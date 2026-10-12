files, you may see a message such as saving /etc/banana.conf as /etc/banana.conf.rpmave. This means that during the upgrade, RPM considered your changes to the existing file to be potentially incompatible with the new configuration file in the new package. RPM saved your original configuration file and installed a new one. You should investigate and resolve the differences between the two files as soon as possible to ensure that your system continues to function properly.

Because upgrading is really a combination of uninstalling and installing, you can encounter regular errors from those modes, plus one additional error: If RPM thinks you are trying to upgrade to a package with an older version number, you will see

```
[root@cartoons]# rpm -Uvh banana-1.0-1.i386.rpm
banana    package banana-2.0-1 (which is newer) is already installed
error: banana-1.0-1.i386.rpm cannot be installed
[root@cartoons]#
```

To cause RPM to upgrade anyway, include - --oldpackage in the upgrade command:

```
[root@cartoons]# rpm -Uvh --oldpackage banana-1.0-1.i386.rpm
banana    ####################################################
[root@cartoons]#
```

# ## Querying

You can query the database to find installed packages by using the rpm -q command. A simple use is rpm -q banana, which will print the package name, version, and release number of the installed package banana. For example:

```
[scooby@cartoons]$ rpm -q banana
banana-2.0-1
[scooby@cartoons]$
```

# ## Package Specification Options

Instead of specifying the package name, you can use the Package Specification Options with -q to specify the package(s) that you want to query. These options include the following:

+   - a-Queries all currently installed packages.   
+   - f <file>—Queries the package owning the specified file.   
+   - p <packagefile>—Queries the specified package filename.