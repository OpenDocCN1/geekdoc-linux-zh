
## TABLE 7.6 apt-get Commands

| Command | Description |
| :---- | :---- |
| update | Obtains updated information on packages available from the installation sources listed in `/etc/apt/sources.list`. |
| upgrade | Upgrades all installed packages to the newest versions available, based on locally stored information on available packages. |
| dselect-upgrade | Performs any changes in package status (installation, removal, etc.) left undone after running `dselect`. |
| dist-upgrade | Similar to `upgrade` but performs “smart” conflict resolution to avoid upgrading a package if that would break a dependency. |
| install | Installs a package by the package name (not by package filename), obtaining the package from the source that contains the most up-to-date version. |
| remove | Removes a specified package by the package name. |
| source | Retrieves the newest available source package file by the package filename, using information on available packages and installation archives listed in `/etc/apt/sources.list`. |
| check | Checks the package database for consistency and broken package installations. |
| clean | Performs housekeeping to help clear out information on retrieved files from the Debian package database. If you don’t use `dselect` for package management, run this from time to time in order to save disk space. |
| autoclean | Similar to `clean` but removes information only on packages that can no longer be downloaded. |

## TABLE 7.7 Most Useful apt-get Options

| Option | Used with Commands | Description |
| :---- | :---- | :---- |
| -d or --download-only | `upgrade`, `dselect-upgrade`, `install`, `source` | Downloads package files but does not install them. |
| -f or --fix-broken | `install`, `remove` | Attempts to fix a system on which dependencies are unsatisfied. |
| -m, --ignore-missing, or --fix-missing | `upgrade`, `dselect-upgrade`, `install`, `remove`, `source` | Ignores all package files that can't be retrieved (because of network errors, missing files, or the like). |
| -q or --quiet | All | Omits some progress indicator information. May be doubled (for instance, -qq) to produce still less progress information. |
| -s, --simulate, --just-print, --dry-run, --recon, or --no-act | All | Performs a simulation of the action without actually modifying, installing, or removing files. |
| -y, --yes, or --assume-yes | All | Produces a "yes" response to any yes/no prompt in installation scripts. |
| -b, --compile, or --build | `source` | Compiles a source package after retrieving it. |
| --no-upgrade | `install` | Causes apt-get to not upgrade a package if an older version is already installed. |

> **WARNING** If you use apt-get to automatically upgrade all packages on your system, you are effectively giving control of your system to the distribution maintainer. Although Debian or other distribution maintainers are unlikely to try to break into your computer in this way, an automatic update with minimal supervision on your part could easily break something on your system, particularly if you've obtained packages from unusual sources in the past.

A GUI front-end to APT, Synaptic, is available. It presents a list of available packages; or you can use the Search button to narrow the range. When you've found a package you want to install or remove, click the box to the left of its name. When you've made all your selections, click Apply to have Synaptic make the changes. Figure 7.2 shows Synaptic in use.

Several additional tools are part of the APT suite, including **apt-key**, **apt-sortpkgs**, and **apt-cache**. Most of these tools are highly technical; however, **apt-cache** has a useful search function, activated by the search keyword, which searches the APT database's names and descriptions. For instance, typing **apt-cache search samba** finds all packages that explicitly mention Samba.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_353_0.png)

## Handling Tarballs

All distributions can use tarballs—files collected together with the tar utility and typically compressed with `compress`, `gzip`, or `bzip2`. Like RPM and Debian packages, tarballs may contain source code, binary files, or architecture-independent files such as documentation or fonts. These files lack dependency information, however, and tar maintains no database of installed files. Therefore, it's harder to remove programs installed via tarballs than it is to remove RPM or Debian packages. Slackware, though, maintains a database of files installed via Slackware's tarballs and the Slackware `pkgtool` utility.

### The Role of tar and Tarballs

A multipurpose tool, tar was originally created for archiving files to tape—the name stands for “tape archiver.” (The upcoming section “Backing Up and Restoring a Computer” describes this role of tar in more detail.) Because Unix, and hence Linux, treats hardware devices as files, a tape-archiving program like tar can be used to create archives as files on disk. These files can then be compressed, copied to floppy disk or other removable media, sent over a network, and so on.

In the Linux world, tarballs fill a role that’s similar to that of *zip* files in the Windows world. There are differences, however: *Zip* utilities (including the *zip* and *unzip* commands in Linux) compress files and then add them to the archive. By contrast, *tar* does not directly support compression, so to compress files, the resulting archive is compressed with a second utility, such as *gzip*, *bzip2*, or *compress*. The *gzip* and *bzip2* programs are the most popular on Linux systems, although *compress* is still used on some older Unix systems. (The *gzip* utility can uncompress old *compress* archives.) The resulting file may have two extensions (such as *.tar.gz* or *.tar.bz2*), but that extension may be combined into a single, three-character extension (*.tgz* or *.tbz*) for easy storage on filesystems (like DOS’s FAT) that don’t support longer or multiple extensions. The older *compress* archives used an uppercase Z extension, so these tarballs have *.tar.Z* extensions.

Considered as a package distribution mechanism, tarballs are used primarily by the Slackware distribution, which is the oldest of the major Linux distributions still in common use. Slackware eschews flashy configuration tools in favor of a bare-bones approach. In this respect, Slackware resembles Debian, but Slackware uses custom extensions to *tar* as a way of tracking package installations. As noted earlier, Debian also uses source tarballs as part of its source package management system, but most administrators don’t need to be concerned with this detail.

Although most other distributions don’t rely on tarballs, they can be used with any distribution. Tarballs are particularly likely to be useful when you’re faced with the task of compiling a program from source code, and especially if you must modify that source code for your system. The upcoming section “Compiling Source Code” describes how to compile software delivered as source code in a tarball.

Binary tarballs contain precompiled programs. Sometimes the tarball contains the program files in a form that enables you to expand the tarball directly into a target directory. For instance, you could change to the /usr/local directory and uncompress the tarball to have the program files dropped directly into /usr/local/bin, /usr/local/man, and so on. Other times you may need to uncompress the tarball in a temporary directory and then run an installation utility to install the software.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_354_0.png)

## Using tar Commands

The *tar* program is a complex package with many options. Most of what you’ll do with the utility, however, can be covered with a few common commands. Table 7.8 describes the primary *tar* commands, and Table 7.9 describes the qualifiers for these commands that modify what the command does. Whenever you run *tar*, you use exactly one command, and you usually use at least one qualifier.
