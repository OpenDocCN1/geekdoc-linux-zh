```
bash(8391)
[root@host ~]# pkill -SIGKILL -P 8391
[root@host ~]# pgrep -l -u bob
bash(8391)
[root@host ~]#
```

# REFERENCES

**info libc** **signal** (GNU C Library Reference Manual)

+   - Section 24: Signal Handling

**info libc** **processes** (GNU C Library Reference Manual)

+   - Section 26: Processes

kill(1), killall(1), pgrep(1), pkill(1), pstree(1), signal(7), and w(1) man pages