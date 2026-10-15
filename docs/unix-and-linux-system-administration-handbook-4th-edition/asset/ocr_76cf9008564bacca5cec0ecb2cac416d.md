# Solaris packaging

Since SunOS 2.0, Solaris packaging was traditionally managed by SVR4 with some incremental improvements that kept the system hobbling along for twenty years or so. Unfortunately, SVR4 is deficient in many areas, including dependency management, usability, support for new technologies such as ZFS, and support for network repositories. For OpenSolaris, the developers decided to scrap the old system and start fresh.

OpenSolaris now uses the Image Packaging System (IPS), which is a great leap forward over SVR4. It incorporates network repositories as a key architectural theme. In addition to standard package management functionality, the system offers tools for package developers that simplify the creation and centralization of theme. IPS also offers backward compatibility with legacy SVR4 packages.

At the moment, IPS packages are markedly dissimilar to those in formats such as .deb or RPM. An IPS package is not a single file that you can easily copy among systems. Rather, a package is a collection of files, dependencies, and other data that must be served from a repository by IPS’s pkg.depotd daemon. IPS remains under development, and a more palatable format is promised someday.

You use the pkg command for most IPS operations—installation, removal, searching, status queries, etc. pkg also manages repositories, though they’re referred to as “publishers” in the pkg documentation and command syntax. pkg install, pkg uninstall, pkg search, and pkg info all perform the expected functions. The pkg image-update command is similar to APT’s dist-upgrade; it updates all installed packages to the latest available versions.

By default, the OpenSolaris release repository is the default publisher. It currently hosts around 1,700 packages.

```
solaris$ pkg publisher
PUBLISHER          TYPE    STATUS    URI
opensolaris.org (preferred)  origin  online  http://pkg.opensolaris.org/rele...
```

See man -s5 pkg for further details on IPS, or man pkg for information on the pkg command.

# HP-UX packaging

HP’s packaging system, formally known as Software Distributor or SD, has offered HP-UX users robust package management since version 10. It’s a no-nonsense tool with a bundle of features that’s sure to make any system administrator giddy with excitement:

+   - Most tools offer graphical, curses-based, and command-line operating modes, depending on how they are invoked.

> 5. The development team distinguishes between the terms “repository” and “publisher,” but we’ll treat them as equivalent here.

> 6. Contrast with more than 30,000 in Ubuntu Karmic Koala.