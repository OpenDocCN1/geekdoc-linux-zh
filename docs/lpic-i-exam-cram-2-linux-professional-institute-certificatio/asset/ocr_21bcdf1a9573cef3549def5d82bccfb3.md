This returns output similar to what's shown here:

```
Feb 23 21:00:01 localhost sshd(pam_unix)[29358]:
session closed for user root
Feb 23 21:00:04 localhost sshd(pam_unix)[29501]:
Session opened for user root by (uid=0)
Feb 23 21:00:13 localhost sshd(pam_unix)[29501]:
Session closed for user root
Feb 23 21:00:16 localhost sshd(pam_unix)[29549]:
Session opened for user root by (uid=0)
```

It's when you combine the two commands that truly interesting things become possible. For example, say you wanted to view lines 31-40 of a 50-line file. Remember that you can't display ranges with either of the commands, but by putting them together, you can display a range of lines from the file $0$linefile with the following command:

```
head -n 40 50linefile | tail
```

```
31 Both software and hardware watchdog drivers are available in the
32 \*standard
33 kernel. If you are using the software watchdog, you probably also want
34 to use "panic=60" as a boot argument as well.
35
36 The wdt card cannot be safely probed for. Instead you need to pass
37 wdt=ioaddr,irq as a boot parameter - eg "wdt=0x240,11".
38
39 The SA1100 watchdog module can be configured with the "sa1100_margin"
40 commandline argument which specifies timeout value in seconds.
```

![](bbox=[0.08, 0.58, 0.22, 0.64])

> Watch for the `head` and `tail` commands on the exam-particularly the `-l` option for following a log file's latest entries.

# ## Splitting Files

The `split` command is useful for taking a large number of records and splitting them into multiple individual files that contain a certain amount of data.

The `split` command's options include (the `#` character represents a number of prefix characters)

+   > -a #—Uses a suffix a specified number of characters long (the default is xaa).

+   > -b #—Output files will contain the specified number of bytes of data.

+   > -c #—Output files will contain the specified number of lines of bytes of data.

+   > -l #—Output files will contain the specified number of lines of data.