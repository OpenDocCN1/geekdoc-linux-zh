```
/dev/hda8          746387  378208   329625  53% /opt
/dev/hda7         2016016 1341784   571820  70% /usr
/dev/hda6         2478138 1563570   786452  67% /usr/local
/dev/hda10         388693  34010   334604  9% /var
```

# Listing 3.4 A Printout of Disk Space in Terms of Megabyte Blocks

```
$ df -h
Filesystem   Size  Used Avail Use% Mounted on
/dev/hda1    486M  37M  424M   8% /
/dev/hda5    3.3G 1.2G  2.0G  37% /home
/dev/hda8    729M 369M  322M  53% /opt
/dev/hda7    1.9G 1.3G  558M  70% /usr
/dev/hda6    2.4G 1.5G  768M  67% /usr/local
/dev/hda10   380M  33M  327M   9% /var
```

Properly monitoring the amount of space used by each partition will help regulate the amount of space that can be allocated to each user. This also helps to prevent one partition from becoming overloaded. If you know that a partition is quickly approaching maximum capacity, you can take preventative action such as further reducing disk use, adding additional hard drives, or repartitioning existing drives. Knowledge of what your users are doing on your system is the key to keeping it operating at its optimal level.

# Conclusion

This chapter covered the most basic commands associated with viewing files and directories as well as moving and copying those files within differing locations. This chapter also highlighted how Red Hat Linux lays out certain file structures and what types of files each separate directory contains. You also learned what types of files exist under Linux and how you can modify file permissions and ownerships. Lastly, you examined how you can control and monitor the amount of disk space on a Linux drive.

This chapter covered the basics for initial navigation and preliminary system administration. It was designed for beginning users who need to understand how files function under the Linux operating system.