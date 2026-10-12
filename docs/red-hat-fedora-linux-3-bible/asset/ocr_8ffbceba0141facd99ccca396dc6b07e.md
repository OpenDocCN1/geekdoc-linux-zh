and compressed using the gzip command (.gz). You use these two commands (or just the tar command with the -z option) to expand and uncompressed the packages when you are ready to install the applications.

Between the version number and the .tar.gz extension there can be optional tags, separated by dots, which provide specific information about the contents of the package. In particular, if the package is a binary version, this information provides details about where the binaries will run. In the third line, the optional .src tag was added because the developer wanted to differentiate between the source and binary versions of this package. In the fourth line, .bin.SPARC detail indicates that it is a binary package, ready to run on a SPARC workstation. The final line indicates that it is a binary package, consisting of statically linked ELF format executables.

# Using Binary RPMs versus Building from Source

Binaries created in RPM format are easily installed, managed, and uninstalled using Red Hat tools. This is the recommended installation method for Fedora Core novices. Sometimes, however, building an application from source code may be preferable. Here are some arguments on both sides:

+   - RPM — Installing applications from an RPM archive is easy. After the application is installed, there are both shell commands and GUIs for managing, verifying, updating, and removing the RPM package. You don't need to know anything about Makefiles or compilers. When you install an RPM package, RPM tools even check to make sure that other packages that the package depends on are installed. Because Red Hat has released RPM under the GPL, other Linux distributions also use it to distribute their software. Thus, most Linux applications are, or will be, available in RPM format.

+   - Source code — Not all source-code packages are made into RPM binaries. If you use RPM, you may find yourself with software that is several versions old, when you could simply download the latest source code and run a few tar and make commands. Also, by modifying source code, you can tailor the package to better suit your needs.

Source code for RPM binary packages included with Fedora Core are included on the DVD that comes with this book. (The source code is also available on the CD set you can order using the coupon at the end of this book.) You can modify the source code yourself and rebuild the RPM binaries. The rebuilt binaries can be tuned to your hardware and include the features you want with the package. For more information on RPMs, refer to the Red Hat RPM Guide by Eric Foster-Johnson (Red Hat Press/Wiley, 2003).

Here is a breakdown of the parts of a package name: