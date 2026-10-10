
Recommends: libgdbm6 (>= 1.16), libncursesw6 (>= 6), libpre3
Suggests: zsh-doc
Homepage: https://www.zsh.org/
Download-Size: 707 kB
APT-Sources: http://us.archive.ubuntu.com/ubuntu focal/main amd64 Packages
Description: shell with lots of features

Zsh is a UNIX command interpreter (shell) usable as an interactive login shell and as a shell script command processor. Of the standard shells, zsh most closely resembles ksh but includes many enhancements. Zsh has command-line editing, built-in spelling correction, programmable command completion, shell functions (with autoloading), a history mechanism, and a host of other features.

$

> **NOTE**
> **The** `apt show` **command does not indicate that the package is installed on the system. It shows only detailed package information from the software repository.**

One detail you cannot get with apt is a listing of all the files associated with a particular software package. To get this list, you will need to go to the dpkg command itself:

```
dpkg -L package_name
```

Here's an example of using dpkg to list all the files installed as part of the acl package:

```
$ dpkg -L acl
/.
/bin
/bin/chacl
/bin/getfacl
/bin/setfacl
/usr
/usr/share
/usr/share/doc
/usr/share/doc/acl
/usr/share/doc/acl/copyright
/usr/share/man
/usr/share/man/man1
/usr/share/man/man1/chacl.1.gz
/usr/share/man/man1/getfacl.1.gz
/usr/share/man/man1/setfacl.1.gz
/usr/share/man/man5
/usr/share/man/man5/acl.5.gz
/usr/share/doc/acl/changelog.Debian.gz
$
```

You can also do the reverse — find what package a particular file belongs to:

```
dpkg --search *absolute_file_name*
```

Note that you need to use an absolute file reference for this to work:

```
$ dpkg --search /bin/getfacl
acl: /bin/getfacl
$
```

The output shows the getfacl file was installed as part of the *acl* package.

## Installing software packages with apt

Now that you know more about listing software package information on your system, this section walks you through a software package installation. First, you'll want to determine the package name to install. How do you find a particular software package? Use *apt* with the search command:

```
apt search *package_name*
```

The beauty of the search command is that you do not need to insert wildcards around *package_name*. Wildcards are implied. By default, the search command displays packages that contain the search term in either the package name or the package description, which can be misleading at times. If you want to limit the output to only package names, include the --names-only option:

```
$ apt --names-only search zsh
```

Sorting... Done
Full Text Search... Done
fizzsh/focal,focal 1.0.9-1 all
    Friendly Interactive ZShell

zsh/focal 5.8-3ubuntu1 amd64
    shell with lots of features

zsh-antigen/focal,focal 2.2.3-2 all
    manage your zsh plugins

zsh-autosuggestions/focal,focal 0.6.4-1 all
    Fish-like fast/unobtrusive autosuggestions for zsh

zsh-common/focal,focal 5.8-3ubuntu1 all
    architecture independent files for Zsh

zsh-dev/focal 5.8-3ubuntu1 amd64
    shell with lots of features (development files)

zsh-doc/focal,focal 5.8-3ubuntu1 all
    zsh documentation - info/HTML format

zsh-static/focal 5.8-3ubuntu1 amd64
    shell with lots of features (static link)

zsh-syntax-highlighting/focal,focal 0.6.0-3 all
    Fish shell like syntax highlighting for zsh

zsh-theme-powerlevel9k/focal,focal 0.6.7-2 all
    powerlevel9k is a theme for zsh which uses powerline fonts

zshdb/focal,focal 1.1.2-1 all
    debugger for Z-Shell scripts
$

Once you find the package you'd like to install, installing it using apt is as easy as this:

```
apt install package_name
```

The output will show basic information about the package and ask if you want to proceed with the installation:

