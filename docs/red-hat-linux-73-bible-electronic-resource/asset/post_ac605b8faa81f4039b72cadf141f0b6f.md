
## Verifying packages with rpm

If something in a software package isn’t working properly, or if you suspect that your system has been tampered with, the verify (`-V`) option of rpm can help you verify the contents of your software packages. Information about each installed package is stored on your computer in the RPM database. By using the verify option, you can check if any changes were made to the components in the package.

Various file size and permissions tests are done during a verify operation. If everything is fine, there is no output. Any components that have been changed from when they were installed, however, will be printed along with information indicating how they were changed. Here’s an example:

```bash
# rpm -V ppp
S.5....T c /etc/ppp/chap-secrets
S.5....T c /etc/ppp/options
S.5....T c /etc/ppp/pap-secrets
```

This output shows that the ppp package (used to dial-up a TCP/IP network such as the Internet) has had three files changed since it was installed. The notation at the beginning shows that the file size (S), the MD5 sum (5), and the modification time (T) have all changed. The letter c shows that these are all configuration files. By reviewing these files and seeing that the changes were only those that I made to get PPP working, I can verify that the package is okay.

The indicators that you may see when you verify the contents of a configuration file are:

- 5 — MD5 Sum — An MD5 checksum indicates a change to the file contents.
- S — File size — The number of characters in the file has changed.
- L — Symlink — The file has become a symbolic link to another file.
- T — Mtime — The modification time of the file has changed.
- D — Device — The file has become a device special file.
- U — User — The user name that owns the file has changed.
- G — Group — The group assigned to the file has changed.
- M — Mode — If the ownership or permission of the file changed.

> **TIP:** There is a utility available for browsing the contents of RPM files in a Windows system. By using the *rpmbrowser.exe* utility, you can list and extract files from an RPM distribution. This utility is available from winsite.com (search for rpmbrowser from www.winsite.com/ws_search.html).

# Building and installing from source code

If no binary version of the package that you want is available, or if you just want to tailor a package to your needs, you can always install the package from source code. The source code CD that comes with Red Hat Linux contains the source code equivalent (SRPMS) of the binary packages you installed. You can modify the source code and rebuild it to suit your needs.

> **NOTE:** Though the Red Hat Linux source-code CD is not included with this book, you can obtain a copy from the publisher. Refer to the Linux source-code mail-in coupon at the back of this book.

Software packages that are not available in SRPMS format are typically available in `tar/gzip` format. Although the exact instructions for installing an application from a source code archive vary, many packages that are in the `.gz` and `.tar` formats follow the same basic procedure.

> **TIP:** Before you install from source code, you will need to install a variety of software development packages. If you have the disk space, I recommend that you install all software development packages that are recommended during Red Hat installation. (It's annoying to have an install fail because of a missing component. You can end up wasting a lot of time figuring out what is missing.)

The following is a minimal list of C-programming software development tools:

- `gcc` — Contains the `gcc` (GNU C compiler) compiler.
- `make` — Contains the `make` command for making the binaries from Makefiles.
- `glibc` — Contains important shared libraries, the C library, and the standard math library.
- `glibc-devel` — Contains standard header files needed to create executables.
- `binutils` — Contains utilities needed to compile programs (such as the assembler and linker).
- `kernel-source` — Contains the Linux kernel source code and is needed to rebuild the kernel.
- `libc` — Contains libraries needed for programs that were based on `libc 5`, so older applications can run on `glibc` (`libc 6`) systems.

## Installing software in SRPMS format

To install a source package from the Red Hat Linux source CD, use the following procedure:

1. Insert the Red Hat Linux source CD into the CD-ROM drive. It should mount automatically. (If it doesn't, type `mount /mnt/cdrom` in a Terminal window.)
2. Change to the source directory on the CD. For example:

   ```bash
   # cd /mnt/cdrom/SRPMS
   ```

3. Choose the package you want to install (type 1s to see the packages) and install it using the following command:

   ```bash
   # rpm -iv package name*.src.rpm
   ```

   (Replace *packagename* with the name of the package you are installing.) The source is installed in the Red Hat Linux source tree (/usr/src/redhat). Spec files are copied to /usr/src/redhat/SPECS.

4. Change to the SPECS directory as follows:

   ```bash
   # cd /usr/src/redhat/SPECS
   ```

5. Unpack the source code as follows:

   ```bash
   # rpm -bp package name*.spec
   ```

6. The package's source code is installed to the /usr/src/redhat/BUILD/package directory.

7. You can now make changes to the files in the package's BUILD directory. Read the README, Makefile, and other documentation files for details on how to build the individual package.

## Installing software in gzip/tar format

Here are some generic instructions that you can use to install many Linux software packages that are in gzip/tar format:

1. Get the source code package from the Internet or from a CD distribution and copy it into an empty directory (preferably using a name that identifies the package).

2. Assuming the file is compressed using gzip, uncompress the file using the following command:

   ```bash
   # gzip -d package.tar.gz
   ```

   The result is that the package is uncompressed and the .gz is removed from the package name (for example, package.tar).

3. From the resulting tar archive, run the tar command as follows:

   ```bash
   # tar xvf package.tar
   ```

   This command extracts the files from the archive and copies them to a subdirectory of the current directory.

4. Change directories to the new subdirectory created in Step 3, as follows:

   ```bash
   # cd newdir
   ```

5. Look for a file called INSTALL or README. One of these files should give you instructions on how to proceed with the installation. In general, the make command is used to install the package. Here are a few things to look for in the current directory:

   If there is a Makefile, try running:

   ```bash
   # ./configure -prefix=/usr
   # make all
   ```

   If there is an Imake file, try running:

   ```bash
   # xmkmf -a
   # make all
   ```

   If there is a Makefile, try running:

   ```bash
   # make all
   ```

   After the program is built and installed, you may need to do additional configuration. You should consult the man pages and/or the HOWTOs that come with the software for information on how to proceed.

> **TIP:** Even if you are not a programmer, reading the source code used to make a program can often give you insight into how that program works. Sometimes notes about how a program works may be put in the source code, but never make it into the documentation.

To try out this procedure, I downloaded whichman package, which includes utilities that let you find manual pages by entering keywords. The file I downloaded, whichman-1.5.tar.gz, was placed in a directory that I created called /usr/sw/which. I then ran the gzip and tar commands, using whichman-1.5.tar.gz and whichman-1.5.tar as options, respectively.

I changed to the new directory, cd /usr/sw/which/whichman-1.5. I then listed its contents. The README file contained information about the contents of the package and how to install it. As the README file suggested, I typed make, and then make install. The commands whichman, fwhich, and ffff were installed in /usr/bin. (At this point, you can check the man page for each component to see what it does.)

The last thing I found in the README file was that a bit of configuration needed to be done. I added a MANPATH variable to my $HOME/.bashrc to identify the location of man pages on my computer to be searched by the whichman utility. The line I added looked like this:

```bash
export MANPATH=/usr/man:/usr/X11R6/man:/usr/doc/samba-2.0.2/docs
```

In case you are wondering, whichman, fwhich, and ffff are commands that you can use to search for man pages. They can be used to find several locations of a man page, man pages that are close to the name you enter, or man pages that are located beneath a point in the directory structure, respectively.
