
# 18.1.2 Using Tripwire

Once the `twpol.txt` file has been edited, it is time to create the secure version of this file. The Tripwire documentation says to “Make sure that the integrity of the system you are running has not been compromised.” It further suggests that the operating system (Linux) and application files should be installed from original media (CD-ROM) to get a clean baseline; that is, be guaranteed not to have any Trojans. Well, it is a bit late for that unless you want to reformat your disk and start again. However, “Speeding Up the Check with RPM” on page 494 discusses how to use Red Hat’s RPM program to validate that the installed packages have not been tampered with.

Issue the command

```
cd /usr/TSS/bin
./twadmin --create-polfile ../policy/twpol.txt
```

to create the cryptographically safe version of this file, which is signed cryptographically to prevent tampering, and placed in `/usr/TSS/policy/tw.pol`.

Now, initialize the database with the following command:

```
/tripwire --init
```

Test e-mail with this command:

```
/tripwire --test --email root
```

To run a file system integrity check (check the file system for changes), issue the command

```
/tripwire -m c
```

or

```
/tripwire --check
```

It will take a few minutes to check every file on your system, output a report to standard output, and store a report in `/usr/TSS/report/hostname-date.twr`. A copy of this report can be generated to standard output at any later time with

```
twprint --print-report -r ../report/report_file.twr
```

The amount of detail may be specified with the `-t` flag, which takes an argument of between 0 and 4. Increasing numbers mean increasing detail. The following would make a good entry to root's crontab, to be invoked shortly before you normally arrive at the office (or the day's heavy loads starts):

```
/tripwire -m c -r /usr/TSS/report/nightly.twr \
2>&1 mailx -s TRIPWIRE root
```

After reviewing it in the morning (if any changes other than the usual log file access occurs), you could then use the command

```
/tripwire -m u -r /usr/TSS/report/nightly.twr
```

It will "pop" you into the editor where each changed entry has an [x] entry to indicate the default of updating the database to expect the newly altered version. If you replace the "x" with a space, it will not update the database for that entry. You would change the [x] to [ ] for a change that either is unauthorized or requires further research. If your configuration is such that you have not allowed for log files changing, this "update" report makes the previous "check" redundant.

A text version of the scheme and encoded policy (rules) file may be generated with

```
/twadmin --printpolfile ../policy/policy.txt
```

If Tripwire complained about missing files, edit them out of this file. Then update the default policy with this new policy:

```
/tripwire -m p --secure-mode low ../policy/policy.txt
```

The `/bin/date` program is supposed to be mode 755. If you issue the command

```
chmod 711 /bin/date
```

the program will be altered but not broken. A subsequent

```
/tripwire -m c
```

will include the following in its reports.

| Rule Name | Severity Level | Removed | Modified |
| --- | --- | --- | --- |
| * OS execs and libs | 100 | 0 | 0 | 1 |

Modified:
"/bin/date"

Note that Tripwire did not bother to report what changed about the `/bin/date` file even though it knows. Even my "one liners" in the previous section provided more useful information.

# 8.19.3 What Tripwire Cannot Protect From

Earlier versions of Tripwire talked about the necessity of keeping the program and database on Read/Only media to prevent tampering by crackers. It now proudly states that because the database and trusted files are cryptographically signed, this no longer is necessary. This author disagrees. If a cracker is sophisticated enough to tamper with Tripwire's database by "updating" it to not notice her Trojans, she could be sophisticated enough to install a Trojaned version of Tripwire. This Trojan version could prompt the SysAdmin for the passphrases in the usual places and proceed to alter the database and re-sign it or pretend that nothing has been altered.

A very sophisticated cracker could add Trojan horses to tripwire, /bin/sh, and even the kernel. This situation would not be detected by the standard usage of Tripwire (trusting the on-disk copies). When you have reason to believe that a sophisticated cracker has attacked, or periodically "just in case," the following is suggested. Create Tripwire-specific rescue disks. Boot the rescue disks and run that absolutely trusted Tripwire executables and database. Clearly, this trusted database must be updated periodically and it is not acceptable simply to copy it from the "regular" one on hard disk because that one is not completely trustworthy.

# 8.19.4 Replacements for Tripwire

There are several open source competitors to Tripwire. AIDE may be downloaded from `ftp://ftp.linux.hr/pub/aide/`.

