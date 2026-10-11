
## Finding dependencies...
Requires (1): dump
1 block
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/i386/amanda-client-2.3.0-1.i386.rpm

## Binary Packaging: amanda-server-2.3.0-1
Finding dependencies...
1 block
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/i386/amanda-server-2.3.0-1.i386.rpm

```bash
+ umask 022
+ echo Executing: %clean
Executing: %clean
+ cd /usr/src/redhat/BUILD
+ cd amanda-2.3.0
+ exit 0
```

## Source Packaging: amanda-2.3.0-1
- amanda-2.3.0.spec
- amanda-2.3.0-linux.patch
- amanda-2.3.0.tar.gz

374 blocks
Generating signature: 0
Wrote: /usr/src/redhat/SRPMS/amanda-2.3.0-1.src.rpm

Great! Let's take a look at our handiwork:

```bash
# cd /usr/src/redhat/RPMS/i386/
# ls -l
total 2
-rw-r--r-- 1 root root 1246 Nov 20 21:19 amanda-client-2.3.0-1.i386.rpm
-rw-r--r-- 1 root root 1308 Nov 20 21:19 amanda-server-2.3.0-1.i386.rpm
#
```

Hmmm, those binary packages look sort of small. We'd better see what's in there:

```bash
# rpm -qiUp amanda-*-1.i386.rpm
Name    : amanda-client       Distribution: (none)
Version : 2.3.0              Vendor: (none)
Release : 1                  Build Date: Wed Nov 20 21:19:44 1996
Install date: (none)         Build Host: moocow.rpm.org
Group   : System/Backup      Source RPM: amanda-2.3.0-1.src.rpm
Size    : 0
Summary : Client-side Amanda package
Description :
The Amanda Network Backup system contains software necessary to
automatically perform backups across a network. Amanda consists of
two packages -- a client (this package), and a server:

The client package enable a network-capable system to have its
filesystems backed up by a system running the Amanda server.
```

NOTE: In order for a system to perform backups of itself, install both the client and server packages!

(contains no files)

Name : amanda-server
Version : 2.3.0
Release : 1
Install date : (none)
Group : System/Backup
Size : 0
Summary : Server-side Amanda package
Description :
The Amanda Network Backup system contains software necessary to automatically perform backups across a network. Amanda consists of two packages -- a client, and a server (this package):

Distribution: (none)
Vendor: (none)
Build Date: Wed Nov 20 21:19:44 1996
Build Host: moocow.rpm.org
Source RPM: amanda-2.3.0-1.src.rpm

The server package enables a network-capable system to control one or more Amanda client systems performing backups. The server system will direct all backups to a locally attached tape drive. Therefore, the server system requires a tape drive.

NOTE: In order for a system to perform backups of itself, install both the client and server packages! (contains no files)

What do they mean, (contains no files)? The spec file has perfectly good %files lists....

Oops.

### 20.4.1. Creating the %files List

Everything was going so smoothly, we forgot that the %files lists were going to need files. No problem; we just need to put the filenames in there, and we'll be all set. But is it really that easy?

### 20.4.1.1. How to Find the Installed Files

Luckily, it's not too bad. Since we saved the output from our first `make install`, we can see the filenames as they're installed. Of course, it's important to make sure the install output is valid. Fortunately for us, amanda didn't require much fiddling by the time we got it built and tested. If it had, we would have had to get more recent output from the installation phase.

It's time for more decisions. We have one list of installed files and two %files lists. It would be silly to put all the files in both %files lists, so we have to decide which file goes where.

This is where experience with the software really pays off, because the wrong decision made here can result in awkward, ill-featured packages. Here's the %files list we came up with for the client subpackage:

```
%files client
/usr/lib/amanda/amandad
/usr/lib/amanda/sendsize
/usr/lib/amanda/calclsize
/usr/lib/amanda/sendbackup-dump
/usr/lib/amanda/selfcheck
/usr/lib/amanda/sendbackup-gnutar
/usr/lib/amanda/run tar
README
COPYRIGHT
docs/INSTALL
docs/ SYSTEM .NOTES
docs/WHATS .NEW
```

The files in /usr/lib/amanda are all the client-side amanda programs, so that part was easy. The remaining files are part of the original source archive. Amanda doesn't install them, but they contain information that users should see.

Realizing that RPM can't package these files specified as they are, let's leave the client %files list for a moment and check out the list for the server subpackage:

