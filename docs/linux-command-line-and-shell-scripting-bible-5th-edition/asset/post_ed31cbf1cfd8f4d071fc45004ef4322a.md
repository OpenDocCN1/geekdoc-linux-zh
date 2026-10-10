
## Installing software packages with apt

Now that you know more about listing software package information on your system, this section walks you through a software package installation. First, you'll want to determine the package name to install. How do you find a particular software package? Use apt with the search command:

```
apt search package_name
```

The beauty of the search command is that you do not need to insert wildcards around package_name. Wildcards are implied. By default, the search command displays packages that contain the search term in either the package name or the package description, which can be misleading at times. If you want to limit the output to only package names, include the --names-only option:

```
$ apt --names-only search zsh
Sorting ... Done
Full Text Search ... Done

fizzsh/noble 1.0.9-1 all
    Friendly Interactive ZSHell

python3-colcon-zsh/noble 0.5.0.1-1 all
    collective construction meta build tool - zsh extension

zsh/noble,now 5.9-6ubuntu2 amd64 [installed]
    shell with lots of features

zsh-antidote/noble 1.9.4-1 all
    ZSH plugin manager

zsh-antigen/noble 2.2.3-5 all
    manage your zsh plugins

zsh-autosuggestions/noble 0.7.0-1 all
    Fish-like fast/obtrusive autosuggestions for zsh

zsh-common/noble,now 5.9-6ubuntu2 all [installed,automatic]
    architecture independent files for Zsh

zsh-dev/noble 5.9-6ubuntu2 amd64
    shell with lots of features (development files)

zsh-doc/noble 5.9-6ubuntu2 all
    zsh documentation - info/HTML format

zsh-static/noble 5.9-6ubuntu2 amd64
    shell with lots of features (static link)

zsh-syntax-highlighting/noble 0.7.1-2 all
    Fish shell like syntax highlighting for zsh

zsh-theme-powerlevel9k/noble 0.6.7-4 all
powerlevel9k is a theme for zsh which uses powerline fonts
$
```

Once you find the package you'd like to install, installing it using apt is as easy as this:

```
apt install _package_name_
```

The output will show basic information about the package and ask if you want to proceed with the installation:

```
$ sudo apt install zsh
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
libllvm17t64 python3-netifaces
Use 'sudo apt autoremove' to remove them.
Suggested packages:
zsh-doc
The following NEW packages will be installed:
zsh
0 upgraded, 1 newly installed, 0 to remove and 1 not upgraded.
Need to get 812 kB of archives.
After this operation, 2,489 kB of additional disk space will be used.
Get:1 http://us.archive.ubuntu.com/ubuntu noble/main amd64 zsh amd64
5.9-6ubuntu2 [812 KB]
Fetched 812 kB in 1s (1,137 kB/s)
Selecting previously unselected package zsh.
(Reading database ... 209759 files and directories currently installed.)
Preparing to unpack .../zsh 5.9-6ubuntu2_amd64.deb ...
Unpacking zsh (5.9-6ubuntu2) ...
Setting up zsh (5.9-6ubuntu2) ...
Processing triggers for debutils (5.17build1) ...
Processing triggers for man-db (2.12.0-4build2) ...$
```

> **Note**
> 
> Before the *apt* command in the preceding listing, the *sudo* command is used. The *sudo* command allows you to run a command as the root user. You can use the *sudo* command to run administrative tasks, such as installing software.

To check if the installation processed properly, just use the `list` command with the `--installed` option again. You should see the package appear, indicating that it is installed.

Notice that when installing the requested package, *apt* asked to install other packages as well. This is because *apt* automatically resolves any necessary package dependencies and installs the needed additional library and software packages. This is a wonderful feature included in many package management systems.

## Upgrading software with apt

While apt helps protect you from problems installing software, trying to coordinate a multiple-package update with dependencies can get tricky. To safely upgrade all the software packages on a system with any new versions in the repository, use the upgrade command:

```
apt upgrade
```

Notice that this command doesn't take any software package names as an argument. That's because the upgrade option won't upgrade all the installed packages to the most recent version available in the repository, which is safer for system stabilization.

