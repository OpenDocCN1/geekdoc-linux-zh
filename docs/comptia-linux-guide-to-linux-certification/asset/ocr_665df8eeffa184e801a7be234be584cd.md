| Option | Description |
|---|---|
| -a -all | Displays all package names installed on the system (when used with the -q option) |
| -c -configfiles | Displays the locations of the configuration files for a package installed on the system (when used with the -q option) |
| --dump | Displays detailed information regarding configuration files for a package installed on the system (when used following the -q and -c options) |
| -e -erase | Removes a specified package from the system |
| -F -fresen | Upgrades a specified package only if an older version exists on the system |
| -f -file | Displays the package to which the specified file belongs (when used with the -q option) |
| -h -hash | Prints hash marks on the screen to indicate installation progress (when used with the -i option) |
| -i -install | Installs a specified package (provided the -q option is not used) |
| -i -info | Displays full information about the specified package (when used with the -q option) |
| -K -list | When used before a filename argument, validates the checksum listed within the RPM file Lists the filenames the specified package comprises (when used with the -q option) |
| --nodeps | Forces the RPM to avoid checking for dependencies before installing packages (when used following the -i option) |
| -q -query | Queries information about packages on the system |
| --test | Performs a test installation only (when used with the -i option) |
| -U -upgrade | Upgrades a specified package; the package is installed even if no older version exists on the system |
| -V -verify | Verifies the location of all files that belong to the specified package |
| -v | Prints verbose information when installing or manipulating packages |

Table 11-8 Common options used with the rpm command

Fedora 20 installation, files are added to the /etc/ yum/repos.d directory that list standard software repositories on the Internet that contain RPM packages. Thus, if you forgot to choose a particular RPM package during the Fedora installation, you can easily install it afterwards using the yum install package_name command.

![](bbox=[0.12, 0.87, 0.28, 0.96])

You used the yum command discussed in previous chapters to install several different programs on your Fedora 20 virtual machine from software repositories on the Internet.