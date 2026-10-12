![](bbox=[0.175, 0.148, 0.295, 0.225])

You do not have to type the full RPM filename — you can use a few characters from the beginning of the name followed by an asterisk. Make sure that you type enough of the name to uniquely identify the RPM file.

If you try to install an already installed RPM, the rpm command displays an error message. For example, here is what happens when I try to install the Emacs editor on my system:

```
rpm -i emacs-20*
package emacs-20.7-13 is already installed
```

To force the rpm command to install a package even if there are errors, just add --force to the rpm -i command as follows:

```
rpm -i --force emacs-20*
```

# Removing RPMs with the rpm command

You can remove — uninstall — a package if you realize that you don’t really need the software. For example, if you install the X Window System development package, but you are not interested in writing any X applications, you can easily remove the package by using the rpm -e command.

You need the name of the package before you can remove it. One good way to find the name is to use rpm -qa in conjunction with grep to search for the appropriate RPM file. For example, to locate the X Window System development RPM, you can try this:

```
rpm -qa | grep XFree
XFree86-75dpi-fonts-4.0.1-0.43
XFree86-twm-4.0.1-0.43
XFree86-libs-4.0.1-0.43
XFree86-xfs-4.0.1-0.43
XFree86-4.0.1-0.43
XFree86-devel-4.0.1-0.43
XFree86-tools-4.0.1-0.43
XFree86-xdm-4.0.1-0.43
XFree86-SVGA-3.3.6-32
```

In this case, XFree86-devel is the package name you need. To remove the package, type:

```
rpm -e XFree86-devel
```