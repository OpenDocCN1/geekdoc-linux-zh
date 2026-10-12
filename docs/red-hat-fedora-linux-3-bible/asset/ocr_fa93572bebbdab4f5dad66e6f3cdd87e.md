remove packages. You may, however, list installed packages, query packages for information, or verify a package’s contents without root permission.

The following sections describe how to use rpm to install and work with your RPM applications.

# ### Installing with rpm

To install an RPM archive file with the rpm command that is not yet installed on your system, most people generally use the same options they would if they were upgrading (the -U option). Here’s an example of a command line you could use to install a new RPM package.

```
# rpm -U [options] package
```

*Package* is the name of the RPM archive file. This package may be in the current directory, on a DVD or CD for example, (`/media/cdwr_dvdrom/Fedora/RPMS/whatever.rpm`), or on an accessible FTP site (for example, `ftp://sunsite.unc.edu/pub/linux/games/strategy/galaxls-1.7-1.i386.rpm`)

> **CAUTION**: Interrupting rpm during a package installation can leave stale lock files and possibly corrupt the database. As a result, subsequent rpm commands may hang. If this happens, you can probably correct the problem by removing old database locks. If that doesn’t work, you can also try checking whether the database is corrupt and, if so, rebuilding the RPM database. Rebuilding the database can take a long time, so only do it if the other options don’t clear up the problem. Here’s how to remove lock files, check the database, and rebuild the database (as root user):
> # rm -f /var/lib/rpm/__db*
> # db_verify /var/lib/rpm/Packages

Along with the -U option, you can use the following options to get feedback during a new installation:

+   - **-v** — Prints debugging information during installation. This is a good way to see everything that happens during the install process. (This output can be long, so you may want to pipe it to the less command.) You can get more information by adding multiple -v options (for example, -vv).

+   - **-h** — Prints 50 hash marks (#) as the package unpacks. The intent is to see the progress of the unpacking process (so you can tell if the program is still working or stalled).

+   - **-percent** — Prints the percentage of the total package that has been installed throughout the install process.

Before installing a package, rpm checks to make sure that it is not overwriting newer files or installing a package that has dependencies on other packages that are not installed. The following install options can be used to override conditions that may otherwise cause the installation to fail.