The current version is `aide-0.7.tar.gz`.

The sparse manual is available from `www.cs.tut.fi/~rammer/aide/manual.html`.

Trojan horses do not have a ghost of a chance if you use the samhain file integrity checker from the CD-ROM or from `www.la-samhna.de/samhain.index.html`.

Also, there is Gog&Magog, which may be downloaded from `www.multimania.com/cparisel/gog/` and Sentinel, which has a nice optional GUI front end, at `http://zurk.sourceforge.net/zfile.html`.

SuSeaudit operates from a bootable disk to provide very secure integrity checking. It is standard with SuSE and can be ported easily to other distributions. Download it from `www.suse.de/-marc/`.

# 8.20 Detecting Executables

A cracker certainly does not want you to have a copy of his Trojan horse. Besides wanting to keep his techniques secret, it would be evidence that might get him the IP address of the system that he is working from. A common technique that a cracker uses to prevent your “capturing” an executable is simply to remove it from disk. As will be discussed in “Finding the Cracker’s Running Processes” on page 466, removing it from disk will not terminate the already running executable.

Starting in the 2.2 kernel, a symbolic link from /proc/PID/exe to the actual executable is provided. Additionally, it indicates the executable has been removed from the file system by appending “(deleted)” to the name! This example shows what such deleted executable will like.

```
$ file /proc/519/exe
/proc/519/exe: broken symbolic link to /home/mr_ed/foo (deleted)
```

The following command may be invoked periodically, possibly from cron, to detect any instances of these:

```
# file /proc/[0-9]*/exe|grep ‘(deleted)’
/proc/519/exe: broken symbolic link to /home/mr_ed/foo (deleted)
```

A very useful feature in the kernel is this symbolic link in /proc is good for reading though the original file has been removed! This allows you to make a copy of the file for analysis as simply

```
cp /proc/519/exe /home/samspade/del_cracker
```

You could make copies of these automatically via the following script, that I call `getdel.csh`; it is on the CD-ROM. It `dd` instead of `cp` simply because `dd` is likely to be compromised by crackers because it is not as well known.

```
#!/bin/csh -f
# Detect and copy running executables from deleted disk.
# DANGER: this program must run as root to capture all
# data but if it finds something root *may* be compromised.
#
# Optionally kills the program.
# Requires kernel 2.2 or newer.
#
# Copyright 2001 Bob Toxen. All rights reserved.
# This program may be used under the terms of the
# GNU GENERAL PUBLIC LICENSE Version 2.
#
# Offered as is with no warranty of any kind.
set savdir=/sampsade/delexe_dir
set emailaddr=sampsade@pentacorp.com
set g='$(deleted)'
set s='s;./proc/([0-9][0-9]*\).*,\1'
set p='$(file /proc/[0-9]*/exe|grep "$g"|sed "$s")'
umask 077
foreach i ( $p )
if ( ! -f $savdir/$i ) then
techo /bin/dd if=/proc/$i/exe=$savdir/$i
echo /bin/dd if=/proc/$i/exe=$savdir | i |
/bin/mail -s 'DEL' $emailaddr
/bin/dd if=/proc/$i/exe=$savdir/$i >& /dev/null
/bin/ls -1 /proc/$i/exe >$savdir/$ls
# Uncomment next line to kill it automatically
/bin/kill -9 $i
else
echo already captured /proc/$i/exe
endif
end
```

# 8.21 Detecting Promiscuous Network Interface Cards

A simple script, presented here, will detect a system's network interface card (sometimes a NIC or Ethernet card) in Promiscuous mode. An alternative would be to add appropriate entries in /etc/syslog.conf to log the kernel-generated messages that NIC drivers generate when a card is placed into Promiscuous mode, watch the appropriate log for this kernel message, and have yourself notified by e-mail and pager when this happens. See "Promiscuous Kernel Messages" on page 581 for details on the messages, by driver, and "Paging the SysAdmin: Cracking on Progress!" on page 358 for details on how to arrange the e-mail and pager notification.

The following csh script, called `promisc`, will scan the eth0 and eth1 cards every hour and generate e-mail if a card is in Promiscuous mode. It eth0 is usable from any shell. The promisc script will be described shortly.

```
#!/bin/csh -f
set devs=(eth0 eth1)
loop:
foreach i ( $devs
```
