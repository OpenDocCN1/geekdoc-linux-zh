uninstalling, and it will use local files with the extension .rpm to install or upgrade packages.

+   * **yum (Yellowdog Updater Modified)**: The primary tool for getting, installing, deleting, and querying packages from software repositories. This tool will be responsible for downloading the package and the dependencies needed to install the software requested. It allows the update or upgrade of the full system.
+   * **dnf (Dandified YUM)**: The newest version of YUM, having compatibility with the YUM command and options. It is faster than the original yum, is more extensible, and resolves the dependencies in a better way.

The De bian package is the package format for Debian, Ubuntu, and derivatives. The extension for the packages is .deb. The main tools to operate with the De bian packages are as follows:

+   * **dpkg**: The main tool to query, install, build and remove De bian packages. It acts as a frontend for the low-level commands dpkg-query (for listing) and dpkg-deb (to install software).
+   * **apt-get**: One of the popular tools for handling packages from software repositories. It allows to install, update, reinstall, and remove software in the system.
+   * **apt-cache**: This command is used to search packages in the software repositories. The system will keep a local copy of the list of the available packages, and this tool will query this local database to search for packages, search files inside packages or obtain information about a package.
+   * **apt**: Provides a high-level interface for package management. Using this command simplifies the use of only one command for the installation (apt-get tasks) or manipulation of packages and the search or obtaining package information (apt-cache tasks).

# # Commands to operate with RPM packages

# ## Command rpm

This command as described previously is the main command to operate with RPM packages. It contains multiple options depending on the action required. The main actions and syntax are shown in table 4.16:

| Action | Syntax |
|---|---|
| Querying and verifying | rpm -q/--query [select options] [query options] [package] |
| Installing packages | rpm -i/--install [install-options] package.rpm |