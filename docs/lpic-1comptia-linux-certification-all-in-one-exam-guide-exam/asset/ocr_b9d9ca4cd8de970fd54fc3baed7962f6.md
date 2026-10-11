+   • The make uninstall command is typically used to uninstall an executable installed from source.
+   • Distributions based on the Debian distribution use the Debian Package Manager (dpkg).
+   • Debian packages use a naming convention that is similar to that used by RPM packages.
+   • Debian packages include dependency information.
+   • You use the dpkg command to install, uninstall, query, and verify Debian packages in much the same manner as the rpm command.
+   • The apt-cache command is used to query package information from the Debian package database (called the package cache).
+   • The apt-get command automatically downloads and installs packages (along with all dependent packages) for you.
+   • The aptitude utility uses a text-based, menu-driven interface to manage Debian packages.
+   • Applications running on a Linux system can share code elements called shared libraries.
+   • Linux applications can use either dynamic or static shared libraries.
+   • The dynamic shared library configuration file is /etc/ld.so.conf.
+   • The /etc/ld.so.conf file contains a list of paths in the file system where shared library files are stored.
+   • To view a list of all shared libraries available on your Linux system, enter ldconfig -p at the shell prompt.
+   • You can view the shared libraries required by a specific application by entering ldd -v executable_filename at the shell prompt.
+   • The library cache is /etc/ld.so.cache.
+   • The ld.so.cache file contains a list of all the system libraries and is refreshed when the system is initially booted.
+   • If you add library files to a directory not listed in the ld.so.conf file, you must add them and then use the ldconfig command to rebuild the library cache manually.
+   • You can also add a new library file path to the LD_LIBRARY_PATH environment variable.

# ## Questions

+   1. What type of software can be managed with a graphical software utility, such as YaST? (Choose two.)
+   	A. RPM packages
+   	B. Text-based script files