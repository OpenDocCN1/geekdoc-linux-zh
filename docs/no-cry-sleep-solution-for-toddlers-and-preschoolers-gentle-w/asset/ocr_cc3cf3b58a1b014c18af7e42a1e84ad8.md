# TABLE 29-5
Query Options for RPM Packages

| Option | Meaning |
|---|---|
| -qpi RPM-file | Displays all package information in the RPM package. |
| -qpl RPM-file | Lists files in the RPM package. |
| -qpd RPM-file | Lists only documentation files in the RPM package. |
| -qpc RPM-file | Lists only configuration files in the RPM package. |
| -qR RPM-file | Lists packages on which this RPM package depends. |

is also installed by another package. To allow a package to overwrite the file installed by another package, you use the --replacefiles option. Many packages depend on the libraries installed by other packages. If these dependent packages are not already installed, you will first have to install them. RPM informs you of the missing dependent files and suggests packages to install. If no packages are suggested, you can use the --redhatprovides option with the missing files to search for needed packages.

The -U option also installs a package if it is not already installed, whereas the -F option will only update installed packages. If the package includes configuration files that will overwrite currently installed configuration files, it will save a copy of each current configuration file in a file ending with .rpmsave, such as /etc/mtools.conf.rpmsave. This preserves any customized configuration changes you may have made to the file. Be sure to also check for configuration compatibilities between the previous and updated versions. If you are trying to install a package that is older than the one already installed, then you need to use the --oldpackages option.

```
# rpm -Uvh mozilla-1.0.1-24.i386.rpm
```

If you are installing from a CD-ROM, you can change to the CD-ROM's RPMS directory, which holds the RPM packages (the RPMS directory may be located within a directory like RedHat on the Red Hat CD-ROM). An ls command lists all the software packages. If you know how the name of a package begins, you should include that with the ls command and an attached *. The list of packages is extensive and does not all fit on one screen. This is helpful for displaying the detailed name of the package. The following example lists most X Window System packages:

```
# ls x*
```

# Installation Example

In the next example, the user first installs a new package with the -i option, and then updates a package with the -U option. Including the -v and -h options is customary. Here, -v is the verbose option that displays all files as they are installed, and -h displays a crosshatch symbol periodically to show RPM is still working. In the following example, the user installs the software package for the Balsa mail client. Notice the full filename is entered. To list the full name, you can use the ls command with the first few characters