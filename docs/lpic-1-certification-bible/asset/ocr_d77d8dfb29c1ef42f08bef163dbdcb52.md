# # Removing packages

# ## 2.2 Installation and Package Management

+   - **Use Red Hat Package Manager (rpm).** Familiarize yourself with these tasks:
+     - Uninstall a package.

You remove a package with the -e or --uninstall options:

```
rpm -e package_name
```

or:

```
rpm --uninstall package_name
```

> > **Tip**
> >
> > When removing a package, remember to use the package name, not the filename.
> > Wildcards also do not work when removing packages.

Both options perform the same function; some people just find the -uninstall easier to remember. To help memorize -e, consider its standing for erase. When a package is removed, rpm does the normal dependency checks and will not let you remove a package if another depends on it, by default.

```
[root@redhat jason]# rpm -e libcap
error: removing these packages would break dependencies:
libcap >= 0.4 is needed by ethereal-0.8,9-1
```

The --nodeps option can be used to override these warnings. Remember that when removing a package you need to specify the package name, not the filename that was installed. Also, wildcards will not work. When a package is removed, rpm saves any configuration files that were changed from the default. This way you can reinstall the package later without needing to reconfigure it.

```
[root@redhat jason]# ls /etc/pine*
/etc/pine.conf
[root@redhat jason]# rpm -e pine
[root@redhat jason]# ls /etc/pine*
/etc/pine.conf.rpmsave
[root@redhat jason]#
```

# # Querying the RPM database

# ## 2.2 Installation and Package Management

+   - **Use Red Hat Package Manager (rpm).** Familiarize yourself with these tasks:
+     - Determine the version of the package and the version of the software it contains, list the files in a package, list documentation files in a package, list configuration files or installation or uninstallation scripts in a package, find out for a certain file from which package it was installed, find out which packages have been installed on the system (all packages, or from a subset of packages), find out in which package a certain program or file can be found.