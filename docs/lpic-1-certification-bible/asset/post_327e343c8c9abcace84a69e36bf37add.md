
Unpacking file (from .../archives/file_3.28-1_i386.deb) ...
Selecting previously deselected package debhelper.
Unpacking debhelper (from .../debhelper_2.0.86_all.deb) ...
Selecting previously deselected package librpm1.
Unpacking librpm1 (from .../librpm1_3.0.3-1_i386.deb) ...
Selecting previously deselected package rpm.
Unpacking rpm (from .../archives/rpm_3.0.3-1_i386.deb) ...
Selecting previously deselected package alien.
Unpacking alien (from .../archives/alien_6.54_all.deb) ...
Setting up patch (2.5.2-2) ...
Setting up dpkg-dev (1.6.15) ...
Setting up file (3.28-1) ...
Setting up debhelper (2.0.86) ...
Setting up librpm1 (3.0.3-1) ...
Setting up rpm (3.0.3-1) ...
Setting up alien (6.54) ...

3. The next step is to convert the RPM package to a .deb package with the following command:

```
debian:~$ alien wget-1.5.3-6.i386.rpm
-- Examining wget-1.5.3-6.i386.rpm
-- Unpacking wget-1.5.3-6.i386.rpm
659 blocks
----
-- Automatic package debianization
-- Building the package wget_1.5.3-7-i386.deb
dh_testdir
# Nothing to do.
dh_testdir
dh_testroot
dh_clean -k
dh_installdirs
cp -a `ls | grep -v debian` debian/tmp
dh_installdocs
dh_installexamples
dh_installmenu
dh_installcron
dh_instalchangeloglogs
dh_compress
dh_suidregister
dh_installdeb
dh_shlibdeps
dh_gencontrol
dh_makeshlibs
```

```
dh_md5sums
dh_builddeb
dpkg-deb: building package 'wget' in '/../wget_1.5.3-7_i386.deb'.
Generation of wget_1.5.3-7_i386.deb complete.
-- Successfully finished
```

4. The final step is to install the new package just like any other.

```
debian:~# dpkg -i wget_1.5.3-7_i386.deb
Selecting previously deselected package wget.
(Reading database ... 17317 files and directories currently installed.)
Unpacking wget (from wget_1.5.3-7_i386.deb) ...
Setting up wget (1.5.3-7) ...
```

## Answers to Chapter Questions

## Chapter Pre-Test

- 1. Use the `./configure` script to generate a Makefile.
- 2. Use the `ldconfig` command to update the `ld.so.cache` file.
- 3. The tool for converting package formats is called `alien`.
- 4. `apt-get` can access files from a CD-ROM, a local directory, or from the Internet using HTTP or FTP.
- 5. To upgrade a package with RPM, use `rpm -U` or `rpm --upgrade`.
- 6. The RPM package database is stored in `/var/lib/rpm`.
- 7. Use the `apt-get clean` command to clear the `apt-get` package cache.
- 8. To add sources to `apt-get`, edit the `/etc/apt/sources.list` file.
- 9. You can authenticate RPM packages using the GPG, GPG, or MD5 tool.
- 10. You can query a package's status with `dpkg`.

## Assessment Questions

