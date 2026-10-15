
## TABLE 29-5
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

## Installation Example

In the next example, the user first installs a new package with the -i option, and then updates a package with the -U option. Including the -v and -h options is customary. Here, -v is the verbose option that displays all files as they are installed, and -h displays a crosshatch symbol periodically to show RPM is still working. In the following example, the user installs the software package for the Balsa mail client. Notice the full filename is entered. To list the full name, you can use the ls command with the first few characters

and an asterisk, ls balsa*. The rpm command with the -q option is then used to check that the software was installed. For installed packages only, the software name needs to be used—in this case, balsa-1.2.4-7.

```
[root@turtle mypackages]# ls balsa*
balsa-1.2.4-7.i386.rpm
[root@turtle mypackages]# rpm -ivh balsa-1.2.4-7.i386.rpm
balsa-1.2.4-7
[root@turtle mypackages]# rpm -q balsa
balsa-1.2.4-7
```

To display information about the installed package, use -qi, and -ql displays a listing of the files a given RPM package contains.

```
# rpm -qi balsa
# rpm -ql balsa
```

If you are worried that a software package will install on your system incorrectly, you can use the test option (-test) in the debug mode (vv) to see exactly what actions RPM will take.

```
# rpm -ivv --test balsa-1.2.4-7.i386.rpm
```

## Removing RPM Software Packages

To remove a software package from your system, first use rpm -q to make sure it is actually installed. Then use the -e option to uninstall it. You needn't use the full name of the installed file. You only need the name of the application. For example, if you decide you do not need Balsa, you can remove it using the -e option and the software name, as shown here:

```
# rpm -e balsa
```

## Verifying an RPM Installation

You can use the verify option (-V) to see if any problems occurred with the installation. RPM compares the current attributes of installed files with information about them placed in the RPM database when the package was installed. If no discrepancies exist, RPM outputs nothing. Otherwise, RPM outputs a sequence of eight characters, one for each attribute, for each file in the package that fails. Those that do not differ have a period. Those that do differ have a corresponding character code, as shown in Table 29-6. The following example verifies the ProFTPD package:

```
[root@turtle mypackages]# rpm -V proftpd
```

To compare the installed files directly with the files in an RPM package file, you use the -Vp option, much like the -qp option. To check all packages, use the -Va option as shown here:

```
# rpm -Va
```
