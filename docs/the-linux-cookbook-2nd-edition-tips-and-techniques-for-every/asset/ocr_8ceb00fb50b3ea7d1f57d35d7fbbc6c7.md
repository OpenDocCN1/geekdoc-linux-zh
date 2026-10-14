Recipe 7.5 [Finding Where a Program Is Located], page 185). For example, if perl is located on your system at /usr/bin/perl, you will have to edit the first line in this script so that it matches that actual location.

If you try to execute this script, and the system reports an error finding the file, you'll have to change that first line to correspond to the location of the perl binary on your system. The which tool will output this location.

⇒ To find out where perl is installed on your system, type:

```
# which perl [RET]
```

If this command returns /usr/bin/perl or some path name other than /usr/local/bin/perl, you'll have to change the location in the first line of the script to the path name given:

```
#!/usr/bin/perl
```

NOTES: If the output of the which command returns nothing, that means that the perl program is not installed on your system at all; in that case, you should install the perl software in order to run the script.

# A.4 Managing DEB Packages

+   Dpkg
+     DEB: dpkg
+     or
+   Apt
+     DEB: apt

DEB is the native package format on Debian systems. These packages are available on the Web from http://packages.debian.org/.

There are a number of tools available for DEB package management. Traditionally, dselect, where you select packages from a menu, was the tool for installing and removing software from the system. Its interface is unique, it so requires study. Proper usage is, unfortunately, an acquired skill.³ Administrators who are installing a new system are urged to run through dselect and reboot at least a few times, so that all essential packages and their dependencies are installed.

The dpkg tool is Debian's primary command line package manager tool (in fact, dselect is just a front-end interface to it), and it can be used on

> ³ Even its man page makes note of this: “The dselect package selection interface is confusing or even alarming to the new user.”