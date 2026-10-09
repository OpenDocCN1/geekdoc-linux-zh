# **The RPMS Directory**

The Red Hat distribution includes the RPMS directory containing packages. You can also find packages on the Internet and FTP sites. One website where you can find packages is **http://rpmfind.net**.

# **Installing Packages**

When you install Linux, you may install all the packages it comes with. However, it is better to install only the packages you need. Later, when you need to install additional packages, you can use your CD (or whatever source you used) to obtain additional packages. You can check if updated versions of the package have been released and install the recent version.

# **The /usr/lib/rpm/* Directory**

The */usr/lib/rpm/* directory contains the RPM tools required to manage the RPM packages. The */var/lib/rpm/* directory contains the RPM database of the installed packages. By default, the rpmrc file, which is the global RPM configuration file, is located in the */usr/lib/rpm* directory. The rpmrc file contains information of the RPM architecture compatibility. If you want the RPM settings to be applicable for a system-wide configuration, place the rpmrc file in the /etc directory. If the rpmrc file is placed as .rpmrc in the home directory of any user, then the rpm settings will be applicable only for that specific user.

# **RPM Commands**

![](bbox=[0.04, 0.5, 0.15, 0.58])

Common RPM package management commands enable you to perform package management tasks.

Frequently used RPM package management commands are given in the following table.

| Command | Enables You To |
| :--- | :--- |
| `rpm -i {RPM package_file}` | Install a package. |
| `rpm -F {RPM package_file}` | Reinstall the package. |
| `rpm -U {RPM package_file}` | Upgrade the package. |
| `rpm -e {RPM package_name}` | Remove the package. |