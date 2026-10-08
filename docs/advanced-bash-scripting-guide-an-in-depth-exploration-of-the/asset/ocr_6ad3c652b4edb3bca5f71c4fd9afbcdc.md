# Advanced Bash-Scripting Guide

```
file_name=$(stat -cn "$FILENAME") # Same as "$FILENAME" of course.
file_owner=$(stat -cU "$FILENAME")
file_size=$(stat -c "$FILENAME")
# Certainly easier than using 'ls -l "$FILENAME'
# with sed.
file_inode=$(stat -ci "$FILENAME")
file_type=$(stat -cf "$FILENAME")
file_access_rights=$(stat -cA "$FILENAME")
```

```
echo "File name: $file_name"
echo "File owner: $file_owner"
echo "File size: $file_size"
echo "File inode: $file_inode"
echo "File type: $file_type"
echo "File access rights: $file_access_rights"
```

```
exit 0
```

```
sh fileinfo2.sh
```

```
File name: testfile.txt
File owner: bozo
File size: 418
File inode: 1730378
File type: regular file
File access rights: -rw-rw-r-
```

vmstat

Display virtual memory statistics.

```
vmstat
procs memory swap io system cpu
r b w swpd free buff cache si bo in cs us sy id
0 0 0 0 11040 2636 38952 0 0 33 7 271 88 8 3 8 9
```

uptime

Shows long the system has been running, along with associated statistics.

```
uptime
10:28pm up 1:57, 3 users, load average: 0.17, 0.34, 0.27
```

> A load average of 1 indicates that the system handles processes immediately. A load greater than 1 means that processes are being queued. When the load averages above 3 (on a single-core processor), system performance significantly degrades.

hostname

Lists the system name. This command sets the host name in /etc/rc.d setup script (/etc/rc.d/rc.sysinit or similar). It is equivalent to hostname -n, and a counterpart to the $HOSTNAME internal variable.

```
bash hostname
localhost.localdomain

bash echo $HOSTNAME
localhost.localdomain
```

Similar to the hostname command the domainname, dnsdomainname, nisdomainname, and ypdomainname commands. Use these to display or set the system DNS or NIS/YP domain name. Various options to hostname also perform these functions.

Chapter 17. System and Administrative Commands