
In the next example, the user first installs a new package with the -i option, and then updates a package with the -U option. Including the -v and -h options is customary. Here, -v is the verbose option that displays all files as they are installed, and -h displays a crosshatch symbol periodically to show RPM is still working. In the following example, the user installs the software package for the Balsa mail client. Notice the full filename is entered. To list the full name, you can use the ls command with the first few characters and an asterisk, `ls balsa*`. The rpm command with the -q option is then used to check that the software was installed. For installed packages only, the software name needs to be used-in this case, balsa-1.2.4-7.

```bash
[root@turtle mypackages]# ls balsa*
balsa-1.2.4-7.i386.rpm

[root@turtle mypackages]# rpm -ivh balsa-1.2.4-7.i386.rpm
balsa-1.2.4-7 ########################################

[root@turtle mypackages]# rpm -q balsa
balsa-1.2.4-7
```

To display information about the installed package, use -qi, and -ql displays a listing of the files a given RPM package contains.

```bash
# rpm -qi balsa
# rpm -ql balsa
```

If you are worried that a software package will install on your system incorrectly, you can use the test option (--test) in the debug mode (vv) to see exactly what actions RPM will take.

```bash
# rpm -ivv --test balsa-1.2.4-7.i386.rpm
```

# Removing RPM Software Packages

To remove a software package from your system, first use rpm -q to make sure it is actually installed. Then use the -e option to uninstall it. You needn't use the full name of the installed file. You only need the name of the application. For example, if you decide you do not need Balsa, you can remove it using the -e option and the software name, as shown here:

```bash
# rpm -e balsa
```

# Verifying an RPM Installation

You can use the verify option (-V) to see if any problems occurred with the installation. RPM compares the current attributes of installed files with information about them placed in the RPM database when the package was installed. If no discrepancies exist, RPM outputs nothing. Otherwise, RPM outputs a sequence of eight characters, one for each attribute, for each file in the package that fails. Those that do not differ have a period. Those that do differ have a corresponding character code, as shown in Table 29-6.

The following example verifies the ProFTPD package:

```bash
[root@turtle mypackages]# rpm -V proftpd
```

### Table 29-6: RPM Discrepancy Codes

| Attribute | Explanation |
|---|---|
| 5 | MD5 checksum |
| S | File size |
| L | Symbolic link |
| T | File modification time |
| D | Device |
| U | User |
| G | Group |
| M | Mode (includes permissions and file types) |

To compare the installed files directly with the files in an RPM package file, you use the `-Vp` option, much like the `-qp` option. To check all packages, use the `-Va` option as shown here:

```bash
# rpm -Va
```

If you want to verify a package, but you only know the name of a file in it, you can combine verify with the `-f` option. The following example verifies the RPM package containing the `ftp` command:

```bash
# rpm -Vf /bin/ftp
```

# Rebuilding the RPM Database

RPM maintains a record of the packages it has installed in its RPM database. You may, at times, have to rebuild this database to ensure RPM has current information on what is installed and what is not. Use the `--rebuilddb` option to rebuild your database file:

```bash
# rpm --rebuilddb
```

To create a new RPM database, use the `--initdb` option. This option can be combined with `--dbpath` to specify a location for the new database.

# Installing Software from RPM Source Code Files: SRPMs

Red Hat and several other distributors also make available source code versions of their binary RPM packaged software. The source code is packaged into RPM packages that will be automatically installed into designated directories where you can easily compile and install the software. Source code packages are called SRPMs. The names for these packages end in the extension .src.rpm. Source code versions for packages in the Red Hat distribution are located on Red Hat releases in the SRPMS directory. Many online sites like rpmfind.net also list SRPM packages. Source code versions have the advantage of letting you make your own modifications to the source code, allowing you to generate your own customized versions of RPM packaged software. You still use the rpm command with the -i option to install source code packages. In the following example, you install the source code for Freeciv:

```bash
# rpm -i freeciv-1.13.0-2.src.rpm
```

# Source Code RPM Directories

