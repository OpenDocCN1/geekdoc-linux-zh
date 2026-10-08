
## Removing RPM Software Packages

To remove a software package from your system, first use **rpm -q** to make sure it is actually installed. Then use the **-e** option to uninstall it. You didn’t use the full name of the installed file. You only need the name of the application. For example, if you decide you do not need Gnumeric, you can remove it using the **-e** option and the software name, as shown here:

```
# rpm -e gnumeric
```

## RPM: Verifying an RPM Installation

You can use the verify option (**-V**) to see if any problems occurred with the installation. RPM compares the current attributes of installed files with information about them placed in the RPM database when the package was installed. If no discrepancies exist, RPM outputs nothing. Otherwise, RPM outputs a sequence of eight characters, one for each attribute, for each file in the package that fails. Those that do differ have a period. Those that do differ have a corresponding character code, as shown in Table 29-6.

The following example verifies the ProFTPD package:

```
[root@turtle mypackages]# rpm -V proftpd
```

To compare the installed files directly with the files in an RPM package file, you use the **-Vp** option, much like the **-gp** option. To check all packages, use the **-Va** option as shown here:

```
# rpm -Va
```

If you want to verify a package, but you only know the name of a file in it, you can combine verify with the **-f** option. The following example verifies the RPM package containing the **ftp** command:

```
# rpm -Vf /bin/ftp
```

| Attribute | Explanation |
| :--- | :--- |
| S | MD5 checksum |
| S | File size |
| L | Symbolic link |
| T | File modification time |
| D | Device |
| U | User |
| G | Group |
| M | Mode (includes permissions and file types) |

**TABLE 29-6** RPM Discrepancy Codes

## Rebuilding the RPM Database

RPM maintains a record of the packages it has installed in its `rpm` database. You may, at times, have to rebuild this database to ensure RPM has current information on what is installed and what is not. Use the `--rebuilddb` option to rebuild your database file:

```
# rpm --rebuilddb
```

To create a new RPM database, use the `--initdb` option. This option can be combined with `--dbpath` to specify a location for the new database.

## Installing Software from RPM Source Code Files: SRPMs

Fedora and several other distributors also make available source code versions of their binary RPM-packaged software. The source code is packaged into RPM packages that will be automatically installed into designated directories where you can easily compile and install the software. Source code packages are called SRPMs. The names for these packages end in the extension `.src.rpm`. Source code versions for packages in the Fedora distribution are located in the **SRPMS** directory. Many online sites like `rpmfind.net` also list SRPM packages. Source code versions have the advantage of letting you make your own modifications to the source code, allowing you to generate your own customized versions of RPM-packaged software. You still use the `rpm` command with the `-i` option to install source code packages. In the following example, you install the source code for FreeCiv:

```
# rpm -i freeciv-1.14.2-1.src.rpm
```

## Source Code RPM Directories

On Fedora, SRPM files are installed in various subdirectories in the `/usr/src/redhat` directory. When SRPMs are installed, a spec file is placed in the `/usr/src/redhat/SPECS` directory, and the compressed archive of the source code files is placed in the `/usr/src/redhat/SOURCES` directory. For FreeCiv, a spec file called `freeciv.spec` is placed in `/usr/src/redhat/SPECS`, and a compressed archive called `freeciv-1.14.2-1.tar.gz` is placed in the `/usr/src/redhat/SOURCES` directory.

## Building the Source Code

To build the source code files, you need to extract them and run any patches on them that may be included with the package. You do this by changing to the `/usr/src/redhat/SPECS` directory and using the `rpm` command, this time with the `-bp` option, to generate the source code files:

```
# cd /usr/src/redhat/SPECS
# rpm -bp freeciv.spec
```

The resulting source code files are placed in their own subdirectory with the package’s name in the `/usr/src/redhat/BUILD` directory. For FreeCiv, the FreeCiv source code is placed in `/usr/src/redhat/BUILD/freeciv-1.14.2-1` directory. In this subdirectory, you can then modify the source code, as well as compile and install the application. Check the software’s README and INSTALL files for details.

## Installing Software from Compressed Archives: .tar.gz

Linux software applications in the form of source code are available at different sites on the Internet. You can download any of this software and install it on your system. Recent releases are often available in the form of compressed archive files. Applications will always be downloadable as compressed archives, if they don’t have an RPM version. This is particularly true for the recent versions of GNOME or KDE packages. RPM packages are only intermittently generated.

