
## Shell response to CDSLs

| sh (/sbin/sh, /usr/bin/sh) | csh (/usr/bin/csh) | ksh (posix) (/usr/bin/ksh, /usr/bin/posix/sh) | dtksh (ksh93) (/usr/dt/bin/dtksh) | tcsh (/usr/local/bin/tcsh) | bash (/usr/local/bin/bash) | zsh (/usr/local/bin/zsh) |
|---|---|---|---|---|---|---|
| # cd /.local..<br># pwd<br>/cluster/members/member0 | # cd /.local..<br># pwd<br>/cluster/members/member0 | # cd /.local..<br># pwd<br>/.local.. | # cd /.local..<br># pwd<br>/.local.. | # cd /.local..<br># pwd<br>/cluster/members/member0 | # cd /.local..<br># pwd<br>/.local.. | # cd /.local..<br># pwd<br>/.local.. |

**Table 6-5: Shell Responses to Symbolic Links** illustrates each shell’s response when changing the current working directory using a CDSL as the directory. Three alternate shells from the Tru64 UNIX Open Source CD are also shown in the table.

Notice that the bash and zsh shells are like ksh whereas tcsh is similar to csh.

Alternatively, you can use the pwd command in the /usr/bin directory.

## 6.5 Expanded Process IDs

You might be wondering, “What do expanded process IDs have to do with CDSLs and the file system hierarchy?” Nothing really, but we thought you might be interested in this bit of information and chose to offer it here.

Process IDs have been expanded to a 32-bit integer beginning in Tru64 UNIX version 5.0 (although it appears that the maximum value is 2147483647 which is actually 31-bits). In a standalone environment, you will not see any appreciable difference; for instance PID 0 is still [kernel_idle] and PID 1 is still the init daemon. The PID structure in a TruCluster environment, however, is defined to provide a unique range of process IDs (524288 PIDs/member) and is defined as follows:

1. Process ID (19-bits)
2. Member ID (8-bits)
3. Sequence Number (4-bits) – currently unused.
4. Sign-bit (1-bit) – this is reserved for future use.

The PID structure is defined in /usr/include/sys/types.h. The initial PID for each member is shown in Table 6-6.

Let's take a closer look at the PID of the init daemon on a cluster to explore how the PID structure in a cluster affects the PID. On member1, the PID for init would be 524289.

```
# sysconfig -q generic memberid
generic:
memberid = 1
```

```
# ps -eo pid,command | grep "/sbin/init*" | grep -v grep
524289 /sbin/init -a
```

### PID Range by Member ID

memberid × 2^19

| Member ID | PID | Member ID | PID | Member ID | PID |
|---|---|---|---|---|---|
| 1 | 524288 | 22 | 11534336 | 43 | 22544384 |
| 2 | 1048576 | 23 | 12058624 | 44 | 23068672 |
| 3 | 1572864 | 24 | 12582912 | 45 | 23592960 |
| 4 | 2097152 | 25 | 13107200 | 46 | 24117248 |
| 5 | 2621440 | 26 | 13631488 | 47 | 24641536 |
| 6 | 3145728 | 27 | 14155776 | 48 | 25165824 |
| 7 | 3670016 | 28 | 14680064 | 49 | 25690112 |
| 8 | 4194304 | 29 | 15204352 | 50 | 26214400 |
| 9 | 4718592 | 30 | 15728640 | 51 | 26738688 |
| 10 | 5242880 | 31 | 16252928 | 52 | 27262976 |
| 11 | 5767168 | 32 | 16777216 | 53 | 27787264 |
| 12 | 6291456 | 33 | 17301504 | 54 | 28311552 |
| 13 | 6815744 | 34 | 17825792 | 55 | 28835840 |
| 14 | 7340032 | 35 | 18350080 | 56 | 29360128 |
| 15 | 7864320 | 36 | 18874368 | 57 | 29884416 |
| 16 | 8388608 | 37 | 19398656 | 58 | 30408704 |
| 17 | 8912896 | 38 | 19922944 | 59 | 30932992 |
| 18 | 9437184 | 39 | 20447232 | 60 | 31457280 |
| 19 | 9961472 | 40 | 20971520 | 61 | 31981568 |
| 20 | 10485760 | 41 | 21495808 | 62 | 32505856 |
| 21 | 11010048 | 42 | 22020096 | 63 | 33030144 |

**Table 6-6: PID Range by Member**

![](img/a0df85c2e542a8d6c913113908553aa4_165_0.png)

**Figure 6-6: PID Structure Illustrated**

If we convert the PID from decimal to binary, we can see how the PID is composed.

```
# perl -e 'printf ("%032b\n", 524289);'
00000000000001000000000000000001
```

Figure 6-6 shows the bit field breakout.

## 6.6 References

- Tru64 UNIX System Administration Guide – versions 5.1 and 5.1A.
- TruCluster Server Technical Overview – versions 5.1 and 5.1A.
- Reference pages (noted within the text).
