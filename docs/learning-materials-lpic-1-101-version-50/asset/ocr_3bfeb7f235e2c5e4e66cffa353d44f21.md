In the output above, the repository id is shown on the first column (repo id) of each line. Use only the part before the first /, so the id for the CentOS-7 - Updates repo is updates, and not updates/7/x86_64.

```
# yum-config-manager --disable updates
```

The command above will disable the updates repo. To re-enable it use:

```
# yum-config-manager --enable updates
```

> NOTE  Yum stores downloaded packages and associated metadata in a cache directory (usually /var/cache/yum). As the system gets upgraded and new packages are installed, this cache can get quite large. To clean the cache and reclaim disk space you can use the yum clean command, followed by what to clean. The most useful parameters are packages (yum clean packages) to delete downloaded packages and metadata (yum clean metadata) to delete associated metadata. See the manual page for yum (type man yum) for more information.

# DNF

dnf is the package management tool used on Fedora, and is a fork of yum. As such, many of the commands and parameters are similar. This section will give you just a quick overview of dnf.

# Searching for packages

+   dnf search PATTERN, where PATTERN is what you are searching for. For example, dnf search unzip will show all packages that contain the word unzip in the name or description.

# Getting information about a package

+   dnf info PACKAGENAME

# Installing packages

+   dnf install PACKAGENAME, where PACKAGENAME is the name of the package you wish to install. You can find the name by performing a search.

# Removing packages

+   dnf remove PACKAGENAME

# Upgrading packages

+   dnf upgrade PACKAGENAME to update only one package. Omit the package name to upgrade