```
310 1 /var/tmp/sh1649.1
343 1 /var/tmp/sh1649.2
166 1 /var/tmp/sh1649.3
440 1 /var/tmp/sh1649.4
611 1 /var/tmp/swagent.log
0 1 /var/tmp/sysstat_em.fmt
22734848 1 /var/tmp/vmunix.noreloc
#
# cat /tmp/backupgraph
i/var/tmp
#
# cat /tmp/backuplog.010829.15:08
fbackup(1417): cannot open the dates file /var/adm/fbackupfiles/dates
for reading
fbackup(1004): session begins on Wed Aug 29 15:08:10 2001
fbackup(3203): volume 1 has been used 1 time(s)
fbackup(3024): writing volume 1 to the output file /dev/rmt/0m
fbackup(1423): WARNING: could not open the dates file /var/adm/fbackup-
files/dates for writing
fbackup(1030): warnings encountered during backup
fbackup(3055): total file blocks read for backup: 44432
#
```

The two files with the date appended *(8/29/01 time 15:08)* to the end of the filename were produced by the **fbackup** command issued earlier. The date appended to the end of the file can help in the organization of backup files. We could restore any or all of these files with **frestore**.

The backup of vPar *cable1* to the local tape drive is a backup of the system with a hostname of *cvhdcn3*. The other vPar running on this system, *cable2*, was not included in the backup because its host, *cvhdcn4*, is viewed as a separate system. In the next section we'll see how we would backup *cable2* to the tape drive dedicated to *cable1*.

# ## Backup to a Tape Drive on a Different Local Virtual Partition

The tape drive in the preceding section was connected to *cable1* and used to backup *cable1*. Let's now backup *cable2* with the tape drive as part of the *cable1* Virtual Partition. Keep in mind that vPar *cable2* with its hostname