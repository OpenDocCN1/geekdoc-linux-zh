
The uninstall process can vary slightly from product to product. Some applications or services may include an uninstall script in the files you extract from the tarball. If this is the case, you can execute this script to uninstall the application from your system.

Other products may include an UNINSTALL target in their Makefile file. If this is the case, you must first run configure from the directory created when you originally extracted the downloaded tarball file, just as you did when you first installed the software. Then, instead of running `make install`, you run `make uninstall`. This will cause the make utility to follow the instructions in the uninstall portion of the Makefile file to remove the software from your system. For example, you can use the `make uninstall` command to remove the Pure-FTPd service from the system.

How do you know what method to use? The tarball you downloaded should include a README file of some sort that documents both the install and uninstall processes for the particular software you are working with. Check this file first. If the information isn’t available, then check the FAQ or knowledge base on the web site of the organization that produced the software. One of these resources should provide you with the steps you need to follow to uninstall the software.

It’s time to shift gears and look at managing Debian software packages.

## Managing Debian Software Packages

Not all distributions use RPM to manage software packages. Distributions based on the Debian distribution use the Debian Package Manager (`dpkg`) instead. Ubuntu is probably one of the most popular Debian-based distributions that uses `dpkg` instead of RPM to manage software. Debian packages are similar to RPMs in functionality but are totally different in the way they are implemented.

> **NOTE** Occasionally, I encounter folks who mistakenly think RPM and Debian packages are cross-platform compatible. They are not. You can only install RPM packages on RPM-based systems and Debian packages on Debian-based systems.

In this part of the chapter, we’ll discuss how to manage Debian software packages. The following topics will be addressed:

- Debian package naming
- Installing packages with dpkg
- Viewing package information with apt-cache
- Installing packages with apt-get
- Using aptitude

Let’s begin by looking at the naming convention used by Debian packages.

### Debian Package Naming

Debian packages use a naming convention that is similar to that used by RPM packages. The syntax is as follows:

```
packagename_version_architecture.deb
```

For example: `3dchess_0.8.1-16_i386.deb`.

Here’s a breakdown of how to interpret Debian package filenames:

- **packagename**: Like an RPM package name, this simply provides the name of the package. In the example here, the name of the application in the package is `3dchess`.
- **version**: Specifies the version number of the package. In this example, it is `0.8.1-16`.
- **architecture**: Specifies the hardware architecture the package will run on. In the example here, `i386` indicates the package will run on Intel 80386 or later CPUs.

Like RPM packages, Debian packages include dependency information. Before a given package can be installed, all of the other packages it is dependent upon must be installed first.

> **TIP** You can download a wealth of Debian packages from [http://packages.debian.org](http://packages.debian.org).

With this in mind, let’s discuss how you go about installing Debian packages.

### Installing Packages with dpkg

As with RPM packages, you have two options on most distributions for installing Debian packages. The first is to use a nice graphical utility. For example, on Ubuntu you can use the Ubuntu Software Center by selecting Applications | Ubuntu Software Center. This utility allows you to use a GUI menu system to manage your Debian packages, as shown in Figure 8-11.

Just like the RPM graphical utilities we looked at earlier, the Ubuntu Software Center allows you to install new packages, remove installed packages, and update installed packages. It downloads packages from its configured repositories. It also automatically calculates package dependencies and installs them for you.

However, as nice as these graphical package management utilities may be, they aren’t covered on the LPIC-1/CompTIA Linux+ exam. To pass this exam, you have to know how to manage packages using command-line tools.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_349_0.png)

**Figure 8-11 Using the Ubuntu Software Center to install packages**

The key command-line utility used to manage Debian packages is `dpkg`. The syntax for using `dpkg` is:

```
dpkg options action package_name or package_filename
```

You can use the actions and options listed in Tables 8-3 and 8-4 with the `dpkg` command.

**Table 8-3 dpkg Command Actions**

| Action | Description |
| :--- | :--- |
| `-i` | Installs the specified package. |
| `-r` | Uninstalls the specified package but does not delete its configuration files. |
| `-P` | Uninstalls the specified package and deletes all of its configuration files. |
| `--configure` | Reconfigures the specified package (can also be done with `dpkg-reconfigure`). |
| `-p` | Displays information about the specified package. The package must already be installed. |
| `-I` | Displays information about a package that isn't currently installed on the system. |
| `-l` | Lists all installed packages on the system. |
| `-L` | Lists all files that were installed by the specified package on the system. |
| `-S filename` | Identifies the package that installed the specified file. |

**Table 8-4 dpkg Command Options**

