```
nice -n 12 dobigjob
```

Nice only works on jobs that have not started. To make an existing process nice, you use renice. If you want to give the Web server priority before all other processes, root can adjust it like this:

```
[root@digital httpd]# renice -10 188
188: old priority 0, new priority -10
```

# Monitoring Your Disk

One thing that Linux doesn’t like is running out of disk space. Monitoring your disk space is easy. There are two programs that you can use: du and df.

Previous | Table of Contents | Next