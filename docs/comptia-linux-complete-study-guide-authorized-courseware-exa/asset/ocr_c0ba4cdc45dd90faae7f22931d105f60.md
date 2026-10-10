```
```
Size        : 13524400                Licence: GPL
Signature   : DSA/SHA1, Tue 27 May 2008 09:38:42 PM EDT, 
Key ID 9aa8dd0d22458a98
Packager    : Mandriva Linux Security Team <security@mandriva.com>
URL         : http://www.samba.org
Summary     : Samba (SMB) server programs
```
```

# # Extracting Data from RPMs

Occasionally you may want to extract data from RPMs without installing the package. For instance, this can be a good way to retrieve the original source code from a source RPM for compiling the software without the help of the RPM tools or to retrieve fonts or other non-program data for use on a non-RPM system.

RPM files are actually modified cpio archives. Thus, converting the files into cpio files is relatively straightforward, whereupon you can use cpio to retrieve the individual files. To do this job, you need to use the rpm2cpio program, which ships with most Linux distributions. (You can use this tool even on distributions that don't use RPM.) This program takes a single argument—the name of the RPM file—and outputs the cpio archive on standard output. So, if you want to create a cpio archive file, you must redirect the output:

```
```
$ rpm2cpio samba-server-3.0.25b-4.5mdv2008.0.src.rpm
  > samba-server-3.0.25b-4.5mdv2008.0.cpio
```
```

You can then extract the data using cpio, which takes the -i option to extract an archive and --make-directories to create directories:

```
```
$ cpio -i --make-directories < samba-server-3.0.25b-4.5mdv2008.0.cpio
```
```

Alternatively, you can use a pipe to link these two commands together without creating an intermediary file:

```
```
$ rpm2cpio samba-server-3.0.25b-4.5mdv2008.0.src.rpm | cpio -i
  --make-directories
```
```

In either case, the result is an extraction of the files in the archive in the current directory. In the case of binary packages, this is likely to be a series of subdirectories that mimic the layout of the Linux root directory—that is, usr, lib, etc, and so on, although precisely which directories are included depends on the package. For a source package, the result of the extraction process is likely to be a source code tarball, a .spec file (which holds information RPM uses to build the package), and perhaps some patch files.