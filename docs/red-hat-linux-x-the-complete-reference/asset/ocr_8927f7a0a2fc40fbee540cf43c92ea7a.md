You can use the `rpm` command to either install or uninstall a package. The `rpm` command uses a set of options to determine what action to take. The `-i` option installs the specified software package, and the `-U` option updates a package. With an `-e` option, `rpm` uninstalls the package. A `q` placed before an `i` (`-qi`) queries the system to see if a software package is already installed and displays information about the software (`-qpi` queries an uninstalled package file). The `rpm` command with no options provides a complete list of `rpm` options. A set of commonly used options is shown here:

| Option | Action |
|---|---|
| -U | Updates package |
| -i | Installs package |
| -e | Removes package |
| -qi | Displays information for an installed package |
| -ql | Displays file list for installed package |
| -qpi | Displays information from an RPM package file (used for uninstalled packages) |
| -qpl | Displays file list from an RPM package file (used for uninstalled packages) |
| -K | Authenticates and performs integrity check on a package |

The software package name is usually quite lengthy, including information about the version and release date in its name. All end with `.rpm`. In the next example, the user installs the freeciv package using the `rpm` command. Notice that the full filename is entered. To list the full name, you can use the `ls` command with the first few characters and an asterisk:

```
ls freeciv*
```

You can also use the * to match the remainder of the name, as in the following:

```
ls freeciv-1*.rpm
```

In most cases, you are installing packages with the `-U` option, for update. Even if the package is not already installed, `-U` still installs it.

```
$ rpm -Uvh freeciv-1.14.0-2.i386.rpm
```

When RPM performs an installation, it first checks for any dependent packages. These are other software packages with programs the application you are installing needs to use. If other dependent packages must be installed first, RPM cancels the installation and lists those packages. You can install those packages and then repeat the installation of the application. To determine if a package is already installed, use the `-qi` option with `rpm`. The `-q` stands for query. To obtain a list of all the files the package has installed, as well as the directories it installed to, use the `-ql` option. To query package files, add the `p` option. The `-qpi` option displays information about a package, and `-qpl` lists the files in it. The following example lists all the files in the freeciv package:

```
$ rpm -qpl freeciv-1.14.0-2.i386.rpm
```

To remove a software package from your system, first use `rpm -qi` to make sure it is actually installed, and then use the `-e` option to uninstall it. As with the `-qi` option, you needn't use the full name of the installed file. You only need the name of the application. In the next example, the user removes the freeciv game from the system:

```
$ rpm -e freeciv
```

# Package Security Check

If you download an RPM package, you may want to check its integrity and authentication, making sure the package was not tampered with and that it was obtained from a valid source. To just check a package's