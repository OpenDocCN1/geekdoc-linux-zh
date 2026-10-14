# The /var Directory

Since the FSSTND requires that you be able to mount /usr read-only, any programs that write log files or need spool or lock directories probably should write them to the /var directory. The FSSTND states "/var is for ... variable data files. This includes spool directories and files, administrative and logging data, and transient and temporary files." The following directories should be subdirectories of /var:

+   /var
+     |- log
+     |- catman
+     |- lib
+     |- local
+     |- named
+     |- nis
+     |- preserve
+     |- run
+     |- lock
+     |- tmp
+     +- spool
+       |- at
+       |- cron
+       |- lpd
+       |- mail
+       |- mqueue
+       |- rwho
+       |- small
+       |- uucp
+       +- news

System log files such as wtmp and lastlog go in /var/log. The /var/lib directory also contains the RPM system databases. Formatted man pages go in /var/catman, and lock files go in /var/lock. The /var/spool directory has subdirectories for various systems that need to store data files.

```
|- info
|- lib
|- man
|- sbin
+- src
```