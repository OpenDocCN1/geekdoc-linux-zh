Don't add a site to /etc/apt/sources.list unless you're sure it can be trusted. The apt-get utility does automatic and semiautomatic upgrades, so if you add a network source to sources.list and that source contains unreliable programs or programs with security holes, your system will become vulnerable after upgrading via apt-get.

The apt-get utility works by obtaining information about available packages from the sources listed in /etc/apt/sources.list and then using that information to upgrade or install packages. The syntax is similar to that of dpkg:

```
apt-get [options][command] [package-names]
```

Table 2.6 lists the apt-get commands, and Table 2.7 lists the most commonly used options. In most cases, you won't use any options with apt-get—just a single command and possibly one or more package names. One particularly common use of this utility is to keep your system up to date with any new packages. The following two commands will accomplish this goal if /etc/apt/sources.list includes pointers to up-to-date file archive sites:

```
# apt-get update
# apt-get dist-upgrade
```

TABLE 2.6 apt-get Commands
| Command | Description |
| :--- | :--- |
| update | Obtains updated information about packages available from the installation sources listed in /etc/apt/sources.list. |
| upgrade | Upgrades all installed packages to the newest versions available, based on locally stored information about available packages. |
| dselect-upgrade | Performs any changes in package status (installation, removal, and so on) left undone after running dselect. |
| dist-upgrade | Similar to upgrade, but performs "smart" conflict resolution to avoid upgrading a package if doing so would break a dependency. |
| install | Installs a package by package name (not by package filename), obtaining the package from the source that contains the most up-to-date version. |
| remove | Removes a specified package by package name. |
| source | Retrieves the newest available source package file by package file-name using information about available packages and installation archives listed in /etc/apt/sources.list. |