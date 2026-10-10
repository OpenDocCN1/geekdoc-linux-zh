
## Part II: Using CentOS

- `--nodeps` — Uninstall the package without checking for dependencies.
- `--noscripts` — Uninstall the package without running any preuninstall or postuninstall scripts.
- `--notriggers` — Uninstall the package without executing scripts that are triggered by removing the package.

If you feel nervous about boldly removing a package, you can always run the uninstall in test mode (`-test`) before you do the real uninstall. Test mode shows you everything that would happen in the uninstall without actually uninstalling. (Add the `--v` option to see the details.) Here’s an example:

```
# rpm -e -v -test jpliot | less
D:  0 0x00000fd00  4096  218926  2160537 /
D:  1 0x000000003  4096       0     -1 /proc
D:  2 0x000000000  4096       0     -1 /sys
D:  3 0x00000000b  4096       0     -1 /dev/pts
D:  4 0x000000801  1024  77585  26043 /boot
D:  5 0x000000013  4096  64436  64435 /dev/shm
D:  6 0x000000014  4096       0  -1 /proc/sys/fs/binfmt_misc
D:  7 0x000000015  4096       0  -1 /var/lib/nfs/rpc_pipefs
D: sanity checking 1 elements
D: running pre-transaction scripts
D: computing 84 file fingerprints
D: computing file dispositions
D: opening db index /var/lib/rpm/Basenames  rdonly mode=0x0
D: === jpliot-0.99.8.7.1  i386-linux 0x1
D:  erase: jpliot-0.99.8.7.1 has 64 files, test = 1
D: running post-transaction scripts
D: closed  db index /var/lib/rpm/Pubkeys
D: closed  db index /var/lib/rpm/Requirename
D: closed  db index /var/lib/rpm/Basenames
D: closed  db index /var/lib/rpm/Name
D: closed  db index /var/lib/rpm/Packages
D: closed  db index /var/lib/rpm/Arch
D: closed  db environmnt /var/lib/rpm/Packages
D: May free Score board(!!!)
```

If the results look fine, you can run the command again, without the `-test` option, to have the package removed.

### Querying Packages with rpm

You can use the `-q` options (at least one additional option is required after `q`) to `rpm` to get information about `RPM` packages. This can be simply listing the packages that are installed or printing detailed information about a package. Here is the basic format of an `rpm` query command:

```
# rpm -q [options]
```

The following list shows some useful options you can use with an *rpm* query:

- *-qa* — Lists all installed *packages*.
- *-qf* *file* — Lists the *package* that owns *file*. (The *file* must include the full path name or *rpm* assumes the current directory.)
- *-qi* *package* — Lists lots of information about a *package*.
- *-qR* *package* — Lists *components* (such as libraries and commands) that *package* depends on.
- *-ql* *package* — Lists all the *files* contained in *package*.
- *-qd* *package* — Lists all documentation files that come in *package*.
- *-qc* *package* — Lists all *configuration* files that come in *package*.
- *-qp* [*Option*] *package* — Query *packages* that are not yet installed. Using this option, along with other query options, allows you to query *packages* you have that are not yet installed.

To list all the *packages* installed on your computer, use the *-a* query option. Because this is a long list, you should either pipe the output to *less* or, possibly, use *grep* to find the *package* you want. The following command line displays a list of all installed *RPM* *packages* and then shows only those names that include the string of characters *xorg*. (The *-i* option to *grep* says to ignore case.)

```
# rpm -qa | grep -i xorg
```

If you are interested in *details* about a particular *package*, you can use the *rpm* *-i* query option. In the following example, *information* about the *dosfstools* *package* (for working with *DOS* *file* *systems* in *Linux*) is displayed:

```
# rpm -qi dosfstools
Name          : dosfstools            Relocations: (not relocatable)
Version       : 2.11                  Vendor: CentOS
Release       : 7.el5                 Build Date: Wed 21 Jan 2009
            12:03:18 AM EST          Build Host: builder16.centos.org
Install Date  : Sun 22 Nov 2009 10:36:39 AM EST
Group         : Applications/System   Source RPM: dosfstools-2.11 7.el5.src.rpm
Size          : 120853                License: GPL
Signature     : DSA/SHA1, Sun 08 Mar 2009 09:45:25 PM EDT,
    Key ID a8a447dc8562897
Summary     : Utilities for making and checking MS-DOS FAT file systems on Linux.
Description :
The dosfstools package includes the mkdosfs and dosfsck utilities, which respectively make and check MS-DOS FAT filesystems on hard drives or on floppies.
```

To find out about a package's contents, you can use the `-l` option with your query. The following example shows the complete path names of files contained in the `dosfstools` package:

```
# rpm -ql dosfstools | less
/sbin/dosfsck
/sbin/fcck.msdos
/sbin/fcck.vfat
/sbin/mkdosfs
/sbin/mkfs.msdos
/sbin/mkfs.vfat
/usr/share/man/man8/dosfsck.8.gz
.
.
.
```

