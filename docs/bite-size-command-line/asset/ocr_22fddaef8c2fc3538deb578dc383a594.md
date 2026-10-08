# lsof

# lsof

stands for list open files

somebody has that file open WHO IS IT??
I can tell you!

lsof

# what lsof tells you

for each open file:

+   - pid
- file type (regular? directory? FIFO? socket?)
- file descriptor (FD column)
- user
- filename /socket address

# -p PID

list the files PID has open

# lsof /some /dir

list just the open files in lsome /dir

# -i

list open network sockets (sockets are files!)

+   examples:
-i -n -p -n & -p "do not resolve"
-i: 8080 host names /ports/ (also -Pni)
-i: TCP
-i -s TCP:LISTEN

# find deleted files

```
$lsof | grep deleted
```

Will show you deleted files!
You can recover open deleted files from

```
/proc/<pid>/fd/<fd> +
process that opened the file
```

# netstat

another way to list open sockets on Linux is:

+   netstat -tunapl
tuna, please!

On Mac netstat has different args.