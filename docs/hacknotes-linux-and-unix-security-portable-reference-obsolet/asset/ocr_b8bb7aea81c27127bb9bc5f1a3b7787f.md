such as `newsyslog` or `logrotate`. These tools should be called on a frequent time interval using the `cron` daemon. Check the man pages for `newsyslog` or `logrotate` for more details.

# Free Space in /var

Depending upon the environment, log and spool files stored in the `/var` directory can get very big. It is a good idea to routinely check the amount of free space in `/var` using the `df` command.

The `/var` directory must be mounted as a separate partition. Please see the “Disk Partitions” section in Chapter 8 for more information.

# PATCHING

It is most important to stay up-to-date with software patches and updates. Mailing lists such as Bugtraq often list software vulnerabilities, and these are quickly fixed by software vendors. Depending upon your distribution and package management tools, these patches may be found in various locations. The table that follows lists the most popular Unix and Linux distributions, along with resources on where to obtain software patches:

| Distribution | Patches |
| :--- | :--- |
| AIX | <http://techsupport.services.ibm.com/rs6000/fixes> |
| BSDI | <http://www.bsdI.com/services/support/patches/> |
| Caldera OpenLinux | <ftp://ftp.calderasystems.com/pub/updates/OpenLinux/> |
| Debian Linux | <http://www.debian.org/security/> |
| FreeBSD | <ftp://ftp.freebsd.org/pub/FreeBSD/releases/> |
| IRIX | <http://www.sgi.com/support/security/> |
| HP Unix | <http://us-support.external.hp.com/> |
| Mandrake Linux | <http://www.linux-mandrake.com/en/security/> |
| NetBSD | <http://www.netbsd.org/Security/> |
| OpenBSD | <ftp://ftp.openbsd.org/pub/OpenBSD/patches/> |
| Red Hat Linux | <http://www.redhat.com/support/errata/> |
| Slackware Linux | <ftp://ftp.slackware.com/pub/slackware/> |
| Solaris | <ftp://sunsolve1.sun.com/pub/patches/> |
| SuSE Linux | <http://www.suse.com/us/support/security/index.html> |