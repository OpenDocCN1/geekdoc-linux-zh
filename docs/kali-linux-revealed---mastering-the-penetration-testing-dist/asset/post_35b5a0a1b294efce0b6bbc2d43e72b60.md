
The dpkg --contents file.deb (or -c) command lists all the files in a particular .deb file:

```
$ dpkg -c /var/cache/apt/archives/gpgnu_1.4.18_amd64.deb
drwxr-xr-x root/root      0 2014-12-04 23:03 /
drwxr-xr-x root/root      0 2014-12-04 23:03 /lib/
drwxr-xr-x root/root      0 2014-12-04 23:03 /lib/udev/
drwxr-xr-x root/root      0 2014-12-04 23:03 /lib/udev/rules.d/
-rw-rw-r-- root/root   2711 2014-12-04 23:03 /lib/udev/rules.d/60-gpgnu.rules
drwxr-xr-x root/root      0 2014-12-04 23:03 /usr/
drwxr-xr-x root/root      0 2014-12-04 23:03 /usr/lib/
drwxr-xr-x root/root      0 2014-12-04 23:03 /usr/lib/gpgnu/
-rwxr-xr-x root/root   39328 2014-12-04 23:03 /usr/lib/gpgnu/gpgkeys_ldap
drwxr-xr-x root/root   92872 2014-12-04 23:03 /usr/lib/gpgnu/gpgkeys_hkp
-rwxr-xr-x root/root   47576 2014-12-04 23:03 /usr/lib/gpgnu/gpgkeys_finger
-rwxr-xr-x root/root   86468 2014-12-04 23:03 /usr/lib/gpgnu/gpgkeys_curl
drwxr-xr-x root/root    3499 2014-12-04 23:03 /usr/lib/gpgnu/gpgkeys_mailto
drwxr-xr-x root/root      0 2014-12-04 23:03 /usr/bin/
drwxr-xr-x root/root   60128 2014-12-04 23:03 /usr/bin/gpgsplit
-rwxr-xr-x root/root  1012688 2014-12-04 23:03 /usr/bin/gpgnu
[]
```

The dpkg --info file.deb (or -i) command displays the headers of the specified .file:

