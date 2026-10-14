# Review Questions

+   1. Name the two widely used software package formats for Linux, with the file extension used for each type and the command-line utility used to manage each.

+   2. Within the system-config-packages utility, selecting details and checking a package name:
+   a. causes that package to immediately be installed
+   b. verifies whether that package is currently installed correctly
+   c. marks the package as one that will be installed after the Update button is selected after other categories of packages have also been reviewed for possible changes
+   d. has no effect as this utility only reflects the choices made during a custom installation.

+   3. Which option of the rpm command is used to verify the cryptographic signature so you know for certain the person or organization that created a given rpm file?
+   a. --checksig or -K
+   b. -V
+   c. -qa
+   d. -Uvh

+   4. If you know the name of a package, you can see a list of all the files contained in that package using this command:
+   a. rpm -qf packagename
+   b. rpm -Uvh packagename
+   c. rpm -ql packagename
+   d. rpm -e packagename

+   5. If you have an rpm-format file stored on your system, and then you use the rpm command to install that software package, the rpm file will no longer be on your system. True or False?

+   6. When querying an installed package using the -q option, you use ______________ ; when installing an rpm file using the -U option, you use
+   a. the name of the package alone; the complete file name with all version numbers and file extensions
+   b. the name of the package alone; the name of the package alone
+   c. the name of the package with all version numbers and file extensions; the complete file name as it appears in an ls listing
+   d. the name of the package alone; the -h option as well to check for incompatibilities during the installation process