```
%files server
/usr/sbin/amadmin
/usr/sbin/amcheck
/usr/sbin/amcleanup
/usr/sbin/amdump
/usr/sbin/amflush
/usr/sbin/amlater
/usr/sbin/amrestore
/usr/sbin/amtape
/usr/lib/amanda/taper
/usr/lib/amanda/dumper
/usr/lib/amanda/planner
/usr/lib/amanda/reposter
/usr/lib/amanda/getconf
/usr/lib/amanda/chg-generlc
/usr/man/man8/amanda .8
/usr/man/man8/amadmin .8
/usr/man/man8/amcheck .8
/usr/man/man8/amcleanup .8
/usr/man/man8/amdump .8
/usr/man/man8/amflush .8
/usr/man/man8/amlater .8
/usr/man/man8/amrestore .8
/usr/man/man8/amtape .8
README
COPYRIGHT
docs/INSTALL
docs/KERBEROS
docs/SUNOS4 .BUG
docs/ SYSTEM .NOTES
docs/TAPE.CHANGERS
docs/WHATS .NEW
docs/MULTITAPE
example
```

The files in /usr/sbin are programs that will be run by the amanda administrator in order to perform backups and restores. The files in /usr/lib/amanda are the server-side programs that do the actual work during backups. Following that are a number of man pages: one for each program to be run by the amanda administrator, and one with an overview of amanda.

Bringing up the rear are a number of files that are not installed, but would be handy for the amanda administrator to have available. There is some overlap with the files that will be part of the client subpackage, but the additional files here discuss features that would interest only amanda administrators. Included here is the example subdirectory, which contains a few sample configuration files for the amanda server.

As in the client %files list, these last files can’t be packaged by RPM as we’ve listed them. We need to use a few more of RPM’s tricks to get them packaged.

### 20.4.1.2. Applying Directives

Since we’d like the client subpackage to include those files that are not normally installed, and since the files are documentation, let’s use the %doc directive on them. That will accomplish two things:

- When the client subpackage is installed, it will direct RPM to place them in a package-specific directory in /usr/doc.
- It will tag the files as being documentation, making it possible for users to easily track down the documentation with a simple rpm -qd command.

In the course of looking over the %files lists, it becomes apparent that the directory /usr/lib/amanda will contain only files from the two amanda subpackages. If the subpackages are erased, the directory will remain, which won’t hurt anything, but it isn’t as neat as it could be. But if we add the directory to the list, RPM will automatically package every file in the directory. Because the files in that directory are part of both the client and the server subpackages, we’ll need to use the %dir directive to instruct RPM to package only the directory.

After these changes, here’s what the client %files list looks like now:

```
%files client
%dir /usr/lib/amanda/
/usr/lib/amanda/amandad
/usr/lib/amanda/sendsize
/usr/lib/amanda/calcsized
/usr/lib/amanda/sendbackup-dump
/usr/lib/amanda/selifecheck
/usr/lib/amanda/sendbackup-gnutar
/usr/lib/amanda/runtar
%doc README
%doc COPYRIGHT
%doc docs/INSTALL
%doc docs/SYSTEM.NOTES
%doc docs/WHATS.NEW
```

We’ve also applied the same directives to the server %files list:

```
%files server
/usr/sbin/amadmin
/usr/sbin/amcheck
/usr/sbin/amcleanup
/usr/sbin/amdump
/usr/sbin/amflush
/usr/sbin/amlabel
/usr/sbin/amrestore
/usr/sbin/amtape
%dir /usr/lib/amanda/
/usr/lib/amanda/taper
/usr/lib/amanda/dumper
/usr/lib/amanda/driver
/usr/lib/amanda/planner
/usr/lib/amanda/reporter
/usr/lib/amanda/getconf
/usr/lib/amanda/chg-generic
/usr/man/man8/amanda.8
/usr/man/man8/amadmin.8
/usr/man/man8/amcheck.8
/usr/man/man8/amcleanup.8
/usr/man/man8/amdump.8
/usr/man/man8/amflush.8
/usr/man/man8/amlable.8
/usr/man/man8/amrestore.8
/usr/man/man8/amtape.8
%doc README
%doc COPYRIGHT
%doc docs/INSTALL
%doc docs/KEBEROS
%doc docs/SUNOS4.BUG
%doc docs/SYSTEM.NOTES
%doc docs/TAPE.CHANGERS
%doc docs/WHATS.NEW
%doc docs/MULTITAPE
%doc example
```

You’ll note that we neglected to use the %doc directive on the man page files. The reason is that RPM automatically tags any file destined for /usr/man as documentation. Now our spec file has a complete set of tags, the two subpackages are defined, it has build-time scripts that work, and, now, %files lists for each subpackage. Why don’t we try that build again?

```
# rpm -ba amanda-2.3.0.spec
* Package: amanda
* Package: amanda-client
* Package: amanda-server
...
echo Executing: %build
Executing: %build
+ cd /usr/src/redhat/BUILD
+ cd amanda-2.3.0
+ make
Making all in common-src
...
+ echo Executing: %install
Executing: %install
+ cd /usr/src/redhat/BUILD
+ cd amanda-2.3.0
+ make install
Making install in common-src
...
+ echo Executing: special doc
Executing: special doc
```
