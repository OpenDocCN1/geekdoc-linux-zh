
## CSUP, CVSUP, CVS, SUP, AND CTM?

Documentation on the internet unfortunately survives well past reason and rises to sow confusion at the worst possible time. Undead FreeBSD documentation and third-party tutorials might mention using a tool called `CVS` or `CVSup` for source code updates. These tools were replaced in 2013. Any mention of these programs indicates you're reading old docs. If you see a mention of CTM, you're reading docs that predate CVS.

Upgrading from source requires console access. You won't always need it, but recovering from a bad build might require intervention at the keyboard. Test your serial console, Java app, or IPMI console before installing your home-built operating system version. In my experience, the only upgrades that require console access are those where I don't have console access.

### Which Source Code?

Every FreeBSD release ships with the source code used to build the system you're installing. If you didn't choose to install the source when installing the system, you'll find it on the install media in `/usr/freebsd-dist/src.txz`. If you did install the source code, you'll find it in `/usr/src`.

Unfortunately, this version of the source code lacks the version control tags needed to build FreeBSD. It's for reference only. You'll need to use svnlite(1) to download a version of the code with those tags intact.

Is your copy of source code in `/usr/src` suitable for building FreeBSD? Ask svnlite(1).

```
# svnlite info /usr/src
svn: E155007: '/usr/src' is not a working copy
```

The “not a working copy” error means that any source code here can’t be used with Subversion.

The svnlite(1) command to grab source code looks like so.

```
# svnlite checkout \*svn.freebsd.org/@repository/@branch @locadir
```

The mirror is a FreeBSD Subversion mirror. The mirror svn.FreeBSD.org is a geo-routed alias for the closest subversion mirror.

The repository is the group of code you’re working with. You can get a complete list of current repositories at https://svnweb.FreeBSD.org/. The main Project repositories include base, for the operating system; doc, for documentation; and ports, for the Ports Collection.

The branch is the version of FreeBSD you want. For the very latest stumpy-fingered current, use head. To get a stable version, use the branch stable/ followed by the major release. FreeBSD 12-stable would be stable/12. To get a release plus all current patches, use releng/ and the release number. The fully patched FreeBSD 12.2 would be at releng/12.2.

If you have trouble figuring out which branch you need, wander through https://svnweb.freebsd.org/. The branch literally tells svnlite(1) which subdirectory to grab from this site.

Finally, the locadir is the local directory where I want to put the source code.

This host is running FreeBSD 11.1. I want to be adventuresome and move up to FreeBSD 11-stable. Here’s how I’d do that:

```
# svnlite checkout https://svn0.us-east.FreeBSD.org/base/stable/11 /usr/src/

Error validating server certificate for 'https://svn0.us-east.freebsd.org:443':
  - The certificate is not issued by a trusted authority. Use the
    fingerprint to validate the certificate manually!
Certificate information:
  - Hostname: svn0.freebsd.org
  - Valid: from Jul 29 22:01:21 2013 GMT until Dec 13 22:01:21 2040 GMT
  - Issuer: svn0.freebsd.org, clusteradm, FreeBSD.org, CA,
    US(clusteradm@freebsd.org)
  - Fingerprint: 1C:BD:85:95:11:9F:EB:75:A5:4B:C8:A3:FE:08:E4:02:73:06:1E:61
(R)eject, accept (t)emporarily or accept (p)ermanently? p
```

What fresh madness is this? We try to get the FreeBSD source code and instead get a certificate error?

Compare the certificate fingerprint shown to the server's fingerprint on the FreeBSD.org website. If it matches, permanently accept the certificate by entering p. Filenames of source code files will stream past your terminal.

Once svnlite(1) finishes, take a look in `/usr/src`.

```
# ls /usr/src/
COPYRIGHT	cddl	sbin
LOCKS	contrib	secure
MAINTAINERS	crypto	share
Makefile	etc	sys
Makefile.inc1	gnu	targets
Makefile.libcompat	include	tests
Obsoletedfiles.inc	kerberos5	tools
README	lib	usr.bin
README.md	libexec	usr.sbin
UPDATING	release	
bin	rescue
```

This is the top directory of the FreeBSD source tree, which contains all the code needed to build your chosen FreeBSD version.

## Updating Source Code

So you built FreeBSD yesterday? Cool. But now you want to build today's version.

The good news is, Subversion needs only to update the code you've downloaded, not download the whole source code tree. The better news is, the source code records where you got it from and what branch it's supposed to be from in the .svn directory. This makes updating much simpler than the initial download.

FreeBSD has integrated the Subversion commands into the source code. All you'll need to do is tell the system that it may call svnlite(1) for updates by setting SVN_UPDATE in /etc/src.conf.

```
# echo 'SVN_UPDATE=yes' >> /etc/src.conf
```

Now run `make update` to get the latest source code.

```
# cd /usr/src
# make update
```

You'll see the same sorts of updates flow past. These updates will be much quicker than the original download, though.

## Building FreeBSD from Source

Once you have the latest source code, look at /usr/src/UPDATING. The beginning of this file lists, in reverse chronological order, any warnings and special notices about changes to FreeBSD that are of special interest to people who build from source. These notes tell you whether you must take any particular actions before rebuilding your system or whether any major system functionality has changed. If you want your system to work after the upgrade, follow these instructions exactly.

The end of the UPDATING file gives the official instructions for building FreeBSD from source. The procedure described in this book has been used since FreeBSD 6-current, which changed only slightly from 5-current, but I still recommend double-checking the instructions herein against those in UPDATING.

If you use a custom kernel, also examine the new GENERIC or NOTES kernel configuration files for any new options or interesting kernel changes.

> CUSTOMIZING YOUR FREEBSD BUILD
> Remember back in Chapter 16 when we discussed /etc/make.conf ? FreeBSD uses a separate file to handle customizations for building FreeBSD itself. While settings in /etc/make.conf affect all software built on the system, anything in /etc/src.conf affects only building FreeBSD from source.

If you hang around the FreeBSD community for a while, you'll hear all sorts of stories about special methods people use for building FreeBSD. You'll hear anecdotal evidence that one method is faster, more efficient, or somehow mystically “better” than the standard. While you are certainly free to use any build method that strikes your fancy, the only method supported by the FreeBSD Project is that documented at the end of `/usr/src/UPDATING`. If you follow some other procedure and have trouble, you'll be referred to the documented procedure.

## Build the World

First, build the new userland:

```
# cd /usr/src
# make buildworld
```

The `make buildworld` command builds from source the basic tools needed to build the system compiler and then builds the compiler and associated libraries. Finally, it uses the new tools, compiler, and libraries to build all the software included in a core FreeBSD install. (This is much like building a car starting with the instruction, “Dig iron ore out of the ground.”) The buildworld places its output under `/usr/obj`. It can take anywhere from one to several hours, depending on your hardware. You can continue working normally as the buildworld runs, if your hardware is robust enough; while the build consumes system resources, it won't take any of your attention.

When the buildworld finishes, confirm that it completed without errors. If the build ends with a bunch of messages like those you see during a failed kernel compile, do not proceed with the upgrade. If you can't figure out why the build failed, go to Chapter 1 to see how you can get help. Never attempt to install a damaged or incomplete upgrade.

### PARALLEL MAKE WORLD

Experienced sysadmins have probably used the `-j` flag of `make(1)` to increase build speed. This starts multiple build
