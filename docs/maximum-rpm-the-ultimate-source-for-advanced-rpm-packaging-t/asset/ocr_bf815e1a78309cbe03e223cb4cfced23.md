```
-rw-r--r--    1 root     root       16384 Oct 17 20:50 providesindex.rpm
-rw-r--r--    1 root     root       16384 Oct 17 20:50 requiredby.rpm
#
```

You'll notice that packages.rpm decreased in size. This is due to a side-effect of the --rebuilddb option. While it is going through the database, it is getting rid of unused portions of the database. Our example was performed on a newly installed system where only one or two packages have been upgraded, so the reduction in size was small. For a system that has been through a complete upgrade, the difference would be more dramatic.

Does this mean that you should rebuild the database every once in a while? Not necessarily. Since RPM eventually will make use of the holes, there's no major advantage to regular rebuilds. However, when an RPM-based system has undergone a major upgrade, it certainly wouldn't hurt to spend a few minutes using --rebuilddb to clean things up.

# 8.1.2. --initdb: Create a New RPM Database

If you are already using RPM, the --initdb option is one you'll probably never have to use. The --initdb option is used to create a new RPM database. That's why you'll probably not need it if you're already using RPM. You already have an RPM database.

It might seem that the --initdb option would be dangerous. After all, won't it trash your current database if you mistakenly use it? Fortunately, the answer is no. If there is an RPM database in place already, it's still perfectly safe to use the option, even though it won't accomplish much. As an example, here's a listing of the files that make up the RPM database on a Red Hat Linux system:

```
# ls /var/lib/rpm
total 3559
-rw-r--r--    1 root     root       16384 Jan  8 22:10 conflictsindex.rpm
-rw-r--r--    1 root     root      1351680 Jan  8 22:10 fileindex.rpm
-rw-r--r--    1 root     root       16384 Jan  8 22:10 groupindex.rpm
-rw-r--r--    1 root     root       16384 Jan  8 22:10 nameindex.rpm
-rw-r--r--    1 root     root      2349640 Jan  8 22:10 packages.rpm
-rw-r--r--    1 root     root       16384 Jan  8 22:10 providesindex.rpm
-rw-r--r--    1 root     root       16384 Jan  8 22:10 requiredby.rpm
#
```

Next, let's use the --initdb option, just to see what it does to this database:

```
# rpm --initdb
# ls /var/lib/rpm
total 3559
-rw-r--r--    1 root     root       16384 Jan  8 22:10 conflictsindex.rpm
-rw-r--r--    1 root     root      1351680 Jan  8 22:10 fileindex.rpm
-rw-r--r--    1 root     root       16384 Jan  8 22:10 groupindex.rpm
-rw-r--r--    1 root     root       16384 Jan  8 22:10 nameindex.rpm
-rw-r--r--    1 root     root      2349640 Jan  8 22:10 packages.rpm
-rw-r--r--    1 root     root       16384 Jan  8 22:10 providesindex.rpm
-rw-r--r--    1 root     root       16384 Jan  8 22:10 requiredby.rpm
#
```