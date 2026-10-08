output format. The following is an example of converting the RPM package for Adobe Acrobat Reader, some of which you may have heard of, to DEB format:

```
$ sudo alien --scripts --to-deb AdobeReader-enu-7.0.0-2.i386.rpm
Password:
adobereader-enu_7.0.0-3_i386.deb generated
```

Not much to see there, actually. The --scripts option tells alien to convert any or post-installation scripts found in the package, although the validity of the scripts can't be guaranteed—you should carefully make sure that nothing goes amiss when you install the package. The --to-deb option tells alien to generate a Debian package from the input package. If you want to see detailed output, you can add the --to-alien command line, by which you're likely to see more output than you actually care about.

Before installing a converted package, you can verify its integrity using dpkg, in the following example:

```
$ dpkg --info adobereader-enu_7.0.0-3_i386.deb
dewian package, version 2.0.
size 3932742 bytes: control archive= 7436 bytes.
1, 11 lines control
2006 bytes, 207 lines md5sums
1340 bytes, 60 lines * postinst #/bin/sh
980 bytes, 45 lines * postrm #/bin/sh
211 bytes, 7 lines shlibs
Package: adobereader-enu
Version: 7.0.0-3
Section:
Priority: extra
Architecture: i386
Installed-Size: 91916
Maintainer: <root@vmdesktop>
Description: Adobe Reader for Linux. An application that reads a
PDF document. Adobe Reader 7.0.0 can read documents in PDF format.
Adobe Reader also allows you to search within PDF files, search
for PDF files on the internet and participate in collaborative document reviews.
(Converted from a rpm package by alien version 8.64.)
```

This matches quite nicely with information about the original RPM package that was produced on one of my other systems:

```
$ rpm -q -v -p AdobeReader-enu-7.0.0-2.i386.rpm
Name : AdobeReader_enu Relocations: /usr/local/Adobe/Acrobat7.0
Version : 7.0.0 Vendor: Adobe Systems, Incorporated
Release : 2 Build Date: Mon 28 Mar 2005 06:34:42 AM EST
```