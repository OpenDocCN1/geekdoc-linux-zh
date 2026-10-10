
Linux LVM environment. Be sure to consult their man pages for additional details.

> **TIP**
>
> **To see all the various LVM commands available, type `lvm help` at the CLI and press Enter.**

Using the various command-line programs we covered, you have full control over your Linux LVM environment. And you gain the added flexibility LVM provides.

## Summary

Working with storage devices in Linux requires that you know a bit about filesystems. Knowing how to create and work with filesystems from the command line can come in handy as you work on Linux systems. This chapter discussed how to handle filesystems from the Linux command line.

Before you can install a filesystem on a storage device, you must first prepare the drive. The `fdisk`, `gdisk`, and `parted` commands are used to partition storage devices to get them ready for the filesystem. When you partition the storage device, you must define what type of filesystem will be used on it.

After you partition a storage device, you can use one of several filesystems for the partition. Popular Linux filesystems include journaling or volume-managing features, making them less prone to errors and problems.

One limiting factor in creating filesystems directly on a storage device partition is that you can't easily change the size of the filesystem if you run out of disk space. However, Linux supports logical volume management, a method of creating virtual partitions across multiple storage devices, which allows you to easily expand an existing filesystem without having to completely rebuild it.

Now that you've seen the core Linux command-line commands, it's close to the time to start creating some shell script programs. However, before you start coding, we need to discuss another element: installing software. If you plan to write shell scripts, you need an environment in which to create your masterpieces. The next chapter discusses how to install and manage software packages from the command line in different Linux environments.

## CHAPTER 9
### Installing Software

### IN THIS CHAPTER

- **Installing software**
- **Using Debian packages**
- **Working with Red Hat packages**
- **Exploring application containers**
- **Revisiting tarballs**

In the old days of Linux, installing software could be a painful experience. Fortunately, the Linux developers have made life a little easier for us by bundling software into prebuilt packages that are much easier to install. However, there’s still a little work on our part to get the software packages installed, especially if you want to do so from the command line. This chapter takes a look at the various package management systems available in Linux and the command-line tools used for software installation, management, and removal.

## Exploring Package Management

Before diving into the world of Linux software package management, this chapter goes through a few of the basics. Each of the major Linux distributions utilizes some form of package management system to control installing software applications and libraries. A *package management system* uses a database that keeps track of the following:

- What software packages are installed on the Linux system
- What files have been installed for each package
- Versions of each of the software packages installed

Software packages are stored on servers, called *repositories*, and are accessed across the Internet via package management system utilities running on your local Linux system. You can use these utilities to search for new software packages or even updates to software packages already installed on the system.

A software package will often have *dependencies*, or other packages that must be installed first for the software to run properly. The package management system utilities will detect these dependencies and offer to install any additionally needed software packages before installing the desired package.

The downside to a package management system is that there isn’t a single standard utility. Whereas all the Bash shell commands discussed so far in this book will work no matter which Linux distribution you use, this is not true with software package management.

The package management system utilities and their associated commands are vastly different between the various Linux distributions. The two primary package management system base utilities commonly used in the Linux world are *dpkg* and *rpm*.

Debian-based distributions such as Ubuntu and Linux Mint use, at the base of their package management system utilities, the *dpkg* command. This command interacts directly with the package management system on the Linux system and is used for installing, managing, and removing software packages.

The Red Hat–based distributions, such as Fedora, CentOS, and openSUSE, use the *rpm* command at the base of their package management system. Similar to the *dpkg* command, the *rpm* command can list installed packages, install new packages, and remove existing software.

Note that these two commands are the core of their respective package management system, not the entire package management system itself. Many Linux distributions that use the *dpkg* or *rpm* methods have built additional specialty package management system utilities upon these base commands to make your life much easier. The following sections walk through various package management system utility commands you'll run into in the popular Linux distributions.

## Inspecting the Debian-Based Systems

The `dpkg` command is at the core of the Debian-based family of package management system tools. It provides options to install, update, and remove DEB package files on your Linux system.

The `dpkg` command assumes you have the DEB package file either downloaded onto your local Linux system or available as a URL. More often than not, that isn't the case. Usually you'll want to install an application package from the repository for your Linux distribution. To do that, you'll use the Advanced Package Tool (APT) suite of tools:

- `apt-cache`
- `apt-get`
- `apt`

The `apt` command is essentially a front end for both the `apt-cache` and `apt-get` commands. The nice thing about APT is that you don't need to remember which tool to use when—it covers everything you need to do with package management. The basic format for the `apt` command is

```python
apt [options] command
```

The `command` defines the action for `apt` to take. If needed, you can specify one or more `options` to fine-tune what happens. This section looks at how to use the APT command-line tool to work with the software packages on your Linux system.

## Managing packages with apt

A common task faced by Linux system administrators is to determine what packages are already installed on the system. The `apt list` command displays all the packages available in the repository, but by adding the `--installed` option you can limit the output to only those packages already installed on your system:

```bash
$ apt --installed list
Listing... Done
accountsservice/focal, now 0.6.55-0ubuntu11 amd64 [installed, automatic]
acl/focal, now 2.2.53-6 amd64 [installed, automatic]
acpi-support/focal, now 0.143 amd64 [installed, automatic]
acpid/focal, now 1:2.0.32-1ubuntu1 amd64 [installed, automatic]
adduser/focal, focal, now 3.118ubuntu2 all [installed, automatic]
adwaita-icon-theme/focal, focal, now 3.36.0-1ubuntu1 all [installed, automatic]
aisleriot/focal, now 1:3.22.9-1 amd64 [installed, automatic]
alsa-base/focal, focal, now 1.0.25+dfsg-0ubuntu5 all [installed, automatic]
alsa-topology-conf/focal, focal, now 1.2.2-1 all [installed, automatic]
alsa-ucm-conf/focal, focal, now 1.2.2-1 all [installed, automatic]
...
$ 
```

As you can guess, the list of installed packages will be very long, so we've abbreviated the output to show just a sample of what the output looks like. Next to the package name is additional information about the package, such as the version name, and whether the package is installed and flagged for automatic upgrades.

If you already know the packages on your system and want to quickly display detailed information about a particular package, use the `show` command:

```bash
apt show *package_name*
```

Here's an example of displaying the details of the package `zsh`:

```bash
$ apt show zsh
Package: zsh
Version: 5.8-3ubuntu1
Priority: optional
Section: shells
Origin: Ubuntu
Maintainer: Ubuntu Developers <ubuntu-devel- discuss@lists.ubuntu.com>
Original-Maintainer: Debian Zsh Maintainers <pkg-zsh- devel@lists.alioth.debian.org>
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Installed-Size: 2,390 kB
Depends: zsh-common (= 5.8-3ubuntu1), libc6 (>= 2.29), libcap2 (>= 1:2.10), libtinfo6 (>= 6)
```
