section, "Per-Package Updates," can locate all the packages and ports for which updates are available. Likewise, the make world process upgrades everything. Sometimes you don't want to update every program, though. To perform a more selective update, you should evaluate what programs you want to update. The most important updates are those to fix security-related bugs, so you should keep abreast of security developments to learn what might need updating. FreeBSD maintains a list of security advisories at http://www.freebsd.org/security/, so checking this site on a regular basis (say, once a day) can help you learn of security problems. There are also dedicated security web pages and mailing lists, such as those maintained by the Computer Incident Advisory Capability (CIAC; http://www.ciac.org/ciac/) or the Computer Emergency Response Team Coordination Center (CERT/CC; http://www.cert.org). If you've installed packages from unusual sources, you should check back with those sources regularly to learn of important updates.

Nonsecurity updates are less critical, so you may simply want to periodically check for updates to important packages, particularly if you wish those packages were less buggy or had additional features. Installing or not installing such updates is a judgment call.

# Per-Package Updates

The portupgrade program is an extremely useful tool for upgrading programs on a per-package (or per-port) basis. portupgrade may or may not be installed on your system; if not, you can install it with the sutils package or ports section. portupgrade supports many options, so you should consult its man page for details; but a simplified syntax is

```
portupgrade [options] [package-name]
```

The meanings of these options are

+   - **-a or --all** This option causes portupgrade to upgrade every package installed on the system.
+   - **-f or --force** You can have portupgrade replace a package even if the "new" version is the same version number or older than the installed package. This option might be useful if you've upgraded to an experimental package but have problems with it, and so want to return to the last stable version of the package.
+   - **-g or --go-on** Ordinarily, if a package depends upon other packages, portupgrade requires that the depended-upon packages be installed or upgraded successfully before the primary package is upgraded. This option tells the system to ignore failures to install or upgrade depended-upon packages. You might use this option if you've installed such dependencies in a way that doesn't use FreeBSD's package database.