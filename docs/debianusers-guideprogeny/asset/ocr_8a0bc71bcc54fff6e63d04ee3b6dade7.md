# The apt-cdrom Command (Sets Sources)

| Option | Action | Comment |
| :--- | :--- | :--- |
| `-OPTION=no` | Over rides a setting in the configuration file. | The configuration file is `/etc/apt/apt.conf`. |
| `▼ -r` | Gives a CD a new label. | You are prompted for the new label. |
| `▼ --rename` | | |


# Managing Packages With the dpkg Command

The dpkg command for package management. Although dpkg can be used to install a package, its real strength is its ability to retrieve information about package on your system. It is especially useful if you need to search packages or their contents, or for building packages.

For information about building packages, see the on-line help for dpkg and dpkg-deb. Most of the functions of dpkg-deb can be had using the actions defined for dpkg.

Type: dpkg OPTIONS ARGUMENT ACTION PACKAGE.