![](bbox=[0.14, 0.17, 0.24, 0.28])

You don't have to type the full RPM filename — you can use a few characters from the beginning of the name followed by an asterisk (*). Make sure you type enough of the name to identify the RPM file uniquely.

If you try to install an RPM that's already installed, the rpm -i command displays an error message. For example, here is what happens when I type the following command to install the man package on my system:

```
rpm -i man-1*
```

I get the following error message from the rpm -i command:

```
package man-1.5k-8 is already installed
```

To force the rpm command to install a package even if errors are present, just add --force to the rpm -i command, like this:

```
rpm -i --force man-1*
```

# Removing an RPM

You may want to remove — uninstall — a package if you realize you don't really need the software. For example, if you have installed the X Window System development package but discover you're not interested in writing X applications, you can easily remove the package by using the rpm -e command.

You have to know the name of the package before you can remove it. One good way to find the name is to use rpm -qa in conjunction with grep to search for the appropriate RPM file. For example, to locate the X Window System development RPM, try the following command:

```
rpm -qa | grep XFree86
```

XFree86-devel happens to be the package name of the X Window System development RPM. To remove that package, type

```
rpm -e XFree86-devel
```

To remove an RPM, you don't need the full RPM filename; all you need is the package name — the first part of the filename up to the dash (-) before the version number.

The rpm -e command does not remove a package other packages need. For example, to remove the vim-common package, type the following command:

```
rpm -e vim-common
```