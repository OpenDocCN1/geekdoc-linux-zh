contrib (contributions) includes open source software that cannot function without some non-free elements.

+   * Kali maintains several repositories including: kali-rolling, which is the main repository for end-users and should always contain installable and recent packages; kali-dev, which is used by Kali developers and is not for public use; and kali-bleeding-edge, which often contains untested and un-vetted packages automatically built out of the upstream Git (or Subversion) repository less than twenty-four hours after they have been committed.
+   * When working with APT, you should first download the list of currently-available packages with `apt update`.
+   * You can add a package to the system with a simple `apt install package`. APT will automatically install the necessary dependencies.
+   * To remove a package use `apt remove package`. It will also remove the reverse dependencies of the package (i.e. packages that depend on the package to be removed).
+   * To remove all data associated with a package, you can "purge" the package with the `apt purge package` command. Unlike a removal, this will not only remove the package but also its configuration files and sometimes the associated user data.

We recommend regular upgrades to install the latest security updates. To upgrade, use `apt update` followed by either `apt upgrade`, `apt-get upgrade`, or `aptitude safe-upgrade`. These commands look for installed packages that can be upgraded without removing any packages.
For more important upgrades, such as major version upgrades, use `apt full-upgrade`. With this instruction, apt will complete the upgrade even if it has to remove some obsolete packages or install new dependencies. This is also the command that you should use for regular upgrades of your Kali Rolling system. Review the pros and cons of updates we outlined in this chapter.
Several tools can be used to inspect Debian packages:

+   * `dpkg --listfiles package` (or `-l`) lists the files that were installed by the specified package.
+   * `dpkg --search file` (or `-S`) finds any packages containing the file or path passed in the argument.
+   * `dpkg --list` (or `-l`) displays the list of packages known to the system and their installation status.
+   * `dpkg --contents file.deb` (or `-c`) lists all the files in a particular .deb file.
+   * `dpkg --info file.deb` (or `-i`) displays the headers of the specified .deb file.
+   * The various `apt-cache` subcommands display much of the information stored in APT's internal database.

To avoid excessive disk usage, you should regularly sort through /var/cache/apt/archives/. Two commands can be used for this: `apt clean` (or `apt-get clean`) entirely empties the direc-