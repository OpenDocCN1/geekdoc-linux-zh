scanning every file on a system, this command could take awhile to complete.

```
$ sudo find /var -xdev -type f -exec wc -c {} \; | sort -n
0 /var/cache/apt/archives/lock
...
2572437 /var/lib/dpkg/available-old
2573098 /var/lib/dpkg/available
38433001 /var/cache/apt/pkgcache.bin
39872802 49659904 /var/cache/apt-xapian-index/index.1/termlist.DB
62783488 /var/cache/apt-xapian-index/index.1/postlist.DB
$
```

# List Processes, Sorted by Memory Usage

```
$ ps aux | sort -nk 4
```

Use this command to find the processes that are consuming the most memory. The processes using the least amount of memory will scroll off the top of your screen and the ones consuming the most amount of memory will be just above your shell prompt.

In this example, mysqld is consuming 1.3% of the memory on this host.

```
$ ps aux | head -1
USER   PID  %CPU  %MEM    VSZ   RSS TTY      STAT   START   TIME COMMAND
$ ps aux | sort -nk 4 | tail -5
```