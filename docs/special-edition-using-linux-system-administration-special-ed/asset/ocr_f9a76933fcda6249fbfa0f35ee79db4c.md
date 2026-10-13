WU-FTPD includes a utility called `xferstats` that is useful for analyzing and summarizing the log information stored in the `xferlog` file. The output of xferstats includes the following information:

+   - Total and average daily bytes transferred
+   - Daily statistics
+   - Breakdown of files and bytes sent by each server directory
+   - Hourly traffic statistics

The `xferstats` program takes several arguments, including `-f filename` to indicate the full path and filename of the `xferlog` file; `-r` to include real users in the statistics; `-a` to include anonymous users in the statistics; `-h` to generate hourly traffic reports; `-d` to generate domain-specific traffic reports; and `-t` to generate total traffic reports by section.

The following is sample output from `xferstats`:

```
# xferstats -f /var/log/xferlog -r -a -h -t
TOTALS FOR SUMMARY PERIOD Sun Nov 7 1999 To Sat Nov 13 1999
Files Transmitted During Summary Period                  107
Bytes Transmitted During Summary Period                8217300
Systems Using Archiving                                  43

Average Files Transmitted Daily                          15
Average Bytes Transmitted Daily                      1173900

Daily Transmission Statistics

                         Number Of    Number of    Average    Percent Of  Percent Of
          Date           Files Sent    Bytes Sent   Xmit       Rate       Files Sent  Bytes Sent
                         ----------    ----------   ------     --------   -----------  -----------
Sun Nov  7 1999               29       2756399    2.2 KB/s       27.10       33.54
Mon Nov  8 1999               11       1618781    3.2 KB/s       10.28        1.97
Tue Nov  9 1999               12        506230    2.9 KB/s       11.21        6.16
Wed Nov 10 1999               10        602695    0.9 KB/s        9.35        7.33
Thu Nov 11 1999                9        498994    1.2 KB/s        8.41        6.07
Fri Nov 12 1999               19       1904576    0.6 KB/s       17.76       23.18
Sat Nov 13 1999               17       1786625    1.7 KB/s       15.89       21.74

Total Transfers from each Archive Section (By bytes)

                                                       ---- Percent Of ----
             Archive Section       Files Sent Bytes Sent   Files Sent  Bytes Sent

/bahai/authors/bahaullah                  38      3072276       35.51       37.39
/bahai/authors/other                      14      2269853       13.08       27.62
/bahai/authors/abdulbaha                  9      1463654        8.41       17.81
/bahai/authors/shoghi_eff                 9       897391        8.41       10.92
/bahai/authors/bab                       2       211318        1.87        2.57
/bahai                                    32       159146       29.91        1.94
/bahai/compilations/bahai                 1        55624        0.93        0.68
```