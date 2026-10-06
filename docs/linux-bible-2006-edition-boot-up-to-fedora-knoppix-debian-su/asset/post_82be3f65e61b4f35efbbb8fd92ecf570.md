
## Package Management Using dpkg

As mentioned earlier, the dpkg utility is the core package management tool in Debian. Most other package management tools within the system, including APT, use dpkg to perform the underlying work, and dpkg in turn uses dpkg-deb and dpkg-query to handle a number of the low-level functions. In most cases, you will need to use APT or Aptitude for package management, and use dpkg in only a few situations.

Far too many commands associated with dpkg exist in this chapter, but the most common ones are explained in the following sections. In most cases, there are short and long commands to perform the same function. Whichever is easier for you to remember.

## Installing and Removing Packages

Packages can be installed with dpkg using the -i --install flags and the path to the .deb file containing the package. The path must be accessible as a filesystem path (HTTP, FTP, and other methods are not supported), and more than one package can be specified:

```
# dpkg --install /home/wayne/lsof_4.71-1_i386.deb
```

Package removal through dpkg is also straightforward and is done with the -r --remove commands. When configuration files are to be removed, the -p or --purge command can be used instead. Both commands can also be used to specify multiple packages to remove:

```
# dpkg --remove lsof
or...
# dpkg --purge lsof
```

## Querying the Package Database

You will often need to obtain more information about packages that are already installed on your system. Because these operations do not modify the package database, they can be done as a non-root user.

To list all packages known to dpkg, use the -l or --list commands:

```
# dpkg --list
```

You can restrict the list by specifying a glob pattern:

```
# dpkg --list *lsof**
```

The quotes are used to prevent the shell from replacing the wildcard with a list of matching files in the current directory. For more information about wildcards, see Chapter 2 or type man 7 glob to see a list of wildcards.

To view detailed information about a specific package, use the -s or --status command:

```
$ dpkg --status lsof
Package: lsof
Status: install ok installed
Priority: standard
Section: utils
...
```

The origin package for a file can be determined using the -S or --search command:

```
$ dpkg --search /bin/ls
coreutils:/bin/ls
```

The list of files in an installed package can be viewed using the -L or --list command:

```
$ dpkg --list lsof
/usr
/usr/sbin
/usr/bin
```

## Examining a Package

Package files can be examined before installing them using either the --info (-i) or the --contents (-c) command. These options can be used on packages in a local directory, as opposed to using them to examine packages on a remote server.

The following --info option shows the package name, version information, and sizes of different parts of the package. Beyond that (although shortened here) you would be able to see a list of packages depends on and descriptive information about the package.

```
$ dpkg --info lsof_4.71-1_i386.deb
new debian package, version 2.0,
size 319038 bytes: archive=15334 bytes, 557 bytes, 16 lines control, 2246 bytes, 12 lines mdsums
Package: lsof
Version: 4.71-1
```

The following --contents option lets you see the full contents of the package as if you were listing them with ls -l command. You can see the path to each file, its permission settings and group ownership:

```
$ dpkg --contents lsof_4.71-1_i386.deb
drwx-xr-x root/root ./
drwx-xr-x root/root /usr
drwx-xr-x root/root /usr/bin
```

## Installing Package Sets (Tasks) with Tasksel

Some package sets are too large to be managed practically through meta packages, so tasks have been created as an alternative. Tasks are installed and removed using the tasksel utility. When run without any arguments, tasksel presents a menu from which you can select to install or remove.

Additional options are available from the command line:

- To see a list of known tasks, run tasksel --list
- To list the packages that are installed by a task, run tasksel --packages <task name>.

> Caution When a task is removed, all packages associated with that task, whether installed manually or as part of that task, are removed

An example of a popular task to install is the desktop task. The desktop task installs three complete desktop environments on the X Window System: GNOME, KDE, and XFCE. Note that this task will take a long time to download and requires several gigabytes of disk space to complete. To start the desktop task, run the following:

```
$ tasksel install desktop
```

## Alternatives, Diversions, and Stat Overrides

In cases where there is more than one installed program that provides a specific function, package maintainers have the option of utilizing Debian's alternatives system. The alternatives manages which program is executed when you run a specific command. For instance, the ed, nano, and nvi packages provide a text editor. An alternative maintained in the system guarantees that a text editor is accessible through the generic editor command, regardless of which combination of these packages is installed.

```
# dpkg-statoverride --update --add 0000 /usr/bin/wall
```

This sets the owner and group of /usr/bin/wall to root and root and disables all permissions on the file.

> You can find more information about file permissions in the "Understanding File Permissions" section of Chapter 2.

Unlike dpkg-diver, dpkg-statoverride does not keep track of the original file permissions. As a result, removing an override does not restore the old permissions. After removing the override, you may need to set the permissions manually or reinstall the package that contained it:

```
# dpkg-statoverride --remove /usr/bin/wall
# apt-get --reinstall bdtutils
Reading Package Lists... Done
Building Dependency Tree... Done
0 upgraded, 0 newly installed, 1 to remove and 0 not upgraded.
Need to get 08/62.5kb of archives.
After unpacking 0B of additional disk space will be used.
Do you want to continue? [Y/n]
(Reading database ... 16542 files and directories installed)
Preparing to replace bdtutils 1:22-10 (using .../bdtutils_1%3a2.12-10_i386.deb) ...
Unpacking replacement bdtutils ...
Setting up bdtutils (2:12-10)
```

## Managing Package Configuration with debconf

All packages that support configuration management through debconf are configured as they are installed. If you want to change a configuration option, you can do so using the dpkg-reconfigure utility. For instance, you can change the configuration options for ssh using the following:

```
# dpkg-reconfigure ssh
```

Every configuration parameter is assigned a priority by the package maintainer. This allows debconf to select the default values for below a specific priority. By default, you will be prompted to answer questions of only medium, high, or critical priority; low-priority questions are answered automatically. You can change this by reconfiguring the debconf package:

```
# dpkg-reconfigure debconf
```

> Advanced users maintaining multiple systems may want to create a database of configuration settings that can be distributed to every computer (or to sets of computers) to reduce the number of repeated steps. This process is documented in the debconf and debconf.conf pages.
