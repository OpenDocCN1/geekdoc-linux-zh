
previously, the control file consists of a series of stanzas. The first stanza will always begin with Source: and will include information on the source package. Each following stanza will describe a single binary package. In this case, there is only one binary package, which, like the source package, is named most. This situation—a single source package creating a single binary package of the same name—is a very common case.

The rules file is a GNU Make makefile and contains all of the makefile rules to create and build a package. Running debian/rules binary from within the unpacked source package directory results in the creation of a Debian package in one directory above (../) if your system has all the necessary dependencies installed. In most cases, the software will build and “install” into a series of subdirectories within the debian directory; these files in their temporary location will then be included as the package contents.

Additional files in the debian directory include the copyright file, the changelog for the package, optional scripts to be run after and before installation or removal of the package, and extra configuration data plus anything else the packager would like to include.

## Binary Packages

Debian binary packages are very simple in format, so it is unnecessary to spend much time on them here. More importantly, they are almost never manipulated by hand. Binary packages are merely installed and removed. Changes to a binary package are made first in the source package and then new, changed binary packages are rebuilt. In Ubuntu and Debian, binary packages are a single file in an archive in the ar format. In the archive is debian-binary, which contains a series of lines, separated by newlines. At the moment, only the format version number is included. The second member of the archive is named control.tar.gz, and it contains the package control information (as described previously). The third and last member is called data.tar.gz, and it contains the file system archive as a gzipped tar archive.

## Package Management in Ubuntu

The administrator of every Ubuntu installation—servers and desktops—must learn the basic mechanics of package management. As administrators need to find new software to solve particular problems, metadata in the packaging system can be a great place to start. When administrators want to install new software, the packaging system provides the best way to do so. The Ubuntu package system will also allow users to install and remove software, check for updates—and for security updates in particular—and install these updates. Finally, when a new release of Ubuntu is made, the packaging system will allow administrators to update their systems.

Ubuntu provides a variety of different tools for package management. On a desktop Ubuntu system, users' interaction with the package management system is primary through a little icon on the desktop that alerts them to new releases of software and through the graphical Add/Remove Programs application and a second graphical package management program called Synaptic that provides functionality to let users browse the package archives. Since these programs are covered in depth in The Official Ubuntu Book and because the focus of this book is servers, this section focuses on the command-line tools for package browsing and management.

Most server administrators primarily use tools in the APT family that handle high-level package management. The original tool developed for this purpose was apt-get. Aptitude is a frequently used alternative to apt-get that provides both an interactive front end and that takes most of the default apt-get commands. Many of the commands described in the rest of this chapter that call aptitude can also be used with apt-get with little or no difference in either output or behavior. The primary differences are in the ways that the systems resolve complicated dependency situations and certainly would not affect the reasonably simple operations described here.

## Staying Up-to-Date

Each Ubuntu system stores a list of package repositories in /etc/apt/sources.list. This describes the list of “places” where your package managers—originally just APT but now several other tools—will look for updated versions of software. These sources may include local repositories on your file system, a CD in your computer, or—as is common in the vast majority of situations—a network location. To update the system’s list of packages, you can run apt-get update or aptitude update.

This command downloads the latest updated package lists for all repositories listed in your /etc/apt/sources.list files and checks any cryptographic