On Red Hat, SRPM files are installed in various subdirectories in the /usr/src/redhat directory. When SRPMs are installed, a spec file is placed in the /usr/src/redhat/SPECS directory, and the compressed archive of the source code files is placed in the /usr/src/redhat/SOURCES directory. For Freeciv, a spec file called freeciv.spec is placed in /usr/src/redhat/SPECS, and a compressed archive called freeciv-1.13.0.tar.gz is placed in the /usr/src/redhat/SOURCES directory.

# Building the Source Code

To build the source code files, you need to extract them and run any patches on them that may be included with the package. You do this by changing to the /usr/src/redhat/SPECS directory and using the rpm command, this time with the -bp option, to generate the source code files:

```bash
# cd /usr/src/redhat/SPECS
# rpm -bp freeciv.spec
```

The resulting source code files are placed in their own subdirectory with the package's name in the /usr/src/redhat/BUILD directory. For Freeciv, the Freeciv source code is placed in /usr/src/redhat/BUILD/freeciv-1.13.0 directory. In this subdirectory, you can then modify the source code, as well as compile and install the application. Check the software's README and INSTALL files for details.

# Installing Software from Compressed Archives: .tar.gz

Linux software applications in the form of source code are available at different sites on the Internet. You can download any of this software and install it on your system. Recent releases are often available in the form of compressed archive files. Applications will always be downloadable as compressed archives, if they don't have an RPM version. This is particularly true for the recent versions of GNOME or KDE packages. RPM packages are only intermittently generated.

# Decompressing and Extracting Software in One Step

Though you can decompress and extract software in separate operations, you will find that the more common approach is to perform both actions with a single command. The tar utility provides decompression options you can use to have tar first decompress a file for you, invoking the specified decompression utility. The z option automatically invokes gunzip to unpack a .gz file, and the j option unpacks a .bz2 file. Use the z option for .z files. For example, to combine the decompression and unpacking operation for a tar.gz file into one tar command, insert a z option to the option list, xzvf (see the section "Extracting Software" later in this chapter for a discussion of these options). The next example shows how you can combine decompression and extraction in one step:

```bash
# tar xzvf htdig-3.1.6.tar.gz
```

For a .bz2 compressed archive, you would use the j option instead of the z option.

```bash
# tar xvjf htdig-3.1.6.tar.bz2
```

# Decompressing Software

Many software packages under development or designed for cross-platform implementation may not be in an RPM format. Instead, they may be archived and compressed. The filenames for these files end with the extension .tar.gz, tar.bz2, or .tar.Z. The different extensions indicate different decompression methods using different commands: gunzip for .gz, bunzip2 for .bz2, and decompress for .Z. In fact, most software with an RPM format also has a corresponding .tar.gz format. After you download such a package, you must first decompress it, and then unpack it with the tar command. The compressed archives could hold either source code that you then need to compile or, as is the case with Java packages, binaries that are ready to run.

A compressed archive is an archive file created with tar, and then compressed with a compression tool like gzip. To install such a file, you must first decompress it with a decompression utility like gunzip utility, and then use tar to extract the files and directories making up the software package. Instead of the gunzip utility, you could also use gzip -d. The next example decompresses the htdig-3.1.6.tar.gz file, replacing it with a decompressed version called htdig-3.1.6.tar:

```bash
# ls
htdig-3.1.6.tar.gz
# gunzip htdig-3.1.6.tar.gz
# ls
htdig-3.1.6.tar
```

You can download compressed archives from many different sites, including those mentioned previously. Downloads can be accomplished with FTP clients such as ncftp and Gftp, or with any Web browser, such as Mozilla. Once downloaded, any file that ends with .Z, .bz2, .zip, or .gz is a compressed file that must be decompressed.

For files ending with .bz2, you would use the bunzip2 command. The following example decompresses the Java 2 SDK downloaded from www.blackdown.org:

```bash
# bunzip2 j2sdk-1.3.0-FCS-linux-i386.tar.bz2
```
