online backup vendor or talk to your ISP. If you are hosting your Web server(s) on your own network, however, you can keep backups on another host on your network. On most Unix systems, you can run a program called \underline{r\hbox{d}i\hbox{m}} to create mirror directories of your Web sites on other Unix sites (Chapter 23 has an example of an \underline{r\hbox{d}i\hbox{s}\hbox{t}}-based site-mirroring application).

It may even be a good idea to keep a compressed version of the Web data on the Web server itself. On Unix systems, you can set up a \underline{cron} job to create a compressed \underline{tar} file of the Web data on a desired frequency. For example:

```
# for system V-\hbox{ish} Unix, weekday range is 0-6 where 0=Sunday # For BSD-\hbox{ish} system use weekday range 1-7 where 1=Monday # This example is for a Linux system (System V-\hbox{ish} cron\hbox{d}) 30 2 \ *  0,1,3,5,  root  /bin/tar czf /backup/M-W-F-Sun.tgz 30 2 \ *  2, 4,6      root  /bin/tar czf /backup/T-TH-Sat.tgz /www/*
```

If these two \underline{cron} entries are kept in /etc/crontab, then two files will be created. Every Monday, Wednesday, Friday, and Sunday, the first \underline{cron} job will run at 2:30 a.m. to create a backup of everything in /www, and it will store the compressed backup file in the /backup/M-W-F-Sun.tgz file. Similarly, on Tuesday, Thursday, and Saturday mornings (at 2:30 a.m.), the second \underline{cron} entry will create a file called T-TH-Sat.tgz in the same backup directory for the same data. Having two backups ensures that you have at least last two days' backup in two compressed files.

# # Offline backup

You should also perform backups on removable media and keep them in safe locations. Restoring from this type of backup is usually a time-consuming operation. You can use tape drives, removable hard drives (such as Jazz disks) to perform this backup. I prefer an 8-mm tape-based backup because it provides 8GB of data storage capacity; also, 8-mm tape drives have been on the market much longer than the new compact removable media.

As your Web sites grow richer in content, the available Web space is rapidly filling. This is often a consequence of files that are unused but that are never removed for fear that something (such as a link) will break somewhere. If you think this is true for your Web site, and you are on a Unix platform, you may want to consider running the \underline{find} utility to locate files that have not been accessed for a long time. For example:

```
find /www -name "*.bak" -type f -atime +10 -exec ls -l {} \;
```

This lists all files in /www directories that end with the \underline{.bak} extension and have not been accessed for the last 10 days. If you want to remove these files, you can replace the \underline{ls} -l command and do a \underline{find} such as:

```
find /www -name "*.bak" -type f -atime +10 -exec rm -f {} \;
```