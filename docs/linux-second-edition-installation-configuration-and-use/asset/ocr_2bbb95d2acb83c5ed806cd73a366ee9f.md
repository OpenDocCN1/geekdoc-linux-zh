# PACKAGE MANAGEMENT (RPM) 215

rpm manages a database with information on all installed packages. This database is stored in seven *.rpm files in the directory /var/lib/rpm.

Under no circumstances must the files of the rpm database be changed! To keep the files up-to-date, packages must not be removed by deleting their files, but by means of a regular reinstallation (rpm -u). The amount of space required for the four files is fairly high (on a system with 600 Mbytes, or 12 Mbytes).

Despite the *.rpm extension, the database files are not rpm packages, but in an rpm-specific binary format. The database only contains information on binary packages; packages installed via source code compilation are not included in the database.

# The rpm command

For most users, rpm only fulfils administrative tasks. Advanced users, however, can employ rpm also to assemble their own packages – this aspect of rpm usage will, however, be discussed.

Depending on the distribution, other, more user-friendly programs are available as alternatives to rpm: glint, package, yast, and so on. An overview can be found in a separate section from page 72 onward.

The advantage of direct employment of rpm is, on the one hand, you save on the overhead of other programs (without X); on the other hand, rpm provides substantially more possibilities for obtaining information on packages and their files.

```
rpm --install [options] file_name
rpm --install [options] http://ftp.server/file_name
```

-i --install installs the specified package. If it is a binary package, it is installed at the predefined location in the root directory. The second variation automatically establishes an FTP connection.

If the additional option --test is used, rpm does not perform any changes, but merely displays what would happen during an actual installation.

The installation location can be changed by means of the additional option --root directory.

With the --noscripts option, automatic execution of installation programs is disabled. This may, however, lead to the consequence that the program you just installed not work as expected.

In the current version, it is unfortunately impossible to install only a single file or a selection of files. You can only install the entire package (or nothing). One possible remedy is the mc file manager, which displays the contents of *.rpm files as a virtual directory and is capable of extracting individual files.