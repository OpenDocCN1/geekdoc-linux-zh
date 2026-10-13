
WU-FTPD includes a utility called `xferstats` that is useful for analyzing and summarizing the log information stored in the `xferlog` file. The output of xferstats includes the following information:

- Total and average daily bytes transferred
- Daily statistics
- Breakdown of files and bytes sent by each server directory
- Hourly traffic statistics

The `xferstats` program takes several arguments, including `-f filename` to indicate the full path and filename of the `xferlog` file; `-r` to include real users in the statistics; `-a` to include anonymous users in the statistics; `-h` to generate hourly traffic reports; `-d` to generate domain-specific traffic reports; and `-t` to generate total traffic reports by section.

The following is sample output from `xferstats`:

```text
# xferstats -f /var/log/xferlog -r -a -h -t
TOTALS FOR SUMMARY PERIOD Sun Nov 7 1999 To Sat Nov 13 1999
Files Transmitted During Summary Period                  107
Bytes Transmitted During Summary Period                8217300
Systems Using Archiving                                  43

Average Files Transmitted Daily                          15
Average Bytes Transmitted Daily                      1173900
```

### Daily Transmission Statistics

| Date | Number Of Files Sent | Number of Bytes Sent | Average Xmit Rate | Percent Of Files Sent | Percent Of Bytes Sent |
|---:|---:|---:|---:|---:|---:|
| Sun Nov 7 1999 | 29 | 2756399 | 2.2 KB/s | 27.10 | 33.54 |
| Mon Nov 8 1999 | 11 | 161878 | 3.2 KB/s | 10.28 | 1.97 |
| Tue Nov 9 1999 | 12 | 506230 | 2.9 KB/s | 11.21 | 6.16 |
| Wed Nov 10 1999 | 10 | 602695 | 0.9 KB/s | 9.35 | 7.33 |
| Thu Nov 11 1999 | 9 | 498994 | 1.2 KB/s | 8.41 | 6.07 |
| Fri Nov 12 1999 | 19 | 1904576 | 0.6 KB/s | 17.76 | 23.18 |
| Sat Nov 13 1999 | 17 | 1786625 | 1.7 KB/s | 15.89 | 21.74 |

### Total Transfers from each Archive Section (By bytes)

| Archive Section | Files Sent | Bytes Sent | Percent Of Files Sent | Percent Of Bytes Sent |
|---:|---:|---:|---:|---:|
| /bahai/authors/bahaullah | 38 | 3072276 | 35.51 | 37.39 |
| /bahai/authors/other | 14 | 2269853 | 13.08 | 27.62 |
| /bahai/authors/abdulbaha | 9 | 1463654 | 8.41 | 17.81 |
| /bahai/authors/shoghi_eff | 9 | 897391 | 8.41 | 10.92 |
| /bahai/authors/bab | 2 | 211318 | 1.87 | 2.57 |
| /bahai | 32 | 159146 | 29.91 | 1.94 |
| /bahai/compilations/bahai | 1 | 55624 | 0.93 | 0.68 |
| /bahai/compilations/peace | 1 | 51099 | 0.93 | 0.62 |
| /bahai/compilations/schol | 1 | 36939 | 0.93 | 0.45 |

### Hourly Transmission Statistics

| Time | Number Of Files Sent | Number of Bytes Sent | Average Xfer Rate | Percent Of Files Sent | Percent Of Bytes Sent |
|---:|---:|---:|---:|---:|---:|
| 00 | 4 | 344770 | 3.2 KB/s | 3.74 | 4.20 |
| 01 | 30 | 2607905 | 2.1 KB/s | 28.04 | 31.74 |
| 02 | 5 | 422711 | 3.7 KB/s | 4.67 | 5.14 |
| 03 | 2 | 37908 | 0.7 KB/s | 1.87 | 0.46 |
| 04 | 1 | 3127 | 3.1 KB/s | 0.93 | 0.04 |
| 05 | 1 | 1826 | 1.8 KB/s | 0.93 | 0.02 |
| 06 | 13 | 721616 | 0.8 KB/s | 12.15 | 8.78 |
| 07 | 6 | 1121640 | 0.9 KB/s | 5.61 | 13.65 |
| 09 | 4 | 40445 | 0.5 KB/s | 3.74 | 0.49 |
| 10 | 1 | 4992 | 2.5 KB/s | 0.93 | 0.06 |
| 12 | 1 | 1826 | 1.8 KB/s | 0.93 | 0.02 |
| 13 | 3 | 89864 | 0.7 KB/s | 2.80 | 1.09 |
| 15 | 8 | 1353325 | 1.9 KB/s | 7.48 | 16.47 |
| 16 | 1 | 92 | 0.1 KB/s | 0.93 | 0.00 |
| 17 | 2 | 28298 | 4.0 KB/s | 1.87 | 0.34 |
| 18 | 5 | 116513 | 2.9 KB/s | 4.67 | 1.42 |
| 19 | 4 | 153783 | 4.0 KB/s | 3.74 | 1.87 |
| 20 | 4 | 399828 | 4.3 KB/s | 3.74 | 4.87 |
| 21 | 4 | 203706 | 0.1 KB/s | 3.74 | 2.48 |
| 22 | 2 | 226956 | 2.1 KB/s | 1.87 | 2.76 |
| 23 | 6 | 332629 | 2.3 KB/s | 5.61 | 4.09 |

