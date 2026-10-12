I get the following error message from the `rpm -i` command:

```
package man-1.5m2-6 is already installed
```

To force the `rpm` command to install a package even if errors are present, just add `--force` to the `rpm -i` command, like this:

```
rpm -i --force man-1*
```

# Removing an RPM

You may want to remove — uninstall — a package if you realize you don’t really need the software. For example, if you have installed the X Window System development package but discover you’re not interested in writing X applications, you can easily remove the package by using the `rpm -e` command.

You have to know the name of the package before you can remove it. One good way to find the name is to use `rpm -qa` in conjunction with `grep` to search for the appropriate RPM file. For example, to locate the X Window System development RPM, try the following command:

```
rpm -qa | grep xorg
```

`xorg-x11-devel` happens to be the package name of the X Window System development RPM. To remove that package, type

```
rpm -e xorg-x11-devel
```

To remove an RPM, you don’t need the full RPM filename; all you need is the package name — the first part of the filename up to the dash (-) before the version number.

The `rpm -e` command does not remove a package other packages need. For example, to remove the `vim-common` package, I type the following command:

```
rpm -e vim-common
```

Then I get the following error message:

```
error: Failed dependencies:
    vim-common is needed by (installed) vim-enhanced-6.2.457-1
```

# Upgrading an RPM

Use the `rpm -U` command to upgrade an RPM. You must provide the name of the RPM file that contains the new software. For example, if I have version 2.0.48 of Apache `httpd` (Web server) installed on my system but I want to