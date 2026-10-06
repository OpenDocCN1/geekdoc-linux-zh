# Part II: Using Fedora and RHEL

The value of metadata_expire determines the metadata you have from a repository expires. The default of 1800 causes metadata to expire 30 minutes after it is received.

Some packages can be installed but never updated. These packages include kernel, kernel-spm, kernel-bigmern and others, as by the default installonly_pkgs value in yum. Because kernel packages are stored separately, you can keep multiple kernel packages installed on your system. By default, the installonly_limit value of 3 in /etc/yum.conf keeps the latest three installonly_pkgs on your system, but will delete older packages of the same name as new kernel packages are added.

Here are some tips for setting up yum.conf:

+   - Getting metadata — The metadata describes the contents of a yum repository downloaded to your computer when you run the yum command. If you run the command again after the metadata expires (30 minutes by default, as described earlier), you will have to wait again the metadata downloads before you proceed.
- If you configured to access several repositories, it can take a long to repeatedly download the metadata. To get around this problem, you can extend the metadata_expire value or run yum with a -C on the command line (to use existing metadata). The downside is that if the repository data has changed, you might not getting the latest packages.
- Excluding repositories — Excluding repositories on the yum command is another way to save time by preventing unneeded metadata from being downloaded. For example, if you know the package you want is Fedora, you can disable the repository by adding --disablerepo=livna to the yum command.
- Plugins — Fedora comes with the plugins feature enabled in the yum.conf file. This file causes plugins in the /usr/lib/yum-plugins directory to be enabled. When you start out, you may have no plugins or only plugins to notify the yum-updates daemon to refresh yum metadata. For information on other available plugins, refer to the YumPlugins Wiki
http://wiki.linux.duke.edu/YumPlugins.

For more information about the yum.conf file, type man yum.conf from a shell.

# Adding repositories (/etc/yum.repos/)

When you use the yum command to request install a software package, it checks repositories listed in the /etc/yum.conf file and files in the /etc/yum.repos.d directory. By default, you use repository listings from the following:

+   - Fedora (fedora.repo) — These are all the packages that are on the DVD that comes with this book. You can install any of those packages, or updates to them, from the repositories using yum. There are thousands of software packages in this repository.