In addition to xferstats, there are several freely available third-party tools for summarizing the contents of xferlog files:

- `dumpxfer` processes xferlog files and gives more humanly readable output (available through anonymous ftp at `ftp://tnt.microimages.com/tools/`; requires Perl).
- Koos van den Hout has written a Perl script to process the xferlog file, mail daily statistics and upload files, and create a top-most downloaded files list (available at `ftp://ftp.cetis.nvu.nu/pub/koos/ftplogcheck`).
- `iisstat` generates nice transfer graphs from xferlog files and from many other sources (available from `ftp://ftp.support.lotus.com/pub/utils/InternetServices/iisstat/iisstat.html`).
- `Webalizer` is available from `ftp.mrunix.net/pub/webalizer`. It analyzes WU-FTPD format log files and creates reports in HTML pages that can be viewed with a Web browser.

## TROUBLESHOOTING

Two problems commonly occur when configuring a WU-FTPD server:

- **ls works for real users, but produces no output for anonymous users.** To resolve this problem, you need the dynamic libraries used by `ls` in the `lib` directory in the FTP user’s home directory (`/home/ftp/lib/` in the examples in this chapter). You can test if `ls` will work for FTP users with the following command:

  ```sh
  # chroot ~ftp /bin/ls
  ```

  If `ls` doesn’t work you can use the `ldd` command to determine which libraries are needed by the `ls` command and copy these files to `/home/ftp/lib/`:

  ```text
  # ldd /bin/ls
          libc.so.6 => /lib/libc.so.6 (0x40000000)
          /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
  ```

  The same principles hold true for other programs in the `/bin` directory such as `compress` and `gzip`. If FTP users cannot use them then check that the libraries needed are present using `ldd`.

- **ls works fine but the file and directory owner and group names are not shown; UID and GID numbers are displayed instead of names.** There are two possible causes of this problem. One is that the user and group names for the UIDs and GIDs have not been added to `/home/ftp/etc/passwd` and `/home/ftp/etc/group`. A second possible cause for the problem is related to missing dynamic libraries in `/home/ftp/lib/`. WU-FTPD needs the `libnsl.*` and `libnss_files.*` libraries on Linux in order to display this information.

Two common problems can occur when starting the ProFTPD server:

- After installing ProFTPD for the first time, when you try to start it up either from inetd or as standalone you might see the error “Group nogroup not found.” This is because the default `proftpd.conf` file calls for the user nobody and group nogroup to run the daemon. Commonly, Linux systems don’t have the group nogroup defined in `/etc/group`. To fix it you can either define the group nogroup in `/etc/group` or change the `proftpd.conf` file to use the group nobody instead.

- When starting ProFTPD in standalone mode you might see the error “Unable to bind to port/Address already in use.” This problem happens when a line for the FTP service exists in the `/etc/inetd.conf` file. To solve the problem, comment out the line starting with “ftp” in `/etc/inetd.conf` and send inetd a hang-up signal. Alternatively, make sure another copy of ProFTPD or another FTP daemon is not already running in standalone mode.

## APPENDIXES

- **A** Linux Command Reference
- **B** Linux Hardware Support

## Linux Command Reference

The following are reproductions of selected manual pages as shipped with Red Hat Linux 6.2. They are copyrighted by their respective authors or copyright holders and are freely redistributable, as is Linux.

### AT

#### NAME

`at`, `batch`, `atq`, and `atrm` queue, examine, or delete jobs for later execution.

#### SYNOPSIS

```text
at [-V] [-q queue] [-f file] [-mldbv] TIME
at -c job [job...]
atq [-V] [-q queue] [-v]
atrm [-V] job [job...]
batch [-V] [-q queue] [-f file] [-m] [-v] [TIME]
```

#### DESCRIPTION

`at` and `batch`, which are to be executed at a later time, read commands from standard input or from a specified file using `/bin/sh`.

- **at**—Executes commands at a specified time.
- **atq**—Lists the user’s pending jobs, unless the user is the super-user; in that case, everybody’s jobs are listed.
- **atrm**—Deletes jobs.
- **batch**—Executes commands when system load levels permit; in other words, when the load average drops below 0.8, or the value specified in the invocation of `atrun`.

`at` allows fairly complex time specifications, extending the POSIX.2 standard. It accepts times of the form HH:MM to run a job at a specific time of day. (If that time is already past, the next day is assumed.) You can also specify midnight, noon, or teatime (4 p.m.) and you can have a time-of-day suffixed with AM or PM for running in the morning or the evening. You can also say what day the job will be run by giving a date in the form month-name day with an optional
