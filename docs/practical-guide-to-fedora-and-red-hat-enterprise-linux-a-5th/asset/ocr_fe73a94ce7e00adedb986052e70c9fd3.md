# QUERYING PACKAGES AND FILES

The rpm utility can be run from the command line. Use rpm -qa to display a list of one-line summaries of all packages installed on the system (any user can run this utility). Give the command rpm -q, followed by the name of the package, to display more information about a particular package. For instance, rpm -q nis tells you whether NIS is installed and, if so, which version. Use the -ql options to list the files in a package.

```
```
$ rpm -q nis
package nis is not installed

$ rpm -ql logrotate
/etc/cron.daily/logrotate
/etc/logrotate.conf
/etc/logrotate.d
/usr/sbin/logrotate
/usr/share/doc/logrotate-3.7.8
/usr/share/doc/logrotate-3.7.8/CHANGES
/usr/share/doc/logrotate-3.7.8/COPYING
/usr/share/man/man8/logrotate.8.gz
/var/lib/logrotate.status
```
```

With the -qi options, rpm displays information about a package:

```
```
$ rpm -qi logrotate
Name          : logrotate                       Relocations: (not relocatable)
Version       : 3.7.8                           Vendor:       Fedora Project
Release       : 4.fcl2                         Build Date:   Thu Sep 17 02:43:34 2009
Install Date  : Tue Sep 22 11:40:43 2009        Build Host:   x86-4.fedora.phx.redhat.com
Group         : System Environment/Base         Source RPM:   logrotate-3.7.8-4.fcl2.src.rpm
Size          : 79680                           License:     GPL+
Signature     : (none)
Packager      : Fedora Project
Summary       : Rotates, compresses, removes and mails system log files
Description   :
The logrotate utility is designed to simplify the administration of
log files on a system which generates a lot of log files. Logrotate
allows for the automatic rotation compression, removal and mailing of
log files. Logrotate can be set to handle a log file daily, weekly,
monthly or when the log file gets to a certain size. Normally,
logrotate runs as a daily cron job.
```
```

Install the logrotate package if you need a utility to deal with the log files on your system.

You can use the -qf options to determine which package a file belongs to. The following command shows that more is part of the util-linux package:

```
```
$ rpm -qf /bin/more
util-linux-ng-2.16-10.2.fcl2.i686
```
```

Include the -p option with other options to query an uninstalled rpm package file.