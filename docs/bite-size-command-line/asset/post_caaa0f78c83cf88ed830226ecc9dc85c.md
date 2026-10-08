
# ps

# 14

ps
ps shows which processes are running
I usually run ps like this:

wchan is for wide. ps auxwww
will show all the command line args for each process,

you can choose which columns to show with ps (ps -eo ...)
One cool column is 'wchan' which tells you the name of the kernel function if the process is sleeping
try it:

```
$ ps aux
a+ttx
u means include together
username column show all process
ps -ef works too)
```

e is for environment. ps auxe
will show the environment vars:

```
$ ps -eo user,pid,wchan,cmd
```

# ★ process state ★

f is for "forest" ツ. ps auxf
Will show you an ASCII art process tree:

ps has 3 different sets of command line arguments 💔

Here's what the letters in 's STATE column mean:

+   1. UNIX (1 dash)
2. BSD (no dash)
3. GNU (2 dashes)

+   R: running
S/D: asleep
Z: zombie
I: multithreaded
t+: in the foreground

you can write monotrites like:
$ ps f -f
full format (UNIX)

pstree can display a process tree too

# top

15

# top

a live-updating summary of the top users of your system's resources

> who's using all memory
> chrome obv

let's explain some numbers in top!

# load average

3 numbers that roughly reflect demand for your CPUs on the system in the last 1, 5, and 15 minutes

if it's higher than the * of CPUs you have, that's often bad

# memory

4 numbers:

total / free / used / cached

One perhaps unexpected thing: total is not free + used!

total = free + used + cached filesystem cache

# % CPU

![](img/5f5d02ddabdd2009c88fde2963d57414_14_0.png)

this column is given as of % of a single core. If you have 4 cores, this can go up to 400 %!

# RES

this column is the "resident set size" aka how much RAM your process is using.

SHR is how much of the RES is shared with other processes

# htop

a prettier & more interactive version of top ★

```
1 [## ] 10% 
2 [#### ] 20% 
3 [### ] 5% 
4 [##### ] used cached 5% 
mem [####################] 4176
swp [##] 2/256
```

# sort & uniq

sort sorts its input
$n sort names.txt
the default sort is alphabetical.

sort -n numeric sort

| 'sort -order' | 'sort -n' order |
| 12 | 12 |
| 15000 | 48 |
| 48 | 96 |
| 6020 | 6020 |
| 96 | 15000 |

sort -h: human sort

| 'sort -n' order | 'sort -h' order |
| 15 | 6 |
| 30 M | 30 M |
| 45 K | 15 G |
| 200 G | 200 G |

useful example:
du-sh * sort -h

+   uniq removes duplicates
a notice there b are still 2 b=> 'a's! 
uniq only unifies c adjacent matching lines

sort + uniq = =
Pipe something to 'sort | uniq' and you'll get a deduplicated list of lines! 
sort -u does the same thing.

+   - a sort -u = =
b b
- or sort uniq

uniq -c
counts each line it saw.
Recipe: get the top 10 most common lines in a file:
$ foo.txt
uniq -c
sort -n
tail -n 10

![](img/5f5d02ddabdd2009c88fde2963d57414_15_0.png)

# misc commands ❤

| rlwrap |
adds history & ctrl support to REPLs that don't already have them (rlwrap stands for readline)
$ rlwrap python | |

| watch |
rerun a command every 2 seconds |

| pv |
"pipe viewer", gives you stats on data going through a pipe |

| file |
figures out what kind of file (png? pdf?) a file is |

| cal |
a tiny calendar ♡ |

| ts |
add a timestamp in front of every input line |

| ncdu |
figure out what's using all your disk space |

| diff |
diff 2 files. Run with '-U 8' for context. |

| comm |
find lines 2 sorted files have in common |

| column |
format input into columns |

| xsel/ xclip |
copy/paste from system clipboard. (pbcopy /pbpaste on Mac) |

# head & tail

# head

shows you the first+ 10 lines of a file

if you pipe a program's output to head, the program will stop after printing 10 lines (it gets sent SIGPIPE)

# tail

tail shows the last 10 lines!

```
tail -f FILE
```
will follow:

print any new lines added to t end of FILE. Super useful for log files!

# -n NUM

-n NUM (either head or tail)
will change the #n lines shown

head -n -NUM show all
tail -n +NUM but the last / first NUM lines

# -c NUM

show the first /last NUM bytes of the file

head -c k
will show the first 1024 bytes

# tail --retry

keep trying to open file if it's inaccessible

# tail --pid PID

stop when process PID stops running (with -f)

# tail --follow=name

Usually tail -f will follow a file descriptor.

tail --follow=name FILENAME
will keep following the same name, eg if the file descriptor is rotated.

# less

19

less is a pager
that means it lets you\view (not edit) text files or piped in text man uses your pager (usually less) to display man pages

+   many vim shortcuts work in less
/ search
n/N next / prev match
j/k down /up a line
m/' mark/return to line
g/G beginning/end of file (gg in vim)

less -r
displays bash escape codes as colours
try ls --color less -r
with -r without -r
a.txt
a.txt.gzed,bold
ESCCOM ESC
COL;31ma.txt.gz
ESCCOM

# q quit

# F

# +

V< lowercase
edit file in your $EDITOR

press F to keep reading from the file as it's updated (like tail -f)
press Ctrl+C to stop reading updates

+ runs a command when less starts
less +F : follow updates
less +G : start at end of file
less +20% : start 20% into file
less +foo : search for 'foo' right away

arrow keys, Home/End,
PgUp, Pg Dn work in less

# # Kill

20

kill doesn't just kill programs

Which signal kill sends

# kill -l lists all signals

![](img/5f5d02ddabdd2009c88fde2963d57414_19_0.png)

| name | num |
|---|---|
| kill | SIGTERM 15 |
| kill -9 | SIGKILL 9 |
| kill -KILL | | |
| kill -HUP | SIGHUP 1 |
| kill -STOP | SIGSTOP 19 |

+   1 HUP 2 INT 3 QUIT 4 ILL
5 TRAP 6 ABRT 7 BUS 8 FPE
9 KILL 10 USR 11 SEGV 12 USR
13 PIPE 14 ALRM 15 TERM 16 SIGFLT
17 CHILD 18 CONT 19 STOP 20 TTSP
21 TINT 22 TTO

| name | num

| kill | SIGTERM 15 |
| kill -9 | SIGKILL 9 |
| kill -KILL | | |
| kill -HUP | SIGHUP 1 |
| kill -STOP | SIGSTOP 19 |

1 HUP 2 INT 3 QUIT 4 ILL
5 TRAP 6 ABRT 7 BUS 8 FPE
9 KILL 10 USR 11 SEGV 12 USR
13 PIPE 14 ALRM 15 TERM 16 SIGFLT
17 CHILD 18 CONT 19 STOP 20 TTSP
21 TINT 22 TTO

# kill -l lists all signals

![](img/5f5d02ddabdd2009c88fde2963d57414_19_0.png)

# -p

list the files PID has open.

# -i

list open network sockets (sockets are files!)

+   examples:
- i -n -p -n "do not resolve"
- i: 8080 host names /ports/ (also -Pni)
- i: TCP
-i -s TCP:LISTEN

# find deleted files

```
$lsof | grep deleted
```

Will show you deleted files!
You can recover open deleted files from

```
/proc/<pid>/fd/<fd>
process that opened the file
```

# netstat

another way to list open sockets on Linux is:

+   netstat -tunapl
tuna, please!

On Mac netstat has different args.