- 1. C. The `./configure` script runs through many tests and creates a Makefile for that specific system. The other options are invalid. See the "Running the configure script" section for more information.
- 2. D. The `make install` command installs software that has already been compiled. The `make` command is used to compile the software. See the "Installing the software" section for more information.
- 3. A. Red Hat created the RPM packaging system. Debian uses .deb packages. See the “Red Hat Package Manager” section for more information.
- 4. B. In some circumstances the RPM database can be corrupted, and the `rpm -rebuilddb` command will try to rebuild the database. The other options are invalid. See the “Red Hat Package Manager” section for more information.
- 5. A, C, and D. All three are supported by RPM. See the “Validating package integrity” section for more information.
- 6. `rpm -i processor-4.2-i386.rpm` or `rpm -e install processor-4.2-i386.rpm`. See the “Installing packages” section for more information.
- 7. D. `ldconfig` creates the `ld.so.cache` file from `ld.so.conf`. See the “Managing Shared Libraries” section for more information.
- 8. A. Dynamic linking does not compile the libraries into the executable like static linking, therefore making the executable smaller. The other options are invalid. See the “Managing Shared Libraries” section for more information.
- 9. A and C. Both `rpm --uninstall` and `rpm -e` remove RPM packages. The other options are invalid. See the “Removing packages” section for more information.
- 10. B. The `spec` file has the compilation options. A `Makefile` is used to compile source code not in RPM format. See the “Creating binary packages from source packages” section for more information.
- 11. A. The `alien` tool converts package files. The `dpkg` tool is used to manipulate packages in Debian. See the “Using alien” section for more information.
- 12. B. The `dpkg --install` command installs Debian `.deb` packages. The `rpm` tool is used with RPM packages. There is no -I option for `apt-get`. See the “Installing packages” section for more information.
- 13. D. `dpkg -P` purges the package, which removes all files including the configuration files. See the “Removing packages” section for more information.
- 14. A. The `dselect` tool has all the functionality of `dpkg`, but uses a character-based graphic interface instead of a command-line interface. `apt-get` is used to retrieve and install packages. `gnopern` is a graphical front end to the `rpm` tool. See the “Using dselect” section for more information.
- 15. A. The sources for `apt-get` are stored in the `sources.list` file. The other options are invalid. See the “Using apt-get” section for more information.
- 16. D. The `upgrade` command checks all the sources in the `sources.list` file and updates the package database accordingly. The `upgrade` command tells `apt-get` to download and install all packages that are newer than those installed on the system. The other options are invalid. See the “Updating the available packages” section for more information.
- 17. A, B, C, and D. The apt-get tool can get packages from local NFS and CD-ROM drives and from the Internet via FTP and HTTP. See the “Using apt-get” section for more information.
- 18. C. The autoclean parameter removes only old packages that can no longer be retrieved. The other options are invalid. See the “Clearing the package archives” section for more information.
- 19. A, B, and D. alien supports Red Hat, Debian, and Slackware package formats, but not BSD. See the “Using alien” section for more information.
- 20. C. The -d option tells alien to create a Debian package. The -r option specifies RPM, and the -t option specifies .tgz. See the “Using alien” section for more information.

### Scenario Answers

- 1. You could either compile the source code yourself or convert the RPM package to .deb format using alien. While either option should create a working application, only by converting the package can you manage the application with the package tools.
- 2. Since no packages are shown as having been installed, it would appear that the RPM database is incorrect or corrupt. The best option at this point is to run a rebuild with the rpm -rebuilddb command.

## Getting Around in Linux

Now that you have a working Linux distribution installed, you can move into the use of the system. This includes how to move around efficiently using commands and utilities. Chapter 4 introduces the tools and utilities used for working with text files. Also covered in this chapter are the tools used for data redirection. Chapter 5 goes in depth into tools and utilities used to create and manage file systems and partitions on Linux systems. Chapter 6 covers file management including the various commands to move, create, and remove files, quotas, and permissions. Chapter 7 covers the Linux documentation available to users on Linux systems. This includes man page documentation located on the Linux system as well as documentation available on the Internet. Chapter 8 provides detailed information on the Linux boot process including troubleshooting and recovery tips. Chapter 9 provides information on X, an application used on Linux systems to provide a graphical environment using window managers.

## In This Part

- **Chapter 4**
    Processing Text
- **Chapter 5**
    Using Partitions and File Systems
- **Chapter 6**
    Managing Files
- **Chapter 7**
    Using Documentation
- **Chapter 8**
    Understanding the Boot Process
- **Chapter 9**
    Using X
