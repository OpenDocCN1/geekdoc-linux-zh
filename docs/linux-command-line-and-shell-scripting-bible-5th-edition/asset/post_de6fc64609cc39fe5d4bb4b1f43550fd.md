
## Note

Instead of removing a snap, you can just disable it without removing it. Just use the `snap disable` command. To reenable the snap, use the `snap enable` command.

### Using flatpak containers

The *flatpak* application container format was created as an independent open source project with no direct ties to any specific Linux distribution. That said, battle lines have already been drawn, with Red Hat, CentOS, Rocky, and Fedora oriented toward using flatpak instead of Canonical’s snap container format.

If you’re using a Linux distribution that supports flatpak, you can list the installed application containers using the `flatpak list` command:

```bash
$ flatpak list
$
```

In this Rocky distribution, there aren’t any flatpak application containers installed by default. To find an application in the flatpak repository, you use the `flatpak search` command:

```bash
$ flatpak search solitaire
Name            Description                    Application ID       Version     Branch     Remotes
Aisleriot So...    Play many differe...           org.gnome.Aisle    3.22.35    stable     flathub
PySolFC                Solitaire game co...         org.pysolfc.PyS    3.2.0      stable     flathub
TriPeaks NGSUG    Patience game            …           …             imogpuz.trip     peaks.n     0.9.2     stable     flathub
TriPeaks         A Tri Peaks solit...        …          …             imogpuz.TriPe    aks-GDX     1.2.3     stable     flathub
KPaticience     Solitaire card ga...        …           …            org.kde.kpat     25.04.1    stable     flathub
KMahjonggg     Mahjong Solitaire        …             …            org.kde.kmah     jonggg      0.9.25041  stable     flathub
Simon Tatham...    Puzzle game colle...          …         …         …rk.gsth     am.puzzles   20230408   stable     flathub
Peg-E          Jump pegs to elim...            …          …            org.gottcode.P     eg-E       1.3.5     stable     flathub
Mahjongg        Match tiles and c...        …           …            org.gnome.Mah    jongg       48.1     stable     flathub
KShisen        Shisen-Sho Mahjon...        …            …             org.kde.kshi     sen      1.1.25041  stable     flathub
$
```

The output from the command trims some of the information to help simplify things. When working with a container, you must use its Application ID value and not its name. To install the application, use the `flatpak install` command:

```bash
$ sudo flatpak install org.gnome.Aisle
[sudo] password for rich:
Looking for matches...
Required runtime for org.gnome.Aisleriot/x86_64/stable (runtime/org.gnome.Platform/x86_64/48) found in remote flathub
Do you want to install it? [Y/n]: y

org.gnome.Aisleriot permissions:
   ipc          fallback-x11       pulseaudio       wayland       x11          dri
```

| ID | Branch | Op | Remote | Download |
| :--- | :--- | :--- | :--- | :--- |
| 1. | org.freedesktop.Platform.GL.default 24.08 | + | flathub | 155.3 MB / 155.7 MB |
| 2. | org.freedesktop.Platform.GL.default 24.08x86_64 | - | flathub | 23.9 MB / 155.7 MB |
| 3. | org.freedesktop.Platform.openh264 2.5.1 | + | flathub | 913.7 KB / 971.4 KB |
| 4. | org.gnome.Aisleriot.Locale stable | - | | 7.5 KB / 1.3 MB |
| 5. | org.gnome.Platform.Locale 48 | - | flathub | 18.6 KB / 387.8 MB |
| 6. | org.gnome.Platform 48 | - | flathub | 340.5 MB / 398.3 MB |
| 7. | org.gnome.Aisleriot stable | - | flathub | 17.9 MB / 24.3 MB |

```bash
Installation complete.
$
```

The installation automatically installs any dependencies required for the package. To check if the installation went well, you can use the `flatpak list` command again:

```bash
$ flatpak list
```

| Name | Application ID | Version | Branch | Installation |
| :--- | :--- | :--- | :--- | :--- |
| FreeDesktop SDK | .freedesktop.Platform.GL.default | 25.0.5 | 24.08 | system |
| FreeDesktop SDK | .freedesktop.Platform.GL.default | 25.0.5 | 24.08x86_64 | system |
| Cisco Systems, Inc. | .freedesktop.Platform.openh264 | 2.5.1 | 2.5.1 | system |
| The GNOME Project | org.gnome.Aisleriot | 3.22.35 | stable | system |
| GNOME Application Platform | .gnome.Platform | 48 | | system |

```bash
$
```

And finally, to remove an application container, use the `flatpak uninstall` command:

