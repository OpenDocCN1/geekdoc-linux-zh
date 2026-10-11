I pointed out that you should verify your downloads using checksums whenever possible. You can generate a checksum using the sum command on the file you downloaded and compare it to the checksum provided on the web site where you obtained it.

We then reviewed the process for installing software using RPM packages. I pointed out that you have to use a package manager to manage prepackaged software, such as the Red Hat Package Manager (RPM). RPM packages are precompiled software packages that the package manager can install on your system. Because they are precompiled, you need to verify that a given package is compatible with your system before installing it. To do this, you need to review the package filename. The package filename includes the following information:

+   - Package name
+   - Version number
+   - Release number
+   - Compatible distribution (optional)
+   - Architecture type

You can enter rpm --checksig to verify the digital signature of an RPM package before you install it. You can then enter rpm -i to actually install the package file on your system. I pointed out that many RPM packages are dependent on other packages being installed on the system for them to work properly. If these packages aren't present, the software won't run. The rpm utility automatically checks to see if dependent software is installed before it installs a new package. You can also run rpm -test to check for dependencies before installing.

I then discussed the process you need to follow to uninstall software from your Linux system. To uninstall an RPM package, you enter rpm -e.

I also pointed out that you can use the rpm command to update an existing package to a newer version. This is done using the rpm -U command. The rpm command can also be used to query and verify RPM packages. To query a package, you use the -q option with rpm. To verify a package, you use the -V option. If you determine that a package has been damaged, you can re-install an existing package by entering rpm -U --replacepkgs.

Next, we looked at using the yum command as an alternative to rpm. I pointed out that yum allows you to download and then install a package and all of its dependencies with a single command. We looked at commonly used yum commands, such as yum install packagename and yum remove packagename. If you only want to download the file but not install it, you can use the yumdownloader command instead of yum. We looked at the yum.conf file, which is the configuration file for yum. It defines such things as the software repository URLs and their names where yum will search for packages, the directory (cachedir) where downloaded packages will be saved, and where the yum log file (logfile) will be saved. I also pointed out that repository information can be stored in this file or in separate files named filename.repo in the /etc/yum.repos.d directory.

I then discussed the process you need to follow to install software from source code. I pointed out that most software installed in this manner is distributed in tarball format. After downloading the file, you need to use the tar -xzvf command to extract the files