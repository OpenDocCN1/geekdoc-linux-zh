![](bbox=[0.06, 0.09, 0.94, 0.28])

Figure 4.1: Base Filesystem Hierarchy Specified by the FHS

community in general have already established the `/opt/` directory for add-on software. The following list is a compilation of best practices for installing applications.

> In the following list, `package` is the product name of an application and `provider` is a LANANA-registered vendor name.

+   * The applications of the base operating system, or “the Linux distribution,” are the only ones allowed to be installed in the `/sbin/`, `/bin/`, and `/usr/` directories.
+   * System administrators who build packages from source—either source packages (`srpm`) or tape-archives (`tar`)—should install in the `/usr/local/bin/` directory, and must avoid the temptation to install in the `system` directories.
+   * Add-on binary-only packaged applications must be installed in the `/opt/package/` or `/opt/provider/` directory. For example, the binary executables should reside in their respective `/opt/provider/bin/` directories.
+   * Manual pages for applications must be located in their respective `/opt/package/share/man/` or `/opt/provider/share/man/` directories. Documentation other than man pages should be located in the corresponding `/opt/package/share/doc/` or `/opt/provider/share/doc/` directories.
+   * Host-specific configuration files for `/opt/` binary executables should go in the `/etc/opt/package/` or `/etc/opt/provider/` directory (all host-specific system configuration files reside in these directories).