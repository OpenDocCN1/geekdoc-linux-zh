```
udev          189M   44K  189M   1% /dev
devshm        189M     0  189M   0% /dev/shm
/dev/sda3      20G   15G  5.9G  71% /home
```

The df command lets you know how much space is used by each file system, but after you know that, you still need to figure out what is consuming all of that disk space. The similarly named du command is invaluable for this purpose. This command with the right arguments can scan through a file system and report how much disk space is consumed by each directory. If you pipe it to a sort command, you can then easily see which directories consume the most disk space. What I like to do is save the results in /tmp (if there’s enough free space, that is) so I can refer to the output multiple times and not have to rerun du. I affectionately call this the “duck command”:

```
$ cd /
$ sudo du -ckx | sort -n > /tmp/duck-root
```

This command won’t output anything to the screen but instead creates a sorted list of what directories consume the most space and outputs the list to /tmp/duck-root. If I then use tail on that file, I can see the top ten directories that use space:

```
$ sudo tail /tmp/duck-root
67872  /lib/modules/2.6.24-19-server
67876  /lib/modules
69092  /var/cache/apt
69448  /var/cache
76924  /usr/share
82832  /lib
124164 /usr
404168 /
404168 total
```

In this case I can see that /usr takes up the most space, followed by /lib, /usr/share, and then /var/cache. Note that the output separates out /var/cache/apt and /var/cache so I can tell that /var/cache/apt is the subdirectory that consumes the most space under /var/cache. Of course, I might have to open the duck-root file with a tool like less or a text editor so I can see more than the last ten directories.

So what can you do with this output? In some cases the directory that takes up the most space can’t be touched (as with /usr), but often when the free