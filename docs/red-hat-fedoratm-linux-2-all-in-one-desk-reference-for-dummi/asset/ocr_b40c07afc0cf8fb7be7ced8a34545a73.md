If you compare this output with the output of plain `df` (see previous listing), you see that `df -h` prints the sizes with terms like **M** for megabytes and **G** for gigabytes. These are clearly easier to understand than 1K-blocks.

The other command — `du` — is useful for finding out how much space a directory takes up. For example, type the following command to view the contents of all the directories in the `/etc/rc.d` directory (this directory contains system startup files):

```
du /etc/rc.d
4            /etc/rc.d/rc1.d
4            /etc/rc.d/rc0.d
4            /etc/rc.d/rc5.d
4            /etc/rc.d/rc3.d
4            /etc/rc.d/rc4.d
4            /etc/rc.d/rc2.d
308          /etc/rc.d/init.d
4            /etc/rc.d/rc6.d
372          /etc/rc.d
```

Each directory name is preceded by a number — which tells you the number of kilobytes of disk space used by that directory. Thus the `/etc/rc.d` directory, as a whole, uses 372K disk space whereas the `/etc/rc.d/init.d` subdirectory uses 308K. If you simply want the total disk space used by a directory (including all the files and subdirectories contained in that directory), use the `-s` option, as follows:

```
du -s /etc/rc.d
372          /etc/rc.d
```

The `-s` option causes `du` to print just the summary information for the `/etc/rc.d` directory.

Just as `df -h` prints the disk-space information in megabytes and gigabytes, you can use the `du -h` command to view the output of `du` in more human-readable form. For example, here’s how I combine it with the `-s` option to see the space I’m using in my home directory (`/home/naba`):

![](bbox=[0.15, 0.67, 0.23, 0.76])

```
du -sh /home/naba
29M          /home/naba
```