5. View current disk space used by your users by entering `repquota -av` at the shell prompt. A report is displayed on the screen showing how much space each user is consuming, as shown here:

```
ws1:/ # repquota -av
*** Report for user quotas on device /dev/sda3
Block grace time: 7days; Inode grace time: 7days
User used soft hard grace used soft hard grace
games -- 416 0 0 3 0 0
sdm -- 12 0 0 32 0 0
lp -- 12 0 0 3 0 0
man -- 208 0 0 2 0 0
news -- 4 0 0 1 0 0
polkituser -- 24 0 0 2 0 0
root -- 4236032 0 0 154678 0 0
uucp -- 4 0 0 1 0 0
ksanders -- 680 0 0 505 0 0
tux -- 108844 0 0 742 0 0
jsanders -- 52 0 0 14 0 0
tracy -- 52 0 0 14 0 0
\#10000 -- 2688 0 0 211 0 0
Statistics:
Total blocks: 8
Data blocks: 1
Entries: 13
Used average: 13.000000
```

Notice in this report that no limits have been configured for any users.

6. Create disk quotas for your users by doing the following:

+   a. At the shell prompt, enter `edquota -u username`. A screen similar to that shown next for the tracy user is displayed:

```
Disk quotas for user tracy (uid 1004):
Filesystem blocks soft hard inodes soft hard
/dev/sda3 52 0 0 14 0 0
```

In this example, quotas are being set for tracy. Notice that the quota file has been opened in the vi editor. Also notice that you can set hard and soft quotas for blocks and for inodes. Soft quotas are those that can be temporarily exceeded. Hard quotas cannot be exceeded. Block quotas specify how many blocks on disk the user can consume. Inode quotas specify how many files the user can own.

+   b. Use the vi editor to set block and/or inode soft and hard quotas.
+   c. Save your changes and exit the editor.
+   d. Repeat this process for each of your users.

![](bbox=[0.06, 0.92, 0.83, 0.98])