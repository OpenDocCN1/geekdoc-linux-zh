```
/usr/lib/amanda/sendbackup:gntar
/usr/lib/amanda/run tar
README
COPYRIGHT
docs/INSTALL
docs/ SYSTEM .NOTES
docs /WHATS .NEW
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