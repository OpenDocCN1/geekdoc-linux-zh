This book is about Linux system administration. It focuses upon a specialized set of administrative tasks—those relating to operating the computer as a server for a small network. There are certain important administrative tasks that don’t fall under the heading of any of the specific networking tasks I’ve covered in the book to this point, however. I cover these tasks in this chapter.

I cover some administrative tasks elsewhere in this book. For instance:

+   - Chapter 5, “Basic Linux Configuration,” covers installation and the handling of user accounts.
+   - Chapter 6, “Compiling a Kernel for Networking,” covers the important topic of kernel compilation.
+   - Chapter 13, “Using Linux to Back Up Client Machines,” includes information on backing up the server itself, as well as client computers.
+   - Chapter 14, “Preparing to Share a Printer,” covers printer configuration.
+   - Chapter 24, “Maintaining a Secure System,” covers system security issues.

You can also consult a book such as Pitts & Ball’s Red Hat Linux 6 Unleashed from Sams for more information on running a Linux system.

# Installing and Removing RPM Packages

In the Linux community, software programs are often referred to as packages. A package includes not just the program, but also documentation, configuration files, support programs, and so on. For ease of distribution, packages typically come in a single file.

Three distribution formats are common for Linux packages:

+   - Tarballs—A tarball is a group of files bound together in a tar archive and compressed with gzip. Tarballs usually have .tgz or .tar.gz extensions. They can contain either binaries (compiled programs) or source code that you must compile yourself. I describe the process of compiling programs later in this chapter.
+   - Debian packages—The Debian distribution uses its own package format. These packages’ filenames typically end in .deb. Debian package files are more sophisticated than tarballs because Debian’s format includes information on the package contents, including dependency information that tells the system upon what other packages any given package relies. For instance, the package earth.deb can record that it relies upon sun.deb. That way, if you attempt to install earth.deb without sun.deb, the system can tell you that you must first locate and install sun.deb.
+   - RPM packages—Red Hat introduced the Red Hat package manager (RPM) format to accomplish much the same task as the Debian package format. RPM, like Debian’s format, supports dependencies and other package information. Conceptually, these two formats are quite similar to one another, although they aren’t compatible.