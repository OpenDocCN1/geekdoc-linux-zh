+   8. A, B. Both the `rpm -i evolution-2.6.0-41.i586.rpm` command and the `rpm --test evolution-2.6.0-41.i586.rpm` command will automatically check the package for required dependencies and prompt you if any are missing.

+   9. A. The `./configure` command would be used first to generate the Makefile file. This file contains the UNINSTALL target that can then be used with the make utility to uninstall the software.

+   10. D. To erase the rpm from the system, you would enter `rpm -e evolution`.

+   11. A. The `rpm -U evolution-2.6.0-41.i586.rpm` command will upgrade the existing rpm to the newer version.

+   12. C. The `rpm -qi evolution-2.6.0-41.i586.rpm` command will query the package and display summary information on the screen.

+   13. A. The `rpm -q --whatprovides /usr/bin/perl` command displays the name of the package that provides this component.

+   14. A, C, E. The S, 5, and T in the error code indicate that there is a problem with the file’s size, MD5 checksum, and timestamp. The c indicates that the file is a configuration file, so these errors may or may not be significant.

+   15. D. The `rpm2cpio` utility can be used to create a `cpio` archive file from the `RPM` package. You can then extract individual files from the archive using the `cpio` utility.

+   16. B. The `yum install gcc` command can be used to download and install the `gcc` package on your Linux system, including all packages it is dependent upon.

+   17. A. The `yum list updates` command can be used to generate a list of available updates for all installed packages on a Linux system.

+   18. B, D. The `configure` script is used to check the local system to make sure it has the components required to install and run the software. It also creates the `Makefile` file.

+   19. A. The `make` command compiles the text-based source code into a binary executable that can be run on the system.

+   20. C. The `make install` command actually installs the program and its associated support files (such as documentation and configuration files) into the appropriate directories in the file system.

+   21. C. The `-P` option, when used with the `dpkg` command, uninstalls a specified package and deletes all of its configuration files.

+   22. A. The `apt-get install 3dchess` command can be used to download and install the `3dchess` package on your Linux system, along with all other packages it is dependent upon.

+   23. C. Static shared libraries are integrated directly into an executable file when it is initially compiled.

+   24. B. The `/etc/ld.so.cache` file is checked by applications on startup for the location of shared libraries on the Linux system.