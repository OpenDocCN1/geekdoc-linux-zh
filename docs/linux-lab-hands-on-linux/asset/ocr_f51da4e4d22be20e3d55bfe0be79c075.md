# ## 09
# LAB: Softeware Management

# **OBJECTIVES**

+   1. Install and remove RPM packages
+   2. Query packages and verify their state
+   3. Manage packages using YUM
+   4. Understand the relationship between YUM and RPM
+   5. Rebuild and modify existing source RPMS

# **REQUIREMENTS**

P-IV class PC with FC6 or RHEL- 5, and Linux Distro CD/DVD.

# **CONCEPT**

Linux distributions use the popular Redhat Package Manager or RPM, system of adding or removing programs. Almost all Linux users will encounter the desire to add software to their computer. or remove a program that came with their version of Linux. You can also querying the package to know the status of the RPM. The query package systems offer many benefits. As a user, you can find what packages are installed on the system and their versions. While working with Linux you can develop a real taste for YUM (Yellow dog Updater Modified), an automatic update and package installer/remover for RPM systems.

# ### RPM Overview

RPM is a powerful command line driven package management system capable to install, uninstall, verify, query, and update computer software packages. Each software package consists of an archive of files along with information about the version and description of the package.

This lab uses rpm to deals with:

+   - Installing software
+   - Querying software
+   - Removing software

# ### Basic RPM Commands

The basic RPM commands are as follows:

+   - `~U`: Lets you update or install the selected package. This can be done via http or ftp in addition to using local files.