```
$ dpkg -I /var/cache/apt/archives/gpgnu_1.4.18_amd64.deb
 debian package, version 2.0.
size 114832 bytes: control archive=3422 bytes.
1264 bytes,      26 lines control
4521 bytes,      65 lines mdsums
479 bytes,       13 lines * postinst #!/bin/sh
473 bytes,       13 lines * prereinst #!/bin/sh
Package: gnupg
Version: 1.4.18
Architecture: amd64
Maintainer: Debian GnuPG-Maintainers <pkg-gpgnu-maint@lists.debian.org>
Installed-Size: 4888
Deps: gpgv, libbz2-1.0, libc6 (>= 2.15), readline6 (>= 6.0), libusb-0.1-4 (>=2:0.1.12), zlib1 (>= 1:1.14)
Recommends: gpgnu-curl, libaptd-2.4.2 (>= 2.4.7)
Suggests: gpgnu-doc, libpsclient, parcimonie, xonload | imagemagick | eog
Section: utils
Priority: important
Multi-Arch: foreign
Homepage: http://www.gpgnu.org
Description: GNU privacy guard - a free PGP replacement
GnuPG is Gnu's tool for secure communication and data storage.
It can be used to encrypt data and create digital signatures.
It includes an advanced key management facility and is compliant
with the proposed OpenPGP Internet standard as described in RFC 4880.
[...]

You can also use dpkg to compare package version numbers with the --compare-versions option, often called by external programs, including configuration scripts executed by dpkg itself. This option requires three parameters: a version, a comparison operator, and a second version number. The different possible operators are: lt (strictly less than), le (less than equal to), eq (equal), ne (not equal), ge (greater than equal to), and gt (strictly greater than). If the comparison is correct, dpkg returns 0 (success); if not, it gives a non-zero return value (indicating failure). Consider these comparisons:

```
$ dpkg --compare-versions 1.2-3 gt 1.1-4
$ echo $0
$ dpkg --compare-versions 1.2-3 lt 1.1-4
$ echo $1
$ dpkg --compare-versions 2.6.0pre3-1 lt 2.6-1
$ echo $1
```

Note the unexpected failure of the last comparison: for dpkg, the string "pre" (usually denoting a pre-release) has no particular meaning, and dpkg simply interprets it as a string, in which case "2.6.0pre3-1" is alphabetically greater than "2.6-1". When we want a package's version number to indicate that it is pre-release, we use the tilde character, "~".

```
$ dpkg --compare-versions 2.6.0~3-1 lt 2.6-1
$ echo $0
```

## Querying the Database of Available Packages with apt-cache

The apt-cache command can display much of the information stored in APT's internal database. This information is sort of cache since it is gathered from the different sources listed in the sources file. This happens during the apt update operation.

Cache is a temporary storage system used to speed up data access when the usual access method is expensive (performance-wise). This concept can be applied in numerous situations and at different scales, from the core processors to high-end storage systems. In the case of APT, it stores copies of all files (in /var/lib/apt/lists/) and searches are done within those files. Similarly, /var/cache/apt/archives/ contains copies of already downloaded packages to avoid downloading them if you need to reinstall them.

To avoid excessive disk usage when you upgrade frequently, you should regularly sort throughvar/cache/apt/archives/ directory. Two commands can be used for this: apt clean (or apt-get clean) entirely removes the directory; apt autoclean (apt-get autoclean) only removes packages that can no longer be downloaded because they have disappeared from the mirrors. Note that the configuration parameter APT::Clean-Installed can be used to prevent the removal of files that are currently installed. Also, note that this matters when you use other tools.

The apt-cache command can do keyword-based searches with apt-cache search. It can also display the headers of the package's available versions with apt-cache search. This command provides the package's description, its dependencies, and the name of its maintainer. This feature is particularly useful in determining the packages that are installed via meta-packages, such as kali-linux-wireless, kali-linux-web, and kali-linux-gpu. Note that apt search, apt soft, and aptitude search work in the same way.

## Alternative: search

apt-cache search is a very rudimentary tool, basically implementing grep on package descriptions. It often returns many too results or no at all when many keywords are included.

apt search, on the other hand, provides better results, sorted by relevancy. It uses the Xapian search engine and is part of the apt-xapian package, which indexes all package information (and more, like the .desktop files from all Debian packages). It knows about that and results in matter of milliseconds.

### apt search forensics

5 results found:

- 100% autopsy - graphical interface to SleuthKit
- 82% forensics-colorize - show differences between files using color
- 73% diff - Powerful, efficient and modular digital forensic framework
- 53% gpart - Guess disk partition table, find lost partitions

More terms: colorize partitions file disklabel autopsy-digital differences
More tags: admin::forensics security::forensics role::program admin::recovery interface::commandline admin::boot scope::utility

Some features are more rarely used. For instance, apt-cache policy displays the priorities of package sources as well as those of individual packages. Another example is apt-cache dump, which displays the headers of all available versions of all packages. apt-cache pkgnames displays the list of all the packages that appear at least once in the cache.

## 8.2.6 Troubleshooting

Sooner or later, you will run into a problem when interacting with a package. In this section, we will outline some basic troubleshooting steps that you can take and provide some tools that will lead you to a potential solution.

## Handling Problems after an Upgrade

In spite of the Kali-Debian maintainers' best efforts, a system upgrade isn't always as smooth as we would hope. New software versions may be incompatible with previous ones (for instance, their default behavior or their data format may have changed), or may slip through the cracks despite the testing performed by package maintainers and Debian unstable.

### Leveraging Bug Reports

You might sometimes find that a new version of software doesn't work at all. This generally happens if the application isn't particularly popular and hasn't been tested enough. The first thing to do is to have a look at the Kali bug tracker³ the Debian tracking system⁴ check whether the problem has already been reported. If it hasn't, you should report it yourself (see section 6.3, Filing a Bug Report) for detailed instructions. If it is already known, the bug report and the messages are usually an excellent source of information related to the bug. In some cases, a patch already exists and has been made available in the bug report itself; you can then recompile a fixed version of the package locally (see section 9.1, Modifying Kali Packages) and share their insights about it in their replies to the report; in other cases, users may have found a workaround for the problem and shared their insights which may help you work around the problem until a fix or patch is released. In a best-case scenario, the package may have already been fixed and you may find it in the bug report.

> ³http://bugs.kali.org

> ⁴https://bugs.debian.org