```
$ sudo apt install zsh
[sudo] password for rich:
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  zsh-common
Suggested packages:
  zsh-doc
The following NEW packages will be installed:
  zsh zsh-common
0 upgraded, 2 newly installed, 0 to remove and 56 not
upgraded.
Need to get 4,450 kB of archives.
After this operation, 18.0 MB of additional disk space will
be used.
Do you want to continue? [Y/n] y
Get:1 http://us.archive.ubuntu.com/ubuntu focal/main amd64
zsh-common all 5.8-3ubuntu1 [3,744 kB]
Get:2 http://us.archive.ubuntu.com/ubuntu focal/main amd64
zsh amd64 5.8-3ubuntu1 [707 kB]
Fetched 4,450 kB in 4s (1,039 kB/s)
Selecting previously unselected package zsh-common.
(Reading database ... 179515 files and directories currently
installed.)
Preparing to unpack .../zsh-common_5.8-3ubuntu1_all.deb ...
Unpacking zsh-common (5.8-3ubuntu1) ...
Selecting previously unselected package zsh.
Preparing to unpack .../zsh_5.8-3ubuntu1_amd64.deb ...
Unpacking zsh (5.8-3ubuntu1) ...
Setting up zsh-common (5.8-3ubuntu1) ...
Setting up zsh (5.8-3ubuntu1) ...
Processing triggers for man-db (2.9.1-1) ...
$
```

### NOTE

Before the apt command in the preceding listing, the sudo command is used. The sudo command allows you to run a command as the root user. You can use the sudo command to run administrative tasks, such as installing software.

To check if the installation processed properly, just use the list command with the --installed option again. You should see the package appear, indicating that it is installed.

Notice that when installing the requested package, apt asked to install other packages as well. This is because apt automatically resolves any necessary package dependencies for us and installs the needed additional library and software packages. This is a wonderful feature included in many package management systems.

## Upgrading software with apt

While apt helps protect you from problems installing software, trying to coordinate a multiple-package update with dependencies can get tricky. To safely upgrade all the software packages on a system with any new versions in the repository, use the upgrade command:

```
apt upgrade
```

Notice that this command doesn't take any software package names as an argument. That's because the upgrade option will upgrade all the installed packages to the most recent version available in the repository, which is safer for system stabilization.

Here's a sample output from running the apt upgrade command:

```
$
$ sudo apt upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following NEW packages will be installed:
binutils binutils-common binutils-x86-64-linux-gnu build-
essential dpkg-dev
fakeroot g++ g++-9 gcc gcc-9 libalgorithm-diff-perl
libalgorithm-diff-xs-perl libalgorithm-merge-perl libasan5
libatomic1
libbinutils libc-dev-bin libc6-dev libcrypt-dev libcif-
nobfd0 libctf0
libfakeroot libgcc-9-dev libitm1 liblsan0 libquadmath0
libstdc++-9-dev
libtsan0 libubsan1 linux-libc-dev make manpages-dev
The following packages will be upgraded:
chromium-codecs-ffmpeg-extra eog file-roller fonts-
opensymbol gedit
gedit-common gir1.2-gnomedesktop-3.0 glib-networking glib-
networking-common
glib-networking-services gnome-control-center gnome-
control-center-data
gnome-control-center-faces gnome-desktop3-data gnome-
initial-setup
libgnome-desktop-3-19 libjuh-java libjurt-java libnautilus-
extension1a
libnetplan0 libreoffice-base-core libreoffice-calc
libreoffice-common
libreoffice-core libreoffice-draw libreoffice-gnome
libreoffice-gtk3
libreoffice-help-common libreoffice-help-en-us libreoffice-
impress
libreoffice-math libreoffice-ogltrans libreoffice-pdfimport
libreoffice-style-breeze libreoffice-style-colibre
libreoffice-style-elementary libreoffice-style-tango
libreoffice-writer
libridl-java libuno-cppu3 libuno-cppuhelpergcc3-3 libuno-
purpenvhelpergcc3-3
libuno-sal3 libuno-salhelpergcc3-3 libunoloader-java
nautilus nautilus-data
netplan.io python3-distupgrade python3-uno thermald ubuntu-
drivers-common
ubuntu-release-upgrader-core ubuntu-release-upgrader-gtk
ure
56 upgraded, 32 newly installed, 0 to remove and 0 not
upgraded.
Need to get 133 MB of archives.
After this operation, 143 MB of additional disk space will be
used.
Do you want to continue? [Y/n]
```

In the output, notice that apt lists the packages that will be upgraded, but also any new packages that are required to be installed because of upgrades.

The upgrade command won't remove any packages as part of the upgrade process. If a package needs to be removed as part of an upgrade, use the command

```
apt full-upgrade
```

Although this may seem like an odd thing, sometimes it's required to remove packages to keep things synchronized between distribution upgrades.

> NOTE
