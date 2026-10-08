
# 28
# acctcom

/var/adm/pacct is usually the current file to be examined; a busy system may need several files, of which all the current file are found in /var/adm/pacct. acctcom reports only on terminated processes. Use ps(1) for active processes.

# Options

-   -a Show some average statistics about the processes selected. Print the statistics after the output records.
-   -b Read backward, showing latest commands first. This option has no effect when standard input is read.
-   -C sec Show only processes with total CPU time (system-time + user-time) that exceed sec seconds.
-   -e time Show processes existing at or before time.
-   -E time Show processes ending at or before time. Using the same time for both -S and -E, show the processes that existed at time.
-   -f Print the fork()/exec() flag and show exit status columns in the output. Display the numeric output in octal.
-   -g group Show only processes belonging to group. You can designate the group by either the group ID or group name.
-   -h Instead of memory size, show the fraction of total available CPU time consumed by the process during its execution. This hog factor is computed as (total CPU time)/(elapsed time).
-   -H factor Show only processes that exceed factor, where factor is the hog factor, as explained in -h, above.
-   -i Print lines containing the I/O counts in the output.
-   -I chars Show only processes transferring more characters than the cutoff number by chars.
-   -k Instead of memory size, show total kcore-minutes.
-   -1 line Show only processes belonging to terminal /dev/term/line.
-   -m Show mean core size (the default).
-   -n pattern Show commands matching pattern that may be a regular expression, as in regcomp(3), except plus one or more occurrences.
-   -o output-file Copy selected process records in the input data format to output-file, suppress printing to standard output.
-   -O sec Show only processes with CPU system time exceeding sec seconds.
-   -q Do not print any output records, just print the average statistics, with the -a option.
-   -r Show CPU factor (user-time/(system-time + user-time)).
-   -s time Show processes existing at or after time, given in the format hr:min(sec).
-   -S time Show processes starting at or after time.

# acctcom

# 29

-   -t Show separate system and user CPU times.
-   -u user Show only processes belonging to user: You can specify a user ID, a login name that is converted to a user ID, # (which designates only those processes executed with superuser privileges), or ? (which designates only processes associated with unknown user IDs).
-   -v Exclude column headings from the output.

# Examples

The following example turns on accounting, lists the contents of the /var/adm/pacct file by using the acctcom command without any arguments, and then turns off accounting. Notice that the acctcom used to turn on accounting has a pound sign in front of it because it was run by super.

```
castle su
cast#/usr/lib/acct/acctcom /var/adm/pacct
castle exit
cast acctcom
```

| COMMAND NAME | USER | TTYNAME | START TIME | END TIME | REAL (SECS) | CPU (SECS) | MEAN SIZE(KB) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| #acct | root | pts/3 | | 12:09:16 | 12:09:12 | 0.12 | 0.05 | 543.2 |
| ls | root | pts/3 | | 12:09:21 | 12:09:21 | 0.01 | 0.01 | 748.0 |
| sh | root | pts/3 | | 12:09:29 | 12:09:29 | | 0.03 | 548.0 |
| more | root | pts/3 | | 12:09:34 | 12:09:34 | | 0.03 | 537.3 |
| acctcom | root | | 12:09:47 | 12:09:47 | 0.08 | 0.07 | 689.1 |
| dtfile | winner | ? | 12:09:59 | 12:09:59 | | 0.03 | 2510.6 |
| dtfile | winner | ? | 12:10:02 | 12:10:02 | | 0.02 | 3350.0 |
| uscheed | uucp | ? | 12:11:00 | 12:11:00 | 0.05 | 0.05 | 409.6 |
| uuxqt | uucp | ? | 12:11:00 | 12:11:00 | | 0.06 | 449.6 |
| udemon | uucp | ? | 12:11:00 | 12:11:00 | 0.15 | 0.04 | 694.0 |
| # dtfile | winner | ? | 12:13:00 | 12:13:00 | 0.02 | 0.02 | 3298.0 |
| dtfile | winner | ? | 12:13:03 | 12:13:03 | 0.02 | 0.02 | 3338.0 |
| dtfile | winner | ? | 12:16:00 | 12:16:00 | | 0.03 | 0.03 | 2514.6 |
| dtfile | winner | ? | 12:16:03 | 12:16:03 | 0.02 | 0.02 | 3212.0 |
| dtfile | winner | ? | 12:19:01 | 12:19:01 | 0.03 | | 2472.0 |
| acctcom | winner | pts/5 | | | | | | |