### Decompressing and Extracting Software in One Step

Though you can decompress and extract software in separate operations, you will find that the more common approach is to perform both actions with a single command. The `tar` utility provides decompression options you can use to have `tar` first decompress a file for you, invoking the specified decompression utility. The `z` option automatically invokes `gunzip` to unpack a .gz file, and the `j` option unpacks a .bz2 file. Use the `Z` option for .Z files. For example, to combine the decompressing and unpacking operation for a `tar.gz` file into one `tar` command, insert a `z` option to the option list, `xzvf` (see the later section “Extracting Software” for a discussion of these options). The next example shows how you can combine decompression and extraction in one step:

```
# tar xzvf htdig-3.1.6.tar.gz
```

For a .bz2-compressed archive, you would use the `j` option instead of the `z` option.

```
# tar xvJf htdig-3.1.6.tar.bz2
```

### Decompressing Software

Many software packages under development or designed for cross-platform implementation may not be in an RPM format. Instead, they may be archived and compressed. The filenames for these files end with the extension .tar.gz, .tar.bz2, or .tar.Z. The different extensions indicate different decompression methods using different commands: `gunzip` for .gz, `bunzip2` for .bz2, and `decompress` for .Z. In fact, most software with an RPM format also has a corresponding .tar.gz format. After you download such a package, you must first decompress it and then unpack it with the `tar` command. The compressed archives could hold either source code that you then need to compile or, as is the case with Java packages, binaries that are ready to run.

*A compressed archive* is an archive file created with `tar` and then compressed with a compression tool like `gzip`. To install such a file, you must first decompress it with a decompression utility like `gunzip` and then use `tar` to extract the files and directories making up the software package. Instead of the `gunzip` utility, you could also use `gzip -d`. The next example decompresses the `htdig-3.2.6.tar.gz` file, replacing it with a decompressed version called `htdig-3.2.6.tar`:

```
# ls
htdig-3.2.6.tar.gz
# gunzip htdig-3.2.6.tar.gz
# ls
htdig-3.2.6.tar
```

You can download compressed archives from many different sites, including those mentioned previously. Downloads can be accomplished with FTP clients such as NeFTP and gFTP, or with any Web browser. Once downloaded, any file that ends with .Z, .bz2, .zip, or .gz is a compressed file that must be decompressed.

For files ending with .bz2, you would use the bunzip2 command. The following example decompresses a bz2 version:

```
# ls
htdig-3.2.6.tar.bz2
# bunzip2 htdig-3.2.6.tar.bz2
# ls
htdig-3.2.6.tar
```

Files ending with .bin are self-extracting archives. Run the bin file as if it were a command. You may have to use chmod to make it executable. The j2sdk software package is currently distributed as a self-extracting bin file.

```
# j2sdk-1.4.2-PCS-linux-i386.tar.bin
# ls
j2sdk-1.3.0-PCS-linux-i386.tar
```

### Selecting an Install Directory

Before you unpack the archive, move it to the directory where you want it. Source code packages are often placed in a directory like /usr/local/src, and binary packages go in designated directories. When source code files are unpacked, they generate their own subdirectories from which you can compile and install the software. Once the package is installed, you can delete this directory, keeping the original source code package file (tar.gz).

Packages that hold binary programs ready to run, like Java, are meant to be extracted in certain directories. Usually this is the /usr/local directory. Most archives, when they unpack, create a subdirectory named with the application name and its release, placing all those files or directories making up the software package into that subdirectory. For example, the file htdig-3.2.6.tar unpacks to a subdirectory called htdig-3.2.6. In certain cases, the software package that contains precompiled binaries is designed to unpack directly into the system subdirectory where it will be used. For example, as it is recommended that j2sdk-1.4.2-PCS-linux-i386.tar be unpacked in the /usr/local directory, where it will create a subdirectory called j2sdk-1.4.2. The /usr/local/j2sdk-1.4.2/bin directory holds the Java binary programs.

### Extracting Software

First, use tar with the t option to check the contents of the archive. If the first entry is a directory, then when you extract the archive, that directory is created and the extracted files are placed in it. If the first entry is not a directory, you should first create one and then copy the archive file to it. Then extract the archive within that directory. If no directory exists as the first entry, files are extracted to the current directory. You must create a directory yourself to hold these files.

```
# tar tvf htdig-3.1.6.tar
```
