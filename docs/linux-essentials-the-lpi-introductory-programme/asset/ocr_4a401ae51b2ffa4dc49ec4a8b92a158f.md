# 12.4  Package Management

Contemporary Linux distributions normally consist of a multitude (typically thousands) of “packages”, each containing everything necessary for a certain part of the system’s functionality: executable programs, libraries, documentation, ... When initially configuring a Linux computer, you as the administrator can specify which packages should be installed on the computer, and of course you can always add arbitrary packages from your distribution later, or remove unused ones.

The details of how functionality is split into packages depends on the distribution. With libraries, it is usual to distinguish between a “run-time package” and a “development package”. The run-time package contains the files that must be installed so other programs can use the library (like the actual dynamically loadable library in a .so file). You need to install the development package only if you intend to compile new or existing programs using the library—this contains the information the C compiler needs to use the library (“include files”), a statically linkable library for debugging, or documentation about the library’s content. If the documentation is large, it may be separated into yet another package.

For example, here is the package split for the rsvg library (which deals with SVG-format graphics) according to Debian GNU/Linux 6.0 (“Squeeze”):

librsvg2-2 The actual (run-time) library<br>librsvg2-dev Development package<br>librsvg2-bin Command-line programs<br>librsvg2-dbg Debugging information<br>librsvg2-doc Documentation<br>librsvg2-common More command-line programs<br>python-rsvg Python language binding<br>libimage-linuxrsvg-perl Perl language binding

On every Linux computer<sup>1</sup> there is a “package database” containing information about which packages the computer is aware of and which of those are currently installed. You can periodically synchronise the package database with your distribution’s “repositories”, or servers containing packages, and thus find out which of the packages on your computer are out of date because the distribution offers newer versions. The package management system then usually offers you the opportunity to selectively update the packages in question.

How well that works in practice depends (once again) on your distribution. In particular, the issue may be more complicated than it seems: The newer version of a package could, for example, require that a library (available as its own package) must be installed in a newer version, and that can lead to problems if another installed program absolutely requires the old version of the library. Sometimes it is possible that a package cannot be updated without making drastic changes elsewhere in the system. Good package management systems detect such situations and warn you as the administrator and i/or give you the opportunity to intervene.

As pointed out in Section 2.4.7, the major Linux distributions use either of two different package management systems, both of which come with their own tools and their own format for package files—the package management system of Debian GNU/Linux and its derivatives, and the RPM package manager as used by Red Hat, SUSE etc. In principle, both solve the same problem, but differ in details such as the commands used for package management. For example, on an

1Those using one of the major distributions, at any rate—there are a few distributions that seem to get by without a package management system, but these are for nerds.

Copyright © 2012 Linup Front GmbH

![](bbox=[0.7, 0.12, 0.92, 0.98])