# CHAPTER 8 Managing Software and System Resources

(Picasso) release in 1996. Since, the rpm command has the prime feature of Red's unique software management system, which is based on the concept of pristine sources, or the capability to use a single, initial archive of program's source code not only to build packages for different systems, but also to track versions. With the release of Red 8.0 (Psyche) in 2002, Red offered a slightly updated graphical interface for its venerable RPM application.

In addition to improving the package management of early software management scripts, RPM version 4.1 introduced software features designed to ease the task of building software for different platforms from a single set of source-code files. Changes can be tracked and kept outside a developer's initial source code and multiple packages can be built from scratch and installed at the same time -at the same time, RPM also verifies installation dependencies. Additional features, such as a checksum and GNU Privacy Guard (GPG) signatures, enable binary software packages to be safely distributed without the fear of virus infection or the inclusion of Trojan code.

The rpm command uses the RPM system to remove, (erase), upgrade, verify, and build software known as .rpm files. These archives, or packages, contain package identification (a signature), checksums (mathematically derived values), and any archive of the software, either in source or binary format. .rpm package also contains quite a bit of additional information, such as a name, a version, and basic description, and can include pre- post-installation scripts used for installation, erasure, and upgrading.

The RPM database installed on your computer keeps track of which versions of which packages are installed. RPM uses your system's /var/lib/rpm directory to store files (actually databases) containing information about the software installed on your system. You can use the ls to view these files (you might see file sizes from those showing here, depending on the amount of software you have):

```
$ ls -l /var/lib/rpm
total 51108
-rw-r--r-- 1 rpm rpm 10465280 May 23 14:05 Basenames
-rw-r--r-- 1 rpm rpm 12288 May 23 14:03 Conflictname
-rw-r--r-- 1 rpm rpm 1138688 May 23 14:05 Dirnames
-rw-r--r-- 1 rpm rpm 1054310 May 23 14:05 Filemd5s
-rw-r--r-- 1 rpm rpm 24576 May 23 14:05 Installtid
-rw-r--r-- 1 rpm rpm 24576 May 23 14:05 Name
-rw-r--r-- 1 rpm rpm 45856 May 23 14:05 Packages
-rw-r--r-- 1 rpm rpm 3381240 May 23 14:05 Provenidance
-rw-r--r-- 1 rpm rpm 335872 May 23 14:05 Providersion
-rw-r--r-- 1 rpm rpm 86016 May 23 14:05 Requiredname
-rw-r--r-- 1 rpm rpm 405504 May 23 14:05 Requireversion
-rw-r--r-- 1 rpm rpm 192512 May 23 14:05 Requireversion
-rw-r--r-- 1 rpm rpm 86016 May 14 09:55 Shatheader
-rw-r--r-- 1 rpm rpm 86016 May 23 14:05 Sigmd5
-rw-r--r-- 1 rpm rpm 12288 May 23 14:05 Triggername
```