Here's a sample output from running the apt upgrade command:

```
$ sudo apt upgrade
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Calculating upgrade... Done
The following packages were automatically installed and are no longer required:
  libllvm17t64 python3-netifaces
Use 'sudo apt autoremove' to remove them.
Get more security updates through Ubuntu Pro with 'esm-apps' enabled:
  php-symfony-config libzvbl-common php-symfony-dependency-injection libjson1
  php-symfony-cache php-symfony-var-exporter libgpg-error0 php-twig
  libavcodec60 libavdevice60 libavutil58 libswscale7
  php-symfony-expression libswresample4 libavformat60 libavfilter9
  php-symfony-filesystem
Learn more about Ubuntu Pro at https://ubuntu.com/pro
The following NEW packages will be installed:
  linux-headers-6.11.0-26-generic linux-headers-6.11.1-headers-6.11.0-26
  linux-hwe-6.11-tools-6.11.0-26 linux-image-6.11.0-26-generic
  linux-modules-6.11.0-26-generic linux-modules-extra-6.11.0-26-generic
  linux-tools-6.11.0-26-generic
The following upgrades have been deferred due to phasing:
  ubuntu-drivers-common
The following packages will be upgraded:
  apparmor apparmor-profiles apparmor-utils binutils binutils-common
  binutils-x86-64-linux-gnu cloud-init distro-info-data fwupd ghostscript
  gir1.2-glib-2.0 gir1.2-gtk-3.0 gir1.2-gtk-4.0 gir1.2-javascriptcoregtk-4.1
  gir1.2-javascriptcoregtk-6.0 gir1.2-mutter-14 gir1.2-soup-3.0
  gir1.2-webkit-6.0 gir1.2-webkit-4.1 gnome-control-center
  gnome-control-center-data gnome-control-center-faces gnome-shell
  gnome-shell-common gnome-shell-extension-ubuntu-dock grub-common grub-pc
  grub-pc-bin grub2-common libapparmor-lts libmcsctl-microcode
  libabi32t64 libc6v2 libgccv10.1 libgccm2c7 libgccs2 libgccs1 libgccd0 libccrt-noabid5
  ...
122 upgraded, 7 newly installed, 0 to remove and 1 not upgraded.
Need to get 880 MB of archives.
After this operation, 319 MB of additional disk space will be used.
Do you want to continue? [Y/n]
```

In the output, notice that **apt** lists the packages that will be upgraded, but also any new packages that are required to be installed because of upgrades.

The **upgrade** command won’t remove any packages as part of the upgrade process. If a package needs to be removed as part of an upgrade, use this command:

```
apt full-upgrade
```

Although this may seem like an odd thing, sometimes it’s required to remove packages to keep things synchronized between distribution upgrades.

**Note**

Obviously, running **apt**’s **upgrade** option is something you should do on a regular basis to keep your system up to date. However, it is especially important to run it after a fresh distribution installation. Usually there are lots of security patches and updates that are released since the last full release of a distribution. Also, it’s recommended to run the **update** option first, which updates the repository listing to ensure **apt** is working with the latest repositories.

## Uninstalling software with apt

Getting rid of software packages with **apt** is as easy as installing and upgrading them. The only real choice you have to make is whether or not to keep the software’s data and configuration files around afterward.

To remove a software package but not the data and configuration files, use **apt**’s **remove** command. To remove a software package and the related data and configuration files, use the **purge** option:

```
$ sudo apt purge zsh
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libllvm17t64 python3-netifaces zsh-common
Use 'sudo apt autoremove' to remove them.
The following packages will be REMOVED:
  zsh*
0 upgraded, 0 newly installed, 1 to remove and 123 not upgraded.
After this operation, 2,489 kB disk space will be freed.
Do you want to continue? [Y/n] Y
(Reading database ... 209817 files and directories currently installed.)
Removing zsh (5.9-6ubuntu2) ...
Processing triggers for debianutils (5.17build1) ...
Processing triggers for man-db (2.12.0-4build2) ...
(Reading database ... 209759 files and directories currently installed.)
Purging configuration files for zsh (5.9-6ubuntu2) ...
$
```
