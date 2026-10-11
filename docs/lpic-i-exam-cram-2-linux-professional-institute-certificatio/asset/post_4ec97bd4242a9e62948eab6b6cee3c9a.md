
if the package is to be upgraded with the -u option, a complex set of algorithms goes into play to ensure the configuration is properly applied.

## Querying Packages

Querying for package data is only one of the steps that takes place when you manage packages, although it has arguably the most options of all the tasks RPM performs.

It's very important that you understand the difference between packages installed on the system (that appear in the RPM Database) and packages that exist simply as files on the disk or other resource. The chief difference in the rpm command's usage is the addition of the -p option to specify that the package being acted on is a file on disk.

The most basic of all queries is to return output that a particular package is or is not on the system:

```
rpm -q krbafs
```

This returns the output shown here:

```
krbafs-1.1.1-1
```

Simply by adding a few modifier characters to this query, you can gather much more information about any package. The first modifier I usually recommend is to get information on the package:

```
rpm -qi krbafs
```

This returns the following output:

```
Name     : krbafs                  Relocations: (not relocatable)
Version    : 1.1.1                   Vendor: Red Hat, Inc.
Release    : 1
--Build Date: Tue 05 Mar 2002 05:00:20 PM EST
Install date: Wed 13 Aug 2003 10:30:50 AM EDT
--Build Host: porky.devel.redhat.com
Group    : System Environment/Libraries
--Source RPM: krbafs-1.1.1-1.src.rpm
Size     : 46832
--License: Freely Distributable
Packager   : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
Summary    : A Kerberos to AFS bridging library, built against Kerberos 5.
Description : This package contains the krbafs shared library, which allows programs to obtain AFS network filesystem tokens using Kerberos IV credentials, without having to link with official AFS libraries which may not be available for a given platform.
```

To get information about a package's files, use both the `-q` (query) option and the `-l` (file listing) option:

```
rpm -ql krbafs
```

This returns

```
/etc/krb.conf
/etc/krb.realms
/usr/kerberos/lib/libkrbafs.so.0.0.0
/usr/share/doc/krbafs-1.1.1
/usr/share/doc/krbafs-1.1.1/COPYRIGHT
/usr/share/doc/krbafs-1.1.1/ChangeLog
```

![](img/49f4f38f3aec011238fa50f89e643db3_284_0.png)

When you get questions about listing package files or information, remember the difference between listing the contents of a package in the database and doing the same for a package on disk:
- `rpm -qil` package_name—Used for installed packages
- `rpm -qilp` package_name—Used for uninstalled packages

In addition, remember that you can specify these options in any order, as long as they are all there. In effect, **rpm -qilp**, **rpm -qlip**, and **rpm -pliq** all work.

To see a revision history or changelog for the package, use this command:

```
rpm -q --changelog krbafs
```

This returns the following output (truncated for readability):

+ * Fri Mar 01 2002 Nalin Dahyabhai <nalin@redhat.com> 1.1.1-1
+   - update to 1.1.1
+   - build shared only, and use a map file to only export symbols from the shared library which are declared in the header

+ * Fri Feb 22 2002 Nalin Dahyabhai <nalin@redhat.com> 1.1-4
+   - rebuild

This output is similar to the CHANGELOG, REVISIONS, or RELEASES files found in most software package source code repositories describing the history of the package's changes.

![](img/49f4f38f3aec011238fa50f89e643db3_284_1.png)

This is the sort of thing that LPI loves to put on the exam. If you've never used rpm to this level, the questions will get the best of you. Don't forget that you must use the **-q** and **--changelog** options together; otherwise, you'll get a syntax error.

To find all the configuration files for a package, you use the query and config options like so:

```
rpm -qc sendmail
```

This returns

```
/etc/aliases
/etc/mail/Makefile
/etc/mail/access
/etc/mail/domainstable
/etc/mail/helpfile
/etc/mail/local-host-names
/etc/mail/mailetable
/etc/mail/sendmail.mc
/etc/mail/statistics
/etc/mail/trusted-users
/etc/mail/virtusertable
/etc/rc.d/init.d/sendmail
/etc/sendmail.cf
/etc/sysconfig/sendmail
/usr/lib/sasl/Sendmail.conf
```

