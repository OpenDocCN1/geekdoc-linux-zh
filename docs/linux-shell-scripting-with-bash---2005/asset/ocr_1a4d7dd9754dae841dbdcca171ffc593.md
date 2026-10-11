Access: (0664/-rw-rw-r--)  Uid: ( 503/ kburcth) Gid: ( 503/ kburcth)
Device: 303  Inode: 131093  Links: 1
Access: Tue Feb 20 16:34:11 2001
Modify: Tue Feb 20 16:34:08 2001
Change: Tue Feb 20 16:34:08 2001

To make the information more readable from a script, use the *-t* (*terse*) switch. Each stat item is separated by a space.

```
$ stat -t orders.txt
orders.txt 21704 80 81fd 503 503 303 114674 1 6f 89 989439402
981490652 989436657
```

The Linux statftime command has similar capabilities to *stat*, but has a wider range of formatting options. statftimе is similar to the *date* command: It has a string argument describing how the status information should be displayed. The argument is specified with the *-f* (*format*) switch.

The most common statftime format codes are as follows:

+   * %c—Standard format
+   * %d—Day (zero filled)
+   * %D—mm/dd/yy
+   * %H—Hour (24-hr clock)
+   * %I—Hour (12-hr clock)
+   * %j—Day (1..366)
+   * %m—Month
+   * %M—Minute
+   * %S—Second
+   * %U—Week number (Sunday)
+   * %w—Weekday (Sunday)
+   * %Y—Year
+   * %%—Percent character
+   * %_A—Uses file last access time
+   * %_a—Filename (no suffix)
+   * %_C—Uses file inode change time
+   * %_d—Device ID
+   * %_e—Seconds elapsed since epoch
+   * %_f—File system type
+   * %_i—Inode number
+   * %_L—Uses current (local) time