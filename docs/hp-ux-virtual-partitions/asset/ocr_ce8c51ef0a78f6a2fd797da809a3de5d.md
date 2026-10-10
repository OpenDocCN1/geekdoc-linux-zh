file that will contain the backup log. We’ll add the date and time to the end of the index and backup log files.

```
# fbackup -Ou -f /tmp/testbackup -g /tmp/backupgraph
-I /tmp/backupindex.`date '+%y%m%d.%H:%M'` 2> /tmp/backuplog.`date '+%y%m%d.%H:%M'`
#
```

Let’s now see what files were produced as a result of having issued this command. First let’s look at the backup index and backup logfiles:

```
# ls /tmp/backup*
backupgraph
backupindex.000712.15:04
backuplog.000712.15:04
# 
# cat /tmp/backupindex000712.15:04
1024          1 / 
1024          1 /var
2048          1 /var/tmp
0             1 /var/tmp/OBAMFEA01630
0             1 /var/tmp/OBAMHBAO1020
0             1 /var/tmp/OBAMHBAo1540
336           1 /var/tmp/OBAMHBAo7762
102           1 /var/tmp/aaa01112
            .
            .
            .
28            1 /var/tmp/aaaa1487
28            1 /var/tmp/envd.action2
28            1 /var/tmp/envd.action5
4608          1 /var/tmp/exclude.tmp
96            1 /var/tmp/stmp
1595          1 /var/tmp/swagent.log
205           1 /var/tmp/tmp_cfg_file
# 
# cat /tmp/backupgraph000712.15:04
1/var/tmp
# 
# cat /tmp/backuplog000712.15:04

fbackup(1004): session begins on Wed Jul 12 14:56:19 2000
fbackup(3024): writing volume 1 to the output file /tmp/testbackup
fbackup(1030): warnings encountered during backup
fbackup(3055): total file blocks read for backup: 3614
fbackup(3056): total blocks written to output file /tmp/testbackup:3876
#
```