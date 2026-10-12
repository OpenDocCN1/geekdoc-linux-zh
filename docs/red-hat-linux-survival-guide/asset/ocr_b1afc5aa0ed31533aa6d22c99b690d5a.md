The df command summarizes the free disk space for the drives mounted on the system. Hard drive space is an important resource in a computer, and you should monitor it carefully. Mismanagement of hard drive space can cause a computer to crawl on its knees and result in some unhappy users.

```
df
```

```
Filesystem  512-blocks  Free %Used  Iused %Iused Mounted on
/dev/hd4    49152      25872   48%    2257   19%  /
/dev/hd2    1351680    243936  82%    19091  12%  /usr
/dev/hd9var 49152      12224   76%    2917   48%  /var
/dev/hd3    57344      52272   9%     125    2%   /tmp
/dev/lv00   57344      55176   4%     19     1%   /tftpboot
/dev/hd1    163840     16976   90%    1140   6%   /home
/dev/fs01   8192000    6381920 23%    20963  3%   /home/fs01
/dev/fs02   8192000    1873432 78%    72     1%   /home/fs02
```

To view the disk space summary for the current file system:

```
df .
```

```
Filesystem  512-blocks  Free %Used  Iused %Iused Mounted on
/dev/fs01   8192000    6381920 23%    20963  3%   /home/fs01
```

Notice that the df output is printed in 512-byte blocks. It may seem odd to think of blocks with this size if you are used to 1K blocks, or, more precisely, 1,024-byte blocks. The -k option displays the summary with 1,024-byte blocks instead:

```
df -k .
```

```
Filesystem  1024-blocks  Free %Used  Iused %Iused Mounted on
/dev/fs01   4096000    3190960 23%    20963  3%   /home/fs01
```

With the -k option in mind, the results are very different. If you interpret the output incorrectly, you may run out of disk space sooner than you think.

# edquota

See the section on assigning disk quotas to users in Chapter 7 for details.