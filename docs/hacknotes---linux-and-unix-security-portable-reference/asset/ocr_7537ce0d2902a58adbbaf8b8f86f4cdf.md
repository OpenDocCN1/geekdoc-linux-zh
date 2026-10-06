After noticing that "joe" belongs to the group "proj1," the intruder may issue the following command, which will list all the files owned by the "proj1" group:

```
$bash$ find / -group proj1 -print 2> /dev/null
/var/proj1/main.c
/var/proj1/main.o
/var/proj1/README
/var/proj1/pass.txt
/var/log/proji
```

Now, the intruder knows exactly what "proj1" files "joe" has access to. One of these files, pass.txt, may seem pretty interesting:

```
$bash$ more /var/proj1/pass.txt
Note that this program authenticates to the MySQL database with the system password "r00t3rp455.w."
```

Administrators often reuse passwords. If the victim's root password was the same as the MySQL password shown in the preceding note, the intruder may gain root privileges by issuing the command:

```
$bash$ su
Password:r00t3rp455
$bash# id
uid=0(root) gid=0(root) groups=0(root), 1(bin), 2(daemon), 3(sys), 4 (adm), 6(disk), 10(wheel)
```

# Find World-Readable and -Writable Files

In addition to searching for world-readable files, it is also possible to search for world-readable files that a user may have access to. For example, here is how you would search for all world-readable files present in the /etc directory:

```
$bash$ find /etc -type f -perm -4 -print 2> /dev/null
```

Many files in /etc should not be world-readable. For example, the /etc/shadow file contains encrypted passwords of users. Anyone with access to this file may use brute-force crack user passwords using tools like John the Ripper.

An intruder may attempt to search for world-writable files by issuing the following command:

```
$bash$ find / -type f -perm -2 -print 2> /dev/null
/usr/sbin/in.telnetd
```