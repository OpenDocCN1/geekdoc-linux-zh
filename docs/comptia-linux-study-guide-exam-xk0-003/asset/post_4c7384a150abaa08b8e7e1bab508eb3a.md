
## TABLE 7.4 dpkg Primary Actions *(continued)*

| Action | Description |
| :--- | :--- |
| `-I` or `--info` | Displays information about an uninstalled package file |
| `-l pattern` or `--list pattern` | Lists all installed packages whose names match *pattern* |
| `-L` or `--listfiles` | Lists the installed files associated with a package |
| `-S pattern` or `--search pattern` | Locates the package(s) that own the file(s) specified by *pattern* |
| `-C` or `--audit` | Searches for partially installed packages and suggests what to do with them |

## TABLE 7.5 Options for Fine-Tuning dpkg Actions

| Option | Used with Actions | Description |
| :--- | :--- | :--- |
| `--root=dir` | All | Modifies the Linux system using a root directory located at *dir*. Can be used to maintain one Linux installation discrete from another one, say during OS installation or emergency maintenance. |
| `-B` or `--auto-deconfigure` | `-r` | Disables packages that rely on one that is being removed. |
| `--force=things` | Assorted | Forces specific actions to be taken. Consult the dpkg man page for details of *things* this option does. |
| `--ignore-depends=package` | `-i`, `-r` | Ignores dependency information for the specified package. |
| `--no-act` | `-i`, `-r` | Checks for dependencies, conflicts, and other problems without actually installing or removing the package. |
| `--recursive` | `-i` | Installs all packages that match the package name wildcard in the specified directory and all subdirectories. |
| `-G` | `-i` | Doesn't install the package if a newer version of the same package is already installed. |
| `-E` or `--skip-same-version` | `-i` | Doesn't install the package if the same version of the package is already installed. |

As with rpm, dpkg expects a package name in some cases and a package filename in others. Specifically, --install (-i) and --info (-I) both require the package filename, but the other commands take the shorter package name.

As an example, consider the following command, which installs the samba-common_3.0.28a-1ubuntu4.7_amd64.deb package:

```
# dpkg -i samba-common_3.0.28a-1ubuntu4.7_amd64.deb
```

If you're upgrading a package, you may need to remove an old package before installing the new one. To do this, use the -r option to dpkg:

```
# dpkg -r samba
```

To find information on an installed package, use the -p parameter to dpkg, as shown in Listing 7.2. This listing omits an extended English description of what the package does.

## Listing 7.2: dpkg Package Information Query Output

```
$ dpkg -p samba-common

Package: samba-common

Priority: optional

Section: net

Installed-Size: 7112

Maintainer: Ubuntu Core Developers <ubuntu-devel-discuss@lists.ubuntu.com>

Architecture: amd64

Source: samba

Version: 3.0.28a-1ubuntu4.7

Replaces: samba (<< 3.0.20b-1)

Depends: debconf (>= 0.5) | debconf-2.0, libc6 (>= 2.4), libcomerr2w

(>= 1.33-3), libkrb53 (>= 1.6.dfsg.2), libldap-2.4-2 (>= 2.4.7), libncurses5w

(>= 5.6+20071006+3), libpam-modules, libpopt0 (>= 1.10), libreadline5w

(>= 5.2), libuuid1, ucf

Size: 3058414
```

Debian-based systems often use a somewhat higher-level utility called `dselect` to handle package installation and removal. The `dselect` utility provides a text-mode list of installed packages and packages available from a specified source (such as a CD-ROM drive or an FTP site), and it allows you to select which packages you want to install and remove. This interface can be very useful when you want to install several packages, but `dpkg` is often more convenient when manipulating just one or two packages. Because `dpkg` can take package filenames as input, it’s also the preferred method of installing a package that you download from an unusual source or create yourself.

## Using APT

Advanced Package Tool utilities are another option for Debian package management. These tools center around the `apt-get` utility, which enables you to perform easy upgrades of packages, especially if you have a fast Internet connection. Debian-based systems include a file, `/etc/apt/sources.list`, that specifies locations from which important packages can be obtained. If you installed the OS from a CD-ROM in which packages can be found. There are also likely to be a few lines near the top, commented out with hash marks (`#`), indicating directories on an FTP or Web site from which you can obtain updated packages. (These lines may be uncommented if you did a network install initially.)

