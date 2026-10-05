# DEBIAN GNU/LINUX 2.1 715

out all required settings you leave the package list with carry out installation and uninstallation with the two items of the main menu.

# Package dependencies

As soon as you select a package that requires another package, a new screen appears with the list of all missing packages. This list shows all packages that should be installed as well. Required packages are already marked for installation, while packages which are only recommended are not marked. The following lines show unresolved package dependencies of the installation of tkman.

```
* Xtr non-free tkman A graphical, hypertext, manual page browser.
* Opt libs tkl42 The Tk toolkit for TCL and X11 v4.2 - Run-Time
* Xtr non-free rman Rosetta - Reverse compile pages
* Opt libs tcl76 The Tool Command Language (TCL) v7.6 - Run-Time
```

```
tkman depends on tk42
tkman depends on rman
tk42 depends on tcl76 (>= 7.6-0)
```

In the simplest case, you leave the dependency page with dselect. In this case, simply accept all default settings with dselect.

However, before you press you can also use or to select optional packages for installation, thus changing the defaults. It is, however, not possible to leave the dependency path as long as there are unresolved dependencies. (You can force acceptance of your settings with Q if you know what you are doing.)

If the extent of installation of the required packages is too large, and you wish to undo the selection of the package that caused the conflict, just press X.

# dpkg

While dselect provides a more or less user-friendly interface for package installation and management, the same tasks can also be achieved by means of the command driven dpkg command.

As a Debian user, you usually manage with dpkg. dpkg is an efficient alternative to dselect, if you quickly want to install an individual package (for example, from an additional contrib CD). The different dpkg-xyz commands, are, are mostly of interest if you want to build your own packages.

Information on installed and available packages (no matter whether they were installed with dselect or dpkg) can be found in /var/lib/dpkg. Documentation on the installed packages that goes beyond the man and info texts usually be found in /usr/doc/package_name.