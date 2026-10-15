
![](img/6c226e8ba1efd427dec3bf582418d33f_89_0.png)

## FIGURE 4-5 redhat-config-packages

To uninstall a package, first click the Remove Software icon on the bar displayed to the left of the Package panel. In the Group view, installed groups will be displayed with a Remove link at the end. To uninstall packages from a group, click the Remove link. This displays a list of installed packages with a checked check box next to each one. Deselect the ones you want to remove and leave selected the ones you want to keep. When you have finished making your selections, click Remove Packages to queue the packages for removal. Click Continue to perform the removal. In the Package view, all installed packages are listed and you simply select the ones you want removed.

You can also install a particular RPM package directly. You can use this method to install RPM packages you have downloaded or individual packages on your distribution CD-ROM. First display it with the file manager, and then double-click the RPM package file. You can also right-click it and, on GNOME, select Open With and then Install Packages, or on KDE, select Install Package. This invokes the redhat-config-packages tool, which will install the package. It will also check for dependent packages and install those. For packages that are part of your Red Hat distribution, it will prompt you to insert any other CD-ROMs as needed (for the DVD-ROM included with this book, there will be no prompt, as it already holds all packages).

## Installing Packages with the rpm Command

If you do not have access to the desktop or you prefer to work from the command line interface, you can use the rpm command to manage and install software packages. This is the command that performs installation, removal, and verification of software packages.

Each software package is actually an RPM package, consisting of an archive of software files and information about how to install those files. Each archive resides as a single file with a name that ends with .rpm, indicating it is a software package that can be installed by the Red Hat Package Manager.

You can use the rpm command to either install or uninstall a package. The rpm command uses a set of options to determine what action to take. The -i option installs the specified software package, and the -U option updates a package. With an -e option, rpm uninstalls the package. A q placed before an i (-qi) queries the system to see if a software package is already installed and displays information about the software (-qpi queries an uninstalled package file). The rpm command with no options provides a complete list of rpm options.

A set of commonly used options is shown here:

| Option | Action |
| --- | --- |
| -U | Updates package |
| -i | Installs package |
| -e | Removes package |
| -qi | Displays information for an installed package |
| -ql | Displays file list for installed package |
| -qpi | Displays information from an RPM package file (used for uninstalled packages) |
| -qpl | Displays file list from an RPM package file (used for uninstalled packages) |
| -K | Authenticates and performs integrity check on a package |

The software package name is usually quite lengthy, including information about the version and release date in its name. All end with .rpm. In the next example, the user installs the freeciv package using the rpm command. Notice that the full filename is entered. To list the full name, you can use the ls command with the first few characters and an asterisk:

```
ls freeciv*
```

You can also use the * to match the remainder of the name, as in the following:

```
ls freeciv-1*.rpm
```

In most cases, you are installing packages with the -U option, for update. Even if the package is not already installed, -U still installs it.

```
$ rpm -Uvh freeciv-1.14.0-2.i386.rpm
```

When RPM performs an installation, it first checks for any dependent packages. These are other software packages with programs the application you are installing needs to use.
