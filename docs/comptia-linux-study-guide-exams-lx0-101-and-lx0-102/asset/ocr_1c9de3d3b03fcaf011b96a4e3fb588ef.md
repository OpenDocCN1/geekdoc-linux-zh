# Chapter 2 • Managing Software

list directories on the installation CD-ROM in which packages can be found. There are also likely to be a few lines near the top, commented out with hash marks (#), indicating directories on an FTP site or a Web site from which you can obtain updated packages. (These lines may be uncommented if you did a network install initially.)

![](bbox=[0.137, 0.215, 0.226, 0.258])

> Don't add a site to /etc/apt/sources unless you're sure it can be trusted. The apt-get utility does automatic and semiautomatic upgrades, if you add a network source to sources.list and that source contains unreliable programs or programs with security holes, your system will become vulnerable after upgrading apt-get.

APT is most strongly associated with Debian systems, a port to RPM-based systems is also available. Check http://apt4rpm.sourceforge.net for information about this port.
apt-get works by obtaining information about available packages from the sources listed in /etc/apt/sources.list and then using that information to upgrade or install packages. The syntax is similar to that of dpkg:

```
apt-get [options][command] [package-names]
```

Table 2.6 lists the apt-get commands, and Table 2.7 lists the most commonly used options. In most cases, you won't use any apt-get—just a single command and possibly one or more package names. One common use of this utility is to keep your system up to date with new packages. The following two commands will accomplish this goal if /etc/apt/sources.list includes pointers to up-to-date file archive sites:

```
# apt-get update
# apt-get dist-upgrade
```

# TABLE 2.6 apt-get commands

| Command | Description |
|---|---|
| update | Obtains updated information about available packages from the installation sources listed in /etc/apt/sources.list |
| upgrade | Upgrades all installed packages to the newest versions available, based on locally stored information about available packages. |
| dselect-upgrade | Performs any changes in package status (installation, removal, and so on) left undone after running dselect. |