*Note: The original text says "use the -i option" in the paragraph before the code block but shows file listing which corresponds to -l. However, the instruction says "If you are interested in details... use -i". The next paragraph says "To find out about a package's contents, you can use the -i option". This is likely an OCR error for -l. I will correct it to -l based on context and standard RPM usage, as -i shows info, -l shows list. Wait, looking closely at the source: "To find out about a package's contents, you can use the `-i` option with your query." This is definitely a typo in the source book or OCR. Standard usage is -l for listing. I will correct it to `-l` to match the command `rpm -ql` in the code block? Actually, the code block in the source is `# rpm -qi dosfstools | less` but the output is a file list. `rpm -qi` outputs info, `rpm -ql` outputs files. The text says "shows the complete path names of files". The command in the code block is `rpm -qi`. This is a contradiction. I will preserve the text's intent but correct the obvious error in the command to `-ql` to match the output, or keep the text as is? The instruction says "correct obvious OCR errors". A command `rpm -qi` producing a file list is a logical error/OCR error. I will correct the command in the code block to `rpm -ql` and the text to `-l` if it makes sense. Let's look at the next section. "Would you like to know how to use the components... -d option... documentation". "Many packages have configuration files... -c option". "which package a particular command... came from... -qf option".

Let's re-read the specific block:
"To find out about a package's contents, you can use the `-i` option with your query. The following example shows the complete path names of files contained in the `dosfstools` package:
`# rpm -qi dosfstools | less`
`/sbin/dosfsck`..."

This is clearly a typo in the book/OCR. `-i` is for info. `-l` is for list. I will correct `-i` to `-l` in both text and code to ensure accuracy, as "contents" and "path names of files" imply listing.

Wait, looking at the previous page 218, there was a `-i` example showing Name, Version, etc.
So this section on 219 is definitely about listing files. I will correct it to `-l`.

```
# rpm -ql dosfstools | less
/sbin/dosfsck
/sbin/fcck.msdos
/sbin/fcck.vfat
/sbin/mkdosfs
/sbin/mkfs.msdos
/sbin/mkfs.vfat
/usr/share/man/man8/dosfsck.8.gz
.
.
.
```

Would you like to know how to use the components in a package? Using the `-d` option with a query will display the documentation (man pages, README files, HOWTOs, etc.) that is included with the package. If you are having trouble getting your X Window System running properly, you can use the following command line to find documents that may help:

```
# rpm -qd xorg-x11-server-Xorg | less
/usr/share/man/man1/Xorg.lx.gz
/usr/share/man/man1/Xserver.1x.gz
/usr/share/man/man1/cvt.1.gz
/usr/share/man/man1/gtf.lx.gz
/usr/share/man/man1/scancalc1.1x.gz
/usr/share/man/man4/fbdevhw.4.gz
/usr/share/man/man5/xorg.conf.5.gz
```

Many packages have configuration files associated with them. To see what configuration files are associated with a particular package, use the `-c` option with a query. For example, this is what you would type to find configuration files that are used with the `ppp` package:

```
# rpm -qc ppp
/etc/logrotate.d/ppp
/etc/pam.d/ppp
/etc/ppp/chap-secrets
/etc/ppp/options
/etc/ppp/pap-secrets
```

If you ever want to know which package a particular command or configuration file came from, you can use the `-qf` option. In the following example, the `-qf` option displays the fact that the `chgrp` command comes from the `fileutils` package:

```
# rpm -qf /bin/chgrp
coreutils-5.97-19.el5
```

*Note: The text says "fileutils" but the output says "coreutils". In older systems, chgrp was in fileutils, later moved to coreutils. I will keep the text as is but note the output.*

Before you install a package, you can do the same queries on it that you would do on an installed package. This can be a great tool for finding information from a package while it is in your current directory, or even in a software repository. Here is an example of using the `-qp` option with `-i` to see the description of a package in a software repository:

```
# rpm -qpi http://centos.karan.org/el5/extras/testing/i386/RPMS/caca-utils-0.99.0.1.beta11.el5.kb.i386.rpm
Name        : caca-utils           Relocations: (not relocatable)
Version     : 0.99                Vendor: http://www.karan.org/
Release     : 0.1.beta11.el5.kb   Build Date: Mon 28 May 2007
03:46:13 PM EDT
Install Date: (not installed)     Build Host: monk.karan.org
Group      : Amusements/Graphics Source RPM: libcaca-0.99-0.1_
_beta11.el5.kb.src.rpm
Size        : 118940             License: LGPL
Signature   : DSA/SHA1, Tue 29 May 2007 05:06:22 AM EDT,
Key ID 300Ddd9e3e313cf5b
Packager    : Karanbir Singh <kbsingh@karan.org>
URL         : http://libcaca.zoy.org/
Summary     : Colour Ascii Art Text mode graphics utilities based on
libcaca
Description :
This package contains utilities and demonstration programs for lib-
caca, the
Colour Ascii Art library.

cacaview is a simple image viewer for the terminal. It opens most
image
formats such as JPEG, PNG, GIF etc. and renders them on the
terminal using
ASCII art. The user can zoom and scroll the image, set the
filtering method
or enable anti-aliasing.

cacaball is a tiny graphic program that renders animated ASCII
metaballs on
the screen. cacafire is a port of AALib's aafire and displays
burning ASCII
art flames, and cacademo is a simple application that shows the
libcaca
rendering features such as line and ellipses drawing, triangle
filling and
sprite blitting.
```

In the previous example, the long command line that spans two lines should actually be typed on one line. If you are concerned about the content or legality of downloading a package, this example is a way to read the description of a package before you even download it.

In the following example, the command lists the files contained in a package that is in the current directory:

```
# rpm -qpl AdobeReader_en-US_8.3.1-1.1486.rpm
```

Again, this is an excellent way to find out what is in a package before you install it.
