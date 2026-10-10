# CHAPTER 14

# Installing Additional Software

# IN THIS CHAPTER

+   - Introduction to Packages
+   - Installing Packages
+   - Removing Packages

+   - Introduction to Ports
+   - Installing and Removing Ports
+   - Upgrading a Port

+   - Updating and Maintaining
+   Your Ports
+   - Fresh Ports

Up until now, we have covered topics that are largely applicable to many different types of Unix systems. Pretty much any such system, whether commercial or open source, operates the same way regarding the filesystem structure, process automation, and general administration. What sets FreeBSD apart from its BSD brethren (Linux and commercial Unix software) is the model by which the administrator adds new software.

With Solaris, if you want to add a new piece of the software to the system, you have to find a precompiled binary for your particular platform and install it yourself (usually without the aid of installers that help you put it in the right place), because Solaris typically doesn't come with *gcc* (the standard GNU C/C++ compiler). Other systems, such as IRIX and HP-UX, do come with *gcc*, but you still have to find the source code for the program you want to install and then run its configuration script, compile it (a step that's often much easier said than done), and install it.

Different flavors of Linux take this a step further with the concept of *packages*, which are essentially all-in-one bundles that contain the proper binary for your system as well as any required libraries, plus the necessary information about where to install everything. The Red Hat Package Manager (RPM) system is a GNU-licensed packager that runs on many systems, including FreeBSD. Its popularity was a large part of what pushed Red Hat to the top of the Linux distributions, edging out the previous favorite, Slackware. RPM allows administrators to keep tabs on their installed software and to upgrade, deinstall, and add new packages with unprecedented ease.