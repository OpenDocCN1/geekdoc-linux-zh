previously, the control file consists of a series of stanzas. The first stanza will always begin with Source: and will include information on the source package. Each following stanza will describe a single binary package. In this case, there is only one binary package, which, like the source package, is named most. This situation—a single source package creating a single binary package of the same name—is a very common case.

The rules file is a GNU Make makefile and contains all of the makefile rules to create and build a package. Running debian/rules binary from within the unpacked source package directory results in the creation of a Debian package in one directory above (../) if your system has all the necessary dependencies installed. In most cases, the software will build and “install” into a series of subdirectories within the debian directory; these files in their temporary location will then be included as the package contents.

Additional files in the debian directory include the copyright file, the changelog for the package, optional scripts to be run after and before installation or removal of the package, and extra configuration data plus anything else the packager would like to include.

# Binary Packages

Debian binary packages are very simple in format, so it is unnecessary to spend much time on them here. More importantly, they are almost never manipulated by hand. Binary packages are merely installed and removed. Changes to a binary package are made first in the source package and then new, changed binary packages are rebuilt. In Ubuntu and Debian, binary packages are a single file in an archive in the ar format. In the archive is debian-binary, which contains a series of lines, separated by newlines. At the moment, only the format version number is included. The second member of the archive is named control.tar.gz, and it contains the package control information (as described previously). The third and last member is called data.tar.gz, and it contains the file system archive as a gzipped tar archive.

# Package Management in Ubuntu

The administrator of every Ubuntu installation—servers and desktops—must learn the basic mechanics of package management. As administrators need to find new software to solve particular problems, metadata in