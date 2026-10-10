
## Using Flatpak Containers

The *flatpak* application container format was created as an independent open source project with no direct ties to any specific Linux distribution. That said, battle lines have already been drawn, with Red Hat–based Linux distributions oriented toward using flatpak instead of Canonical’s snap container format.

![](img/c0a399aca0d18f8822d714ad0a173123_481_0.png)

> While Red Hat desktop distributions install flatpak by default, the server distributions don’t. However, you can easily install flatpak as a package using the standard dnf or rpm method.

To display the current flatpak containers installed on the system, use the `list` command:

```
$ flatpak list
$
```

Not too exciting. When you first install flatpak there won’t be any containers installed, but now you know that flatpak is installed.

By default Red Hat–based Linux distributions don’t configure any repositories for flatpak (repositories in flatpak are called *remotes*). The most popular flatpak remote is Flathub. Currently, to set flatpak to point to the Flathub remote you use the following:

```
$ sudo flatpak remote-add --if-not-exists flathub
https://flathub.org/repo/flathub.flatpakrepo
[sudo] password for rich:
$
```

To find an application in the flatpak repository, you use the `flatpak search` command:

```
$ sudo flatpak search mosh
```

| Name | Description | Application ID | Version | Branch | Remotes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Mosh | The Mobile Shell | org.mosh.mosh | 1.3.2 | stable | flathub |

When working with a container, you must use its Application ID value and not its name. To install the application, use the `flatpak install` command:

```
$ sudo flatpak install org.mosh.mosh
Looking for matches...
Found similar ref(s) for 'org.mosh.mosh' in remote 'flathub' (system).
Use this remote? [Y/n]: Y
Required runtime for org.mosh.mosh/x86_64/stable
(runtime/org.freedesktop.Platform/x86_64/21.08) found in remote flathub
Do you want to install it? [Y/n]: Y
org.mosh.mosh permissions:
network	ssh-auth
```

| ID | Branch | Op | Remote | Download |
|---|---|---|---|---|
| 1. `org.freedesktop.Platform.GL.default` | 21.08 | i | flathub | 130.9 MB / 131.2 MB |
| 2. `org.freedesktop.Platform.Locale` | 21.08 | i | flathub | 17.7 kB / 325.0 MB |
| 3. `org.freedesktop.Platform.openh264` | 2.0 | i | flathub | 1.5 MB / 1.5 MB |
| 4. `org.freedesktop.Platform` | 21.08 | i | flathub | 153.7 MB / 198.9 MB |
| 5. `org.mosh.mosh` | stable | i | flathub | 10.5 MB / 12.7 MB |

Installation complete.
$

To check if the installation went well, use the `flatpak list` command again:

```
$ flatpak list
```

| Name | Application ID | Version | Branch | Installation |
|---|---|---|---|---|
| Freedesktop Plat... | org.freedesktop.Platform | 21.08.7 | 21.08 | system |
| Mesa | ...freedesktop.Platform.GL.default | 21.3.1 | 21.08 | system |
| openh264 | ...g.freedesktop.Platform.openh264 | 2.1.0 | 2.0 | system |
| Mosh | org.mosh.mosh | 1.3.2 | stable | system |

```
$
```

And finally, to remove an application container, use the `flatpak uninstall` command:

```
$ sudo flatpak uninstall org.mosh.mosh
```

| | ID | Branch | Op |
|---|---|---|---|
| 1. [~] | org.mosh.mosh | stable | r |

Uninstall complete.
$

Working with flatpak containers is a bit different from using package management systems, but once you get comfortable with the format of things, it’s not all that different from the standard package management system.

![](img/c0a399aca0d18f8822d714ad0a173123_482_0.png)

AppImage is yet another format for distributing software in the Linux world. AppImage is a bit different in that standard users don’t need root privileges to install an AppImage package on the system. Instead of installing the software in the standard Linux system directories, AppImage distributes applications as a compressed disk image that standard users can mount in their Home directories and run. Of course, this means each individual user on the system who wants to run the application has to download a separate AppImage file to run the application.

