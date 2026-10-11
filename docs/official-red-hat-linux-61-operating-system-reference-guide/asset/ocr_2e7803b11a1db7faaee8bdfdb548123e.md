Since upgrading is really a combination of uninstalling and installing, you can encounter any errors from those modes, plus one more: If RPM thinks you are trying to upgrade to a package with an *older* version number, you will see:

```
```
# rpm -Uvh foo-1.0-1.i386.rpm
foo    package foo-2.0-1 (which is newer) is already installed
error: foo-1.0-1.i386.rpm cannot be installed
#
```
```

To cause RPM to “upgrade” anyway, use `--oldpackage` on the command line:

```
```
# rpm -Uvh --oldpackage foo-1.0-1.i386.rpm
foo    ########################################
#
```
```

# ## 6.2.4 Freshening

Freshening a package is similar to upgrading:

```
```
# rpm -Fvh foo-1.2-1.i386.rpm
foo    ########################################
#
```
```

RPM’s freshen option checks the versions of the packages specified on the command line against the versions of packages that have already been installed on your system. When a newer version of an already-installed package is processed by RPM’s freshen option, it will be upgraded to the newer version. However, RPM’s freshen option will not install a package if no previously-installed package of the same name exists. This differs from RPM’s upgrade option, as an upgrade will install packages, whether or not an older version of the package was already installed.

RPM’s freshen option works well with single packages or with a group of packages. It’s especially handy if you’ve just downloaded a large number of different packages, and you only want to upgrade those packages that are already installed on your system. Using the freshen option means that you won’t have to pick through the downloaded packages, deleting any unwanted ones before using RPM.

In this case, you can simply issue the following command:

```
```
# rpm -Fvh *.rpm
```
```