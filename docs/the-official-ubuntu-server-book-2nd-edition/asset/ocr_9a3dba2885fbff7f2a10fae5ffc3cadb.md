software since the Ubuntu team is unable to fix the software but can only forward problem reports to the actual authors.

+   - **Universe**  
+     In universe one can find almost every piece of open source software and software available under a variety of less-open licenses, all built automatically from a variety of public sources. All of this software is compiled against the libraries and using the tools that form part of main, so it should install and work well with the software in main, but *it comes with no guarantee of security fixes and support*.

+   - **Multiverse**  
+     The multiverse component contains software that is not free, which means the licensing requirements of this software do not meet the “main” component license policy. The onus is on you to verify your rights to use this software and comply with the licensing terms of the copyright holder. This software is not supported and usually cannot be fixed or updated. Use it at your own risk.

# Using Other Repositories

As you saw when I added the Bazaar repository several sections ago, users will still sometimes want to make use of a variety of outside repositories beyond what is provided in Ubuntu. For example, users might want to install new versions of particular applications or libraries from the development release of Ubuntu but might not want to upgrade all of their packages to the latest version.

The quasi-official “backports” repository in Ubuntu is a useful resource. It contains versions of software from the development version of Ubuntu that have been backported to install cleanly on stable versions of Ubuntu. You can add the backports by installing a DEB package by hand in a one-by-one with dpkg or by adding an extra line to your sources.list. Information on doing both can be found on the Ubuntu Web site at https://help.ubuntu.com/community/UbuntuBackports.

One reason that many users choose to go the à la carte method—that is, the method of downloading packages by hand and installing them with dpkg—as opposed to just adding the repository is because of a limitation in the