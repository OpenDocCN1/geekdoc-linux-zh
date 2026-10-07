# v.4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

```
root@forensic1:# ddrescue -r3 -d /dev/sdj bad_disk.raw bad_log.txt
GNU ddrescue 1.21
Press Ctrl-C to interrupt mapfile
Initial status (read from mapfile)
rescued: 21474 MB,  errsize: 0 B,  errors: 0
```

Current status

```
ipos: 6579 KB, non-trimmed: 0 B, current rate: 62464 B/s
opos: 6579 KB, non-scraped: 0 B, average rate: 62464 B/s
on-tried: 0 B, errsize: 3072 B, run time: 1s
rescued: 21474 MB, errors: 1, remaining time: 1s
percent rescued: 99.99% time since last successful record: 0s
Finished
```

```
root@forensic1:~ cat bad_log.txt
# Mapfile. Created by GNU ddrescue version 1.21
# Command line: ddrescue -r3 -d /dev/sdj bad_disk.raw bad_log.txt
# Start time: 2017-05-31 15:47:59
# Current time: 2017-05-31 15:47:59
# Finished
# current_pos current_status
0x00646400 +
# pos size status
0x00000000 0x00645A00 +
0x00646600 0x04F9B9A00 + -
```

```
root@forensic1:~ echo "$((0x0000C00))"
3072
```

The output show that our file "non-trimmed" areas are now 0, and the error size is 3072 bytes. Looking at the mapfile, we see that a section of the disk is marked with the "-", indicating bad hardware blocks, which in this case are unrecoverable. The size in the map file (0x000C0) matches the errsize in the output (3072). This means we have 6 bad sectors (512 bytes each).

While we were not able to obtain the entire disk in this example, hopefully you recognize the benefits of the approach we take using ddrescue to get the good data first while recovering as much as we can before accessing and potentially causing additional damage to bad areas of the disk.