# Installing RPMs with the rpm command

To install an RPM, you have to use the rpm -i command. You must provide the name of the RPM file as the argument. A typical example is to install one from this book’s companion CD-ROM containing the Red Hat Linux RPMs. As usual, you have to first mount the CD-ROM and then change to the directory in which the RPMs are located. Then, use the rpm -i command to install the RPM followed by the name of the RPM.

For example, to install the kernel-source RPM (which contains the source files for the Linux operating system) from the CD-ROM, you’d type the following commands:

```
```
mount /mnt/cdrom
cd /mnt/cdrom/RedHat/RPMS
rpm -i kernel-source*
```
```

![](bbox=[0.12, 0.37, 0.2, 0.43])

You do not have to type the full RPM filename; you can use a few characters from the beginning of the name followed by an asterisk (*). Make sure that you type enough of the name to identify uniquely the RPM file or files you want to install.

If you try to install an already installed RPM, the rpm command displays an error message such as the following, which results after trying to install the Emacs editor on a sample system:

```
```
rpm -i emacs-20*
package emacs-20.7-34 is already installed
```
```

To force the rpm command to install a package even if there are errors, just add --force to the rpm -i command as follows:

```
```
rpm -i --force emacs-20*
```
```

If you combine the v option with -i, the rpm command will display a little more information about what rpm is doing while it is installing an RPM. If you use the h option, the rpm command will print hash marks (#) to show its progress while installing an RPM. Here’s how an RPM installation looks if you combine the v and h options with -i when installing the zsh RPM:

```
```
rpm -ivh zsh-3.0.8-8.i386.rpm
Preparing...                          ###########################################
[100%]
1:zsh                                    ###########################################
[100%]
```
```

# Removing RPMs with the rpm command

You can remove, or uninstall, a package if you realize that you don’t really need the software, or if it is causing problems for your system. For example, if you install the X Window System development package, but are not interested in writing any X applications, you can remove the package easily by using the rpm -e command.