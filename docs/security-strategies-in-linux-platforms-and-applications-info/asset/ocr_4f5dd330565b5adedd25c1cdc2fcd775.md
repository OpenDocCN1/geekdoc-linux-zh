# PART 3 | Building a Layered Linux Security Strategy

| TABLE 11-2 Standard apt-* commands. |
| COMMAND | DESCRIPTION |
| apt-cdrom | Includes CD/DVDs (or appropriately mounted ISO files) for updates |
| apt-file | Searches for files within uninstalled packages |
| apt-ftarchive | Generates a package archive from a list of packages in a directory; used for creating key files on a local repository |
| apt-get | Installs, updates, removes, and purges packages with dependencies |

# Various apt-* Commands

* apt-* commands are a series of commands developed for Debian Linux. These commands can be used to install, remove, or provide additional information about packages available from distribution-specific repositories. Standard apt-* commands are summarized in Table 11-2.

The apt command works as a front-end to many apt-* commands. In addition, the apt command, when run by itself, opens a console-based configuration tool for Debian-style packages, including those found on Ubuntu systems.

# Various Yum Commands

You can use the yum command to pull updates on Red Hat-style systems, including Red Hat Enterprise Linux, Fedora Linux, and CentOS Linux. The yum command is rich and diverse; this section addresses just a few basic options for the yum command. For full list, run the yum command by itself. Figure 11-2 illustrates the basic options available for yum.

Here are some basic examples of the yum command. To install a new package samba, you'd run the following command:

```
# yum install samba
```

If the Server package is already installed and an upgraded version is available, the preceding command updates the package with any dependencies. Alternatively, the following command updates the Samba package if it is already installed:

```
# yum update samba
```

If you're interested in installing a new kernel package, avoid the update option. The install option preserves the installation of any existing kernel side by side with any updated kernel.