
# Extracting Data from RPMs

Occasionally you may want to extract data from RPMs without installing the package. For instance, this can be a good way to retrieve the original source code from a source RPM for compiling the software without the help of the RPM tools or to retrieve fonts or other non-program data for use on a non-RPM system.

RPM files are actually modified cpio archives. Thus, converting the files into cpio files is relatively straightforward, whereupon you can use cpio to retrieve the individual files. To do this job, you need to use the rpm2cpio program, which ships with most Linux distributions. (You can use this tool even on distributions that don't use RPM.) This program takes a single argument—the name of the RPM file—and outputs the cpio archive on standard output. So, if you want to create a cpio archive file, you must redirect the output:

```
$ rpm2cpio samba-server-3.0.25b-4.5mdv2008.0.src.rpm
  > samba-server-3.0.25b-4.5mdv2008.0.cpio
```

You can then extract the data using cpio, which takes the -i option to extract an archive and --make-directories to create directories:

```
$ cpio -i --make-directories < samba-server-3.0.25b-4.5mdv2008.0.cpio
```

Alternatively, you can use a pipe to link these two commands together without creating an intermediary file:

```
$ rpm2cpio samba-server-3.0.25b-4.5mdv2008.0.src.rpm | cpio -i
  --make-directories
```

In either case, the result is an extraction of the files in the archive in the current directory. In the case of binary packages, this is likely to be a series of subdirectories that mimic the layout of the Linux root directory—that is, usr, lib, etc, and so on, although precisely which directories are included depends on the package. For a source package, the result of the extraction process is likely to be a source code tarball, a .spec file (which holds information RPM uses to build the package), and perhaps some patch files.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_114_0.png)

When you're extracting data from an RPM file using rpm2cpio and cpio, create a holding subdirectory and then extract the data into this subdirectory. This practice will ensure that you can find all the files. If you extract files in your home directory, some of them may get lost amidst your other files. If you extract files as root in the root (/) directory, they could conceivably overwrite files that you want to keep.

Another option for extracting data from RPMs is to use alien, which is described later, in “Converting Between Package Formats.” This program can convert an RPM into a Debian package or a tarball.

# Using Yum

Yum (http://linux.duke.edu/projects/yum/), mentioned earlier, is one of several meta-packagers — it enables you to easily install a package and all its dependencies using a single command line. When using Yum, you don't even need to locate and download the package files, because Yum does this for you by searching in one or more repositories (Internet sites that host RPM files for a particular distribution).

Yum originated with the fairly obscure Yellow Dog Linux distribution, but it's since been adopted by Red Hat, Fedora, and some other RPM-based distributions. Yum isn't used by all RPM-based distributions, though; SUSE and Mandriva, to name just two, each use their own meta-packagers. Debian-based distributions generally employ the Advanced Package Tools (APT), as described later, in “Using apt-get.” Nonetheless, because of the popularity of Red Hat and Fedora, knowing Yum can be valuable.

The most basic way to use Yum is with the yum command, which has the following syntax:

```
yum [options] [command] [package...]
```

Which options are available depend on the command you use. Table 2.3 describes common yum commands.

## TABLE 2.3 Common yum Commands

| Command | Description |
| --- | --- |
| install | Installs one or more packages by package name. Also installs dependencies of the specified package or packages. |
| update | Updates the specified package or packages to the latest available version. If no packages are specified, yum updates every installed package. |
| check-update | Checks to see whether updates are available. If they are, yum displays their names, versions, and repository area (updates or extras, for instance). |
| upgrade | Works like update with the `--obsoletes` flag set, which handles obsolete packages in a way that's superior when performing a distribution version upgrade. |
| remove or erase | Deletes a package from the system; similar to `rpm -e`, but yum also removes depended-on packages. |
| list | Displays information about a package, such as the installed version and whether an update is available. |
| provides or whatprovides | Displays information about packages that provide a specified program or feature. For instance, typing `yum provides samba` lists all the Samba-related packages, including every available update. Note that the output can be copious. |
| search | Searches package names, summaries, packagers, and descriptions for a specified keyword. This is useful if you don't know a package's name but can think of a word that's likely to appear in one of these fields but not in these fields for other packages. |
| info | Displays information about a package, similar to the `rpm -qi` command. |
| clean | Cleans up the Yum cache directory. Running this command from time to time is advisable, lest downloaded packages chew up too much disk space. |
| shell | Enters the Yum shell mode, in which you can enter multiple Yum commands one after another. |
| resolvedep | Displays packages matching the specified dependency. |
| localinstall | Installs the specified local RPM files, using your Yum repositories to resolve dependencies. |
| localupdate | Updates the system using the specified local RPM files, using your Yum repositories to resolve dependencies. Packages other than those updated by local files and their dependencies are *not updated*. |
| deplist | Displays dependencies of the specified package. |

In most cases, using Yum is easier than using RPM directly to manage packages, because Yum finds the latest available package, downloads it, and installs any required dependencies. Yum has its limits, though; it's only as good as its repositories, so it can't install software that's not stored in those repositories.

> If you use Yum to automatically upgrade all packages on your system, you're effectively giving control of your system to the distribution maintainer. Although Red Hat or other distribution maintainers are unlikely to try to break into your computer in this way, an automatic update with minimal supervision on your part could easily break something on your system, particularly if you've obtained packages from unusual sources in the past.

If you don't want to install the package, but merely want to obtain it, you can use yumdownloader. Type this command followed by the name of a package, and the latest version of the package will be downloaded to the current directory. This can be handy if you need to update a system that's not connected to the Internet; you can use another system that runs the same distribution to obtain the packages and then transfer them to the target system.

If you prefer to use GUI tools rather than command-line tools, you should be aware that GUI front-ends to yum exist. Examples include yumex and kyum. You can use the text-mode yum to install these front-ends, as in yum install kyum. Exercise 2.1 runs you through the process of managing packages using the rpm utility.

# EXERCISE 2.1

## Managing Packages Using RPM

To manage packages using the rpm utility, follow these steps:

1. Log into the Linux system as a normal user.
2. Acquire a package to use for testing purposes. You can try using a package from your distribution that you know you haven't installed; but if you try a random package, you may find it's already installed or has unmet dependencies. This lab uses as an example the installation of zsh-4.3.4-4mdv2008.0.x86_64.rpm, a shell that's not installed by default on most systems, from the Mandriva 2008.0 DVD onto a Mandriva 2008.0 system. You must adjust the commands as necessary if you use another RPM file in your tests.
3. Launch an xterm from the desktop environment's menu system if you used a GUI login.
4. Acquire root privileges. You can do this by typing su in an xterm, by selecting Session → New Root Console from a Konsole window, or by using sudo (if it's configured) to run the commands in the following steps.
5. Type rpm -q zsh to verify that the package isn't currently installed. The system should respond with the message package zsh is not installed.