![](img/9903a4d3f7abd8dcbef1035fa04a3406_350_0.png)

> Although APT is most strongly associated with Debian systems, a port to RPM-based systems is also available. Check http://apt4rpm.sourceforge.net for information on this port.

The `apt-get` utility works by obtaining information on available packages from the sources listed in `/etc/apt/sources.list` and then using that information to upgrade or install packages. The syntax is similar to that of `dpkg`:

```
apt-get [options] [package-names]
```

Table 7.6 describes the `apt-get` commands, and Table 7.7 describes the most commonly used options. In most cases, you won’t actually *use* any options with `apt-get`, just a single command and possibly one or more package names. One particularly common use of this utility is to keep your system up-to-date with any new packages. The following two commands will accomplish this goal, if `/etc/apt/sources.list` includes pointers to up-to-date file archive FTP sites:

```
# apt-get update
# apt-get dist-upgrade
```

## TABLE 7.6 apt-get Commands

| Command | Description |
| :------- | :----------- |
| `update` | Obtains updated information on packages available from the installation sources listed in `/etc/apt/sources.list`. |
| `upgrade` | Upgrades all installed packages to the newest versions available, based on locally stored information on available packages. |
| `dselect-upgrade` | Performs any changes in package status (installation, removal, etc.) left undone after running `dselect`. |
| `dist-upgrade` | Similar to `upgrade` but performs "smart" conflict resolution to avoid upgrading a package if that would break a dependency. |
| `install` | Installs a package by the package name (not by package filename), obtaining the package from the source that contains the most up-to-date version. |
| `remove` | Removes a specified package by the package name. |
| `source` | Retrieves the newest available source package file by the package filename, using information on available packages and installation archives listed in `/etc/apt/sources.list`. |
| `check` | Checks the package database for consistency and broken package installations. |
| `clean` | Performs housekeeping to help clear out information on retrieved files from the Debian package database. If you don't use `dselect` for package management, run this from time to time in order to save disk space. |
| `autoclean` | Similar to `clean` but removes information only on packages that can no longer be downloaded. |

## TABLE 7.7 Most Useful apt-get Options

| Option | Used with Commands | Description |
| :----- | :----------------- | :--------- |
| `-d` or `--download-only` | `upgrade`, `dselect-upgrade`, `install`, `source` | Downloads package files but does not install them. |
| `-f` or `--fix-broken` | `install`, `remove` | Attempts to fix a system on which dependencies are unsatisfied. |
| `-m`, `--ignore-missing`, or `--fix-missing` | `upgrade`, `dselect-upgrade`, `install`, `remove`, `source` | Ignores all package files that can't be retrieved (because of network errors, missing files, or the like). |
| `-q` or `--quiet` | All | Omits some progress indicator information. May be doubled (for instance, `-qq` to produce still less progress information). |
| `-s`, `--simulate`, `--just-print`, `--dry-run`, `--recon`, or `--no-act` | All | Performs a simulation of the action without actually modifying, installing, or removing files. |
| `-y`, `--yes`, or `--assume-yes` | All | Produces a “yes” response to any yes/no prompt in installation scripts. |
| `-b`, `--compile`, or `--build` | `source` | Compiles a source package after retrieving it. |
| `--no-upgrade` | `install` | Causes `apt-get` to not upgrade a package if an older version is already installed. |

![](img/9903a4d3f7abd8dcbef1035fa04a3406_352_0.png)

> If you use `apt-get` to automatically upgrade all packages on your system, you are effectively giving control of your system to the distribution maintainer. Although Debian or other distribution maintainers are unlikely to try to break into your computer in this way, an automatic update with minimal supervision on your part could easily break something on your system, particularly if you've obtained packages from unusual sources in the past.

A GUI front-end to APT, Synaptic, is available. It presents a list of available packages; or you can use the Search button to narrow the range. When you've found a package you want to install or remove, click the box to the left of its name. When you've made all your selections, click Apply to have Synaptic make the changes. Figure 7.2 shows Synaptic in use. Several additional tools are part of the APT suite, including `apt-key`, `apt-sortpkgs`, and `apt-cache`. Most of these tools are highly technical; however, `apt-cache` has a useful search function, activated by the search keyword, which searches the APT database's names and descriptions. For instance, typing **`apt-cache search samba`** finds all packages that explicitly mention Samba.