## EXERCISE 13.1

**Working with Packages**

This exercise demonstrates how to work with a package management system to install software.

- 1. Log into your Linux system and open a new command prompt.
- 2. Display the packages currently installed on your system. For Debian-based systems such as Ubuntu, use the command `sudo apt-cache pgnames`. For Red Hat-based systems such as Rocky, use the command `sudo dnf list`.
- 3. If it’s not already installed on your system, install the zsh shell package. For Debian-based systems, use the command `sudo apt install zsh`. For Red Hat-based systems, use the command `sudo dnf install zsh`. If the zsh package is already installed, try installing the tcsh package, which is an open source version of the C shell found in many Unix systems.
- 4. Display the installed packages on your system again to see if the newly installed package appears.
- 5. Now remove the package from your system. For Debian-based systems, use the command `sudo apt remove zsh`. For Red Hat-based systems, use the command `sudo dnf remove zsh`.
- 6. Display the installed packages yet again to see if the package was properly removed.

## Summary

The ability to easily install and remove applications is a must for every Linux system. In the open source world, developers release their applications as source code bundles using the `tar` and `gzip` utilities to create a tarball file. After you download a tarball file, you must decompress and extract the files it contains to be able to compile the application. The `gcc` program is the most common program for compiling many open source applications. You use the `configure` and `make` utilities to create and run installation scripts to make it easier to install applications from source code.

Most Linux distributions help simplify application installation by precompiling the source code and bundling the necessary application files into a package. Package management software makes it easier to track what applications are installed on your Linux system and where their files are located. Debian-based Linux distributions use the `DEB` package management format, with the `dpkg` tool, while Red Hat–based Linux distributions use the `RPM` package management format, with the `rpm` tool.

While package management systems make it easier to install and remove packages, it’s still somewhat of a hassle finding packages. Most Linux distributions now maintain their own repository of packages and provide additional tools, making it easier to retrieve and install packages from the repository. For Debian-based systems, the **apt** suite of tools, including **apt-cache** and **apt-get**, and **apt** are used to retrieve packages from the repository and maintain the package management database. For Red Hat-based systems, either **yum** or **dnf** is the package tool to use.

Application containers are now becoming somewhat popular in the Linux world. An application container bundles all software required to run an application, including dependency applications and all libraries, into a single installation package. The two most popular application container formats are **snap** and **flatpak**.

## Exam Essentials

- Describe how developers bundle their open source applications for distribution. Linux developers bundle source code files, headers, libraries, and documentation files into a single file for distribution. They use the **tar** utility to archive multiple files and folders into a single archive file and then often compress the archive file using the **gzip** utility. You can use the **wget** or **cURL** program to download the source code distribution files and then use the **gzip** and **tar** utilities to decompress and extract the source code files.

- Explain how to generate an executable program from a source code tarball. After you decompress and extract the source code files from a distribution tarball file, you must compile the source code to create an executable file for the application. First, you must use the **configure** utility. This examines your Linux system to ensure that it has the correct dependencies required for the application and configures the installation script to find the dependencies. Next, you run the **make** utility. The **make** utility runs a script that uses the **gcc** compiler to compile the necessary library and source code files to generate the executable file for your system. Once that script completes, use the **make** script with the **install** option to install the executable file on your Linux system.

- Describe how Linux packages applications for distribution. Linux uses a package management system to track what applications are installed on your system. The distribution bundles precompiled application files into a package, which you can easily download and install. The package management database keeps track of which packages are installed and the location of all the files contained within the package. You can also query the package management database to determine what packages are installed and remove packages from the system using the package management tools. Debian-based systems use the **dpkg** tool to interact with the package management database, whereas Red Hat-based Linux systems use the **rpm** tool.

- Describe how Linux distributions use repositories. While using packages makes installing, tracking, and removing software applications easier, you still must be able to find the latest packages for your applications. Most Linux distributions help with that by creating a centralized repository of current application packages, along with tools to work with the
