mode. Then, look for the new user minidisk definition. Figure 4-5 shows the lines in that file and that refer to our newly created user.

```
USER  DISKMAP A1 F 80 Trunc=80 Size=382 Line=231 Col=1 Alt=0
00231
00232 VOLUME USERID CUU DEVTYPE START END SIZE
00233 LX6W02 $ALLOC$ A03 3390 00000 00000 00001
00234 40SASF40 2D2 3390 00001 00150 00150
00235 OSADMIN2 191 3390 00151 00160 00010
00236 OSADMIN3 191 3390 00161 00170 00010
<...snap...>
00318 COSTA 191 3390 01806 01815 00010
00319 HAIMO 191 3390 01816 01825 00010
00320 1826 1999 174 GAP
00321 GUILL 191 3390 02000 02009 00010
00322 OMAR 191 3390 02010 02019 00010
00323 RAY 191 3390 02020 02029 00010
00324 KEN 191 3390 02030 02039 00010
00325 CERON 191 3390 02040 02049 00010
====>
```

Figure 4-5 Checking DASD layout for gaps and overlaps

Notice in Figure 4-5 that line 00320 (in bold) shows a gap starting at cylinder 1826 and running through cylinder 1999, for a total of 174 cylinders. Although you should try to avoid gaps to prevent fragmentation, they are harmless. The second bold line (00325) shows the newly created user; no overlap exists between it and any of its surrounding minidisks definitions. Having checked that, we must run DIRECTXTA USER for the changes to take place.

# Formatting a minidisk

After a new user is created, its owner should format its assigned minidisk space so that files can be created for that disk. This is accomplished by running the FORMAT command after the user logs on:

```
format 191 a
```

This command formats the user's 191 disk and uses it as the A file mode. See Figure 4-6 on page 137

6 Gaps only leave empty disk space between minidisks, but an overlap occurs when one minidisk definition overlaps into following minidisks; z/VM actually allows this overlap.