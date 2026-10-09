What fresh madness is this? We try to get the FreeBSD source code and instead get a certificate error?

Compare the certificate fingerprint shown to the server's fingerprint on the FreeBSD.org website. If it matches, permanently accept the certificate by entering p. Filenames of source code files will stream past your terminal.

Once svnli te(1) finishes, take a look in `/usr/src`.

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

# Updating Source Code

So you built FreeBSD yesterday? Cool. But now you want to build today's version.

The good news is, Subversion needs only to update the code you've downloaded, not download the whole source code tree. The better news is, the source code records where you got it from and what branch it's supposed to be from in the .svn directory. This makes updating much simpler than the initial download.

FreeBSD has integrated the Subversion commands into the source code. All you'll need to do is tell the system that it may call svnli te(1) for updates by setting SVN_UPDATE in /etc/src.conf.

```
# echo 'SVN_UPDATE=yes' >> /etc/src.conf
```

Now run `make update` to get the latest source code.