> Remember, this shows only the configuration files, not the rest of the package contents—the contents are displayed by the -ql option.

To see which other capabilities or packages a given package requires, you use the --requires or -R option (remember it's a package on disk, so use -p), like so:

```
rpm -qRp tree-1.2-7.i386.rpm
```

This returns the output shown here:

```
1d-linux.so.2
libbc.so.6
libbc.so.6(GLIBC_2.0)
```

> If the system doesn't provide these capabilities, you'll probably be in for a down-load-ing and dependency-resolving session. Check out http://www.rpmfind.net and http://freshrpms.net for search engines and help.

What if you can't remember a package's name? Use the output from the rpm command and grep to filter out what you don't need, like so:

```
rpm -qa | grep string
```

What about the problem of finding the package from which a particular file was installed? For example, if the /etc/krb.conf file were somehow damaged, you could find the package it came from with this command:

```
rpm -qf /etc/krb.conf
```

This returns the following output:

```
krbafs-1.1.1-1
```

**ALERT**

The use of the -f option requires the full path and filename of the queried file. That's how it's listed in the package information queried from the database. Failure to include the full path for a queried file when answering a fill-in-the-blank question causes it to be marked wrong.

## Building RPMs

For the process of the exam, building RPMs simply requires a set of steps to understand. The actual process of building RPMs can be much more complex than you see here.

Sysadmins use source RPMs and build custom RPMs for better performance, a guarantee of what's in the RPM files, security of their environment, the integrity of machines, and many other reasons.

A tree of directories makes up the build environment and can be found in the `/usr/src/redhat` directory as subdirectories. These include
- **BUILD** -- This is where the source for the package is uncompressed to and the software is built.
- **RPMs** -- Binary package files that are created by the build process are written to this directory.
- **SOURCES** -- This contains the source packages, any patches, and fixes.
- **SPECS** -- This is where .spec files (essentially a glorified makefile) are kept and the build is initiated from.
- **SRPMS** -- This is where any source packages generated by the build process are stored.

### What Happens in a Build?

The first step is to download the source .rpm or the tarball of compressed code. The steps are the same for both, except a .spec file must be built for the tarball of source code, whereas a source .rpm has all that included.

If it's a source .rpm, you install the .rpm file (`rpm -i source_pkg.rpm`), which places the source files in the /usr/src/redhat/SOURCES directory and the spec file in the /usr/src/redhat/SPECS directory.

Then you edit the /usr/src/redhat/SPECS/somepkg.spec file to make any changes you require. The .spec file consists of a set of information and macros, paths to the files to include, and the installation instructions for the package when it’s installed as an .rpm file.

Here’s an example of a .spec file:

```
# Preamble of spec file
Summary: a special program to do something.
Name: blah-woof
Version: 0.99
Release: 33
Copyright: GPL
Group: Applications/Special
Source: ftp://ftp.brunson.org/blahwoof.tar.gz
BuildRoot: /var/tmp/blahwoof-root

description
Blah-woof is the greatest program it does everything and nothing

prep
rm -rf $RPM_BUILD_DIR/blah-woof-1.0
tar xzf $RPM_SOURCE_DIR/blah-woof-1.0.tar.gz

build
make

install
rm -rf $RPM_BUILD_ROOT
mkdir -p $RPM_BUILD_ROOT/usr/{bin,man/man1}
make DESTDIR=$RPM_BUILD_ROOT install

clean
rm -rf $RPM_BUILD_ROOT

files

doc README
/usr/bin/blah-woof
/usr/bin/blah.inc
/usr/man/man1/blah-woof

changelog
* Wed 10th of Nov. Some developer <some@uy.int>
- fixed tendency to crash unexpectedly
```

For the file to be used to install a package, it must contain the following sections:
- Preamble—The summary and other information that shows up in a query of the info page for the package.
- description—This is just a description.
- prep—This is where the source tarballs are unpacked and processed into the build directory (including any patches that were applied).
- build—This is where the actual software is built, usually with a make command, just like regular software.
- install—The instructions that constitute the installation for the source files, usually a make install.