```bash
$ sudo flatpak uninstall org.gnome.Aisleriot
[sudo] password for rich:
```

| ID | Branch | Op |
| :--- | :--- | :--- |
| 1. | org.gnome.Aisleriot stable | - |
| 2. | org.gnome.Aisleriot.Locale stable | - |

```bash
Uninstall complete.
$
```

Using application containers is similar to using package management systems, but what goes on behind the scenes is fundamentally different. However, the end result is that you have an application installed on your Linux system that can be easily maintained and upgraded.

### Summary

This chapter discussed how to work with a software package management system to install, update, or remove software from the command line. Most of the Linux distributions use fancy GUI tools for software package management, but you can also perform package management from the command line.

The Debian-based Linux distributions use the `dpkg` utility to interface with the package management system from the command line and use the `apt-cache` and `apt-get` utilities to interface with a common repository to easily download and install new software. A frontend to these utilities is `apt`. It provides simple command-line options for working with software packages in the `dpkg` format.

The Red Hat–based Linux distributions are based on the `rpm` utility but use different frontend tools at the command line. Red Hat, CentOS, Rocky, and Fedora use `dnf` for installing and managing software packages. The openSUSE distribution uses `zypper` for managing software.

Application containers are a relatively new player in software package management. An application container bundles all the files necessary for an application to run in one installable package. This means the application doesn’t rely on any external dependencies such as library files, and the container bundle can be installed in any Linux distribution and run. Currently the two most popular container packages are **snap**, common in the Ubuntu Linux distribution, and **flatpak**, used in Red Hat Linux environments.

The next chapter takes a look at the various editors available in Linux distributions. As you get ready to start working on shell scripts, it will come in handy to know what editors are available to use.

## CHAPTER 10
## Working with Editors

### IN THIS CHAPTER

- Visiting the vim editor
- Navigating the nano editor
- Exploring the Emacs editor
- Exploring the KDE family of editors
- Exploring the GNOME editor

Before you start your shell scripting career, it’s wise to gain proficiency using at least one text editor in Linux. Using features such as searching, cutting, and pasting allows you to develop your shell scripts more quickly.

You have the choice of several editors. Many individuals find a particular editor whose functionality they love and use that one exclusively. This chapter provides a brief sampling of a few of the text editors you can employ in the Linux world.

### Visiting the vim Editor

The vi editor was one of the early editors used on UNIX systems. It uses the console graphics mode to emulate a text-editing window, allowing you to see the lines of your file; move around within the file; and insert, edit, and replace text.

Although it is quite possibly the most complicated editor in the world (at least in the opinion of those who hate it), vi provides many features that have made it a staple for programmers and system administrators for decades.

When the GNU Project ported the vi editor to the open source world, they chose to make some improvements to it. Because it extended the original vi editor found in the UNIX world, the developers also renamed it, to “vi improved” or vim.

This section walks you through the basics of using the vim editor to edit your text shell script files.

#### Checking your vim package

Before you begin your exploration of the vim editor, it's a good idea to determine what vim package your Linux system has installed. On some distributions, you will have the full vim package installed and an alias for the vi command, as shown on this Fedora distribution:

```bash
$ alias vi
alias vi='vim'
$ which vim
/usr/bin/vim
$ ls -1 /usr/bin/vim
-rwxr-xr-x. 1 root root 3522560 Nov 11 14:08 /usr/bin/vim
$
```

Notice that the program file's long listing does not show any linked files (see Chapter 3, “Basic Bash Shell Commands,” for more information on linked files). If the vim program is linked, it may be linked to a less than full-featured editor. Thus, it's a good idea to check for linked files.

On other distributions, you will find various flavors of the vim editor. Notice on this Ubuntu distribution that not only is there no alias for the vi command, but the /usr/bin/vi program file belongs to a series of file links:

```bash
$ alias vi
-bash: alias: vi: not found
$ which vi
/usr/bin/vi
$ ls -l /usr/bin/vi
lrwxrwxrwx 1 root root 20 Apr 23 14:33 /usr/bin/vi -> /etc/alternatives/vi
$ ls -l /etc/alternatives/vi
lrwxrwxrwx 1 root root 17 Apr 23 14:33 /etc/alternatives/vi -> /usr/bin/vim.tiny
$ readlink -f /usr/bin/vi
/usr/bin/vim.tiny
$
```

Thus, when the vi command is entered, the /usr/bin/vim.tiny program is executed. The vim.tiny program provides only a few vim editor features. If you are serious about trying out the vim editor and are using a distribution that uses a vim alternative, such as vim.tiny, consider installing the basic vim package for more vim features.