| Option | Associated Action | Description |
| :--- | :--- | :--- |
| `-B` | `-r` | When uninstalling a package that other packages are dependent upon, this option disables those packages. |
| `-G` | `-i` | This option tells `dpkg` not to install the specified package if a newer version of the same package is already installed. |
| `-E` | `-i` | This option tells `dpkg` to not install the specified package if the same version of that package is already installed. |
| `-ignore` | `-i` or `-r` | This option causes `dpkg` to ignore dependency information when installing or removing a package. |
| `-no-act` | `-i` or `-r` | This option tells `dpkg` to check for problems, such as unresolved dependencies, when installing or removing a package. |
| `-recursive` | `-i` | This option allows you to install multiple packages at once using `*` in the package filename part of the command. All matching packages in the current directory as well as subdirectories will be installed. |

For example, if you downloaded a package named `3dchess_0.8.1-16_i386.deb` and wanted to install it, you would first use the `cd` command at the shell prompt to change to the directory where the file resides. Then, as root, you would enter `dpkg -i 3dchess_0.8.1-16_i386.deb` at the shell prompt, as shown in this example:

```
rtracy@Ubuntu-Desktop:~$ su -
Password:
root@Ubuntu-Desktop:~# cd /home/rtracy/Downloads
root@Ubuntu-Desktop:/home/rtracy/Downloads$ ls
3dchess_0.8.1-16_i386.deb
root@Ubuntu-Desktop:/home/rtracy/Downloads# dpkg -i 3dchess_0.8.1-16_i386.deb
(Reading database ... 138218 files and directories currently installed.)
Unpacking 3dchess (from 3dchess_0.8.1-16_i386.deb) ...
Setting up 3dchess (0.8.1-16) ...

Processing triggers for desktop-file-utils ...
Processing triggers for man-db ...
root@Ubuntu-Desktop:/home/rtracy/Downloads$
```

Notice in this command that I had to enter the full filename of the package because it wasn't installed yet. After the package has been installed, you can refer to it by just the package name. For example, to view information about the 3dchess package we just installed, you would enter `dpkg -p 3dchess`, as shown in this example:

```
root@Ubuntu-Desktop:/home/rtracy/Downloads$ dpkg -p 3dchess
Package: 3dchess
Priority: optional
Section: games
Installed-Size: 144
Maintainer: Debian Games Team <pkg-games-devel@lists.alioth.debian.org>
Architecture: i386
Version: 0.8.1-6
Depends: libc6 (>= 2.7-1), libx11-6, libxext6, libxmu6, libxpm4, libxt6, xaw3dg
(>= 1.5+R-1)
Size: 34932
Description: 3D Chess for X11
 3 dimensional chess game for Xl1R6. There are three boards, stacked
 vertically. 96 pieces of which most are the traditional chess pieces with
 just a couple of additions; 26 possible directions in which to move. The
 AI isn't wonderful, but provides a challenging enough game to all but the
 most highly skilled players.
```

Likewise, you could uninstall the 3dchess package using the `dpkg -r 3dchess` command, as shown here:

```
root@Ubuntu-Desktop:/home/rtracy/Downloads# dpkg -r 3dchess
(Reading database ... 138218 files and directories currently installed.)
Removing 3dchess ...
Processing triggers for man-db ...
Processing triggers for desktop-file-utils ...
root@Ubuntu-Desktop:/home/rtracy/Downloads#
```

Now that you know how to manage packages with `dpkg`, let's next look at the `apt-cache` command.

### Viewing Package Information with apt-cache

In addition to `dpkg`, you can also use several apt (Advanced Package Tool) tools to manage packages on a Debian-based system. The first apt tool that you need to be familiar with is `apt-cache`. This command is comparable to the `rpm -q` command in that it is used to query package information from the Debian package database (called the *package cache*). Common `apt-cache` commands are shown in Table 8-5.

**Table 8-5 Common apt-cache Commands**

| Common apt-cache Command | Description |
| :--- | :--- |
| `apt-cache showpkg package_name` or `apt-cache show package_name` | Displays information about the package. |
| `apt-cache stats` | Displays the number of packages installed, dependency information, and other package cache statistics. |
| `apt-cache unmet` | Reports any missing dependencies in the package cache. |
| `apt-cache depends package_name` | Displays all of the package's dependencies. |
| `apt-cache pkgnames package_name` | Checks to see whether a package is installed on the system or not. Leaving out the package name displays a list of all of the packages installed on the system. |
| `apt-cache search keyword` | Searches package descriptions for the specified keyword. |
