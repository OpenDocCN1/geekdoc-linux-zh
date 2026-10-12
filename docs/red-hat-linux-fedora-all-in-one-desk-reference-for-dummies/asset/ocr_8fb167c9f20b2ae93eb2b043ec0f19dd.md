contents of all the directories in the /etc/rc.d directory (this directory contains system startup files):

```
du /etc/rc.d
288   /etc/rc.d/init.d
4     /etc/rc.d/rc0.d
4     /etc/rc.d/rc1.d
4     /etc/rc.d/rc2.d
4     /etc/rc.d/rc3.d
4     /etc/rc.d/rc4.d

4     /etc/rc.d/rc5.d
4     /etc/rc.d/rc6.d
352   /etc/rc.d
```

Each directory name is preceded by a number — which tells you the number of kilobytes of disk space used by that directory. Thus the /etc/rc.d directory, as a whole, uses 352K disk space whereas the /etc/rc.d/init.d subdirectory uses 288K. If you simply want the total disk space used by a directory (including all the files and subdirectories contained in that directory), use the -s option, as follows:

```
du -s /etc/rc.d
352   /etc/rc.d
```

The -s option causes du to print just the summary information for the /etc/rc.d directory.

![](bbox=[0.15, 0.73, 0.27, 0.86])

Just as df -h prints the disk-space information in megabytes and gigabytes, you can use the du -h command to view the output of du in more human-readable form. For example, here's how I combine it with the -s option to see the space I'm using in my home directory (/home/naba):

```
du -sh /home/naba
29M   /home/naba
```