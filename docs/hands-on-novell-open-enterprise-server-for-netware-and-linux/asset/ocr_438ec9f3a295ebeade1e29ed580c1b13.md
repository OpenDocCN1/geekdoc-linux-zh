+   1. If necessary, log in to your SUSE Linux server with your user name and password.
+   2. Start the YaST utility and enter the password for your root account.
+   3. In the left pane, click the System icon, and then check the Runlevel Editor option in the right pane.
+   4. Click the Expert Mode option button and record the default run level:
+   
+   _________________________
+   5. Click the Set default runlevel after booting to list arrow, and record the run level options:
+   
+   _________________________
+   6. Click the Back button twice to return to the YaST System menu.
+   7. Exit YaST, and stay logged in for the next activity.

# RPM Package-Related Operations

Installing applications can require a number of steps, such as determining what support modules an application needs, decompressing software modules, performing the actual installation procedure, and then testing the application. Just as Windows has wizards to help with installation procedures, Linux offers several software package tools to help administrators install applications. The application tool that Linux administrators use most often is RedHat Package Manager (RPM). RPM has the following features that make it an excellent software package manager:

+   ■ Noninteractive, scriptable installatons—Provides a set of tools you can use to perform scriptable installations of software packages.
+   ■ Verification of correct installation—Includes several methods for verifying installed files so that administrators can verify that software is installed correctly and hasn’t been modified since installation.
+   ■ Dependency tracking—With this feature, administrators can determine whether additional updates or modules need to be installed on the Linux server before installing the package.
+   ■ Digitally signed packages—Allows all packaged software to be digitally signed using public key technology, so that you can verify the authenticity of software and help prevent installation of Trojan programs.

To use RPM to install a software package, first copy the package to a temporary work directory in the Linux file system. RPM software packages have a name in the following format: name-version-release.architecture.rpm. Each part of the RPM name describes the package component:

+   ■ Name—Indicates the software packaged in the .rpm file
+   ■ Version—Version number not required but can be used in the .rpm file
+   ■ Release—An optional component that specifies the revision of the version number
+   ■ Architecture—Indicates the computer platform the software package is written for; typical values include the following:

+   – i686: The package can be used on any Pentium class or higher 32-bit CPU; default value for SUSE Linux.
+   – i686: The package can be used on any 686-class 32-bit Intel-compatible CPU.
+   – noarch: The package doesn’t contain binary code.
+   – nosrc: The package contains code and no source is available.
+   – src: The package contains items such as the source code, patches, and spec file you need to build a binary package.

After you copy the file to a work directory, you can use the cd/r command to change to the directory and then use the rpm package_name.rpm command. You can also install rpm packages from a graphical interface by using YaST. In Appendix B, you have the opportunity to practice using the YaST utility and rpm command to install packages, such as ifolder.