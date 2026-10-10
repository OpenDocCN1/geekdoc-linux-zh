# The Red Hat–Based Systems

Like the Debian-based distributions, the Red Hat–based systems have several different front-end tools available. The common ones are:

+   * *yum* : Used in Red Hat, CentOS, and Fedora

+   * *zypper* : Used in openSUSE

+   * *dnf* : An updated version of *yum* with some additional features

These front ends are all based on the *rpm* command-line tool. The following section discusses how to manage software packages using these various *rpm* -based tools. The focus will be on *dnf* , but the other packages use similar commands and formats.

# Listing installed packages

To find out what is currently installed on your system, at the shell prompt type the following command:

```
dnf list installed
```

The information will probably whiz by you on the display screen, so it's best to redirect the installed software listing into a file. You can then use the `more` or `less` command (or a GUI editor) to look at the list in a controlled manner.

```
dnf list installed> installed_software
```

To find out detailed information for a particular software package, *dnf* really shines. Not only will it give you a very verbose description of the package, but with another simple command, you can see whether the package is installed:

```
$ dnf list xterm
Last metadata expiration check: 0:05:17 ago on Sat 16 May
2020 12:10:24 PM EDT.
Available Packages
xterm.x86_64                      351-1.fc31
updates
```

```
$ dnf list installed xterm
Error: No matching Packages to list
```