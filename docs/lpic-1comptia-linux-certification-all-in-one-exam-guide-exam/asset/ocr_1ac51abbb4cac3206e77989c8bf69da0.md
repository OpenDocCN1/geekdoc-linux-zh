# Installing Packages with apt-get

In addition to apt-cacher, the apt suite of tools also includes the apt-get utility, which is the equivalent of the yum utility on an RPM system. It automatically downloads and installs packages (along with all dependent packages) for you.

The /etc/apt/sources.list file defines the repositories where apt-get can install packages from. As with yum, these repositories can reside on a local optical disc (such as your installation disc), a local hard drive, or a server on the Internet (via the HTTP or FTP protocol). A sample sources.list file is shown here:

```
root@Ubuntu-Desktop:/etc/apt# cat sources.list
#deb cdrom:Ubuntu 9.10 _Karmic Koala_ - Release i386 (20091028.5)/ karmic main restricted
deb http://us.archive.ubuntu.com/ubuntu/ karmic main restricted
deb-src http://us.archive.ubuntu.com/ubuntu/ karmic main restricted
deb http://us.archive.ubuntu.com/ubuntu/ karmic universe
deb-src http://us.archive.ubuntu.com/ubuntu/ karmic universe
deb http://us.archive.ubuntu.com/ubuntu/ karmic-multiverse
deb-src http://us.archive.ubuntu.com/ubuntu/ karmic-multiverse
deb http://us.archive.ubuntu.com/ubuntu/ karmic-updates universe
deb-src http://us.archive.ubuntu.com/ubuntu/ karmic-updates universe
deb http://security.ubuntu.com/ubuntu karmic-security main restricted
deb-src http://security.ubuntu.com/ubuntu karmic-security main restricted
deb http://security.ubuntu.com/ubuntu karmic-security universe
deb-src http://security.ubuntu.com/ubuntu karmic-security universe
deb http://security.ubuntu.com/ubuntu karmic-security multiverse
deb-src http://security.ubuntu.com/ubuntu karmic-security multiverse
```

Package repositories are identified in this file with the prefix deb, while source file repositories are identified with deb-src. After the prefix, the URL to the repository is specified.

The syntax for using apt-get is pretty straightforward:

```
apt-get options command package_name
```

Commonly used apt-get commands and options are listed in Tables 8-6 and 8-7, respectively.

| apt-get Command | Description |
| :------------ | :-------------------------------------------- |
| install | Installs the latest version of a specified package. |
| remove | Removes the specified package. |
| update | Displays updated information about all packages available in your configured package repositories. |
| upgrade | Upgrades all installed packages to the newest version. |
| dist-upgrade | Upgrades all installed packages to the newest version, but avoids upgrading packages if the upgrade would break a dependency. |
| check | Verifies the integrity of installed packages as well as the package database. |
| clean | Removes outdated information from the package database. |