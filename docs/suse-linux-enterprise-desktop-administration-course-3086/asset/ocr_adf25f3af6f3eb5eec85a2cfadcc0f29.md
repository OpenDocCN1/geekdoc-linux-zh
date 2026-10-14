+   11. List all files included in the installed gcal package by entering
+   
+       `rpm -ql gcalctool`
+   
+   12. Log out as root by entering
+   
+       `exit`
+   
+   13. Close the terminal window.

# Summary

+   - The easiest way to install, update, manage, and uninstall software packages after a SUSE Linux installation is to use the Software Management module of YaST. Although YaST obtains software packages from your installation media by default, you can specify other installation sources such as a network server or software repository on the Internet.
+   - You can use the Online Update module of YaST to obtain the latest software updates for your SUSE Linux system provided that you have a valid SUSE Customer Center subscription.
+   - Most Linux software is in Red Hat Package Manager (RPM) format. RPM package file names include the software version, release number, architecture, and the rpm extension.
+   - SUSE Linux maintains a database of all RPM installed software in the `/var/lib/rpm` directory and backs up this database to the `/var/adm/backup/rpmdb` directory on a daily basis.
+   - You can install, remove, verify, and find information about RPM software packages using the `rpm` command in a terminal or using YaST in a desktop environment.
+   - To configure the default options for the `rpm` command, you can edit the `/etc/rpmrc` and `~/.rpmrc` files.
+   - Periodically, you should verify the contents of packages using the `-V` (or `--verify`) option to the `rpm` command.

# Key Terms

| Term | Definition |
|---|---|
| `/etc/rpmrc` | A file that contains configuration information that is written to the `/usr/lib/rpm/rpmrc` file. |
| `/etc/sysconfig/backup` | The configuration file that controls automatic system backups. |
| `/usr/lib/rpm/rpmrc` | The main RPM configuration file. |
| `/var/adm/backup/rpmdb` | The directory that stores backup copies of the RPM database. |
| `/var/lib/rpm` | The directory that stores the RPM database. |
| `~/.rpmrc` | A file that contains configuration information that is written to the `/usr/lib/rpm/rpmrc` file. |
| **Installation Source** | A YaST module that allows you to specify the source of software packages available for installation. |