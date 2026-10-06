# Part IV Alternative Linux Shells

### TABLE 20-6
### The ulimit Command Line Parameters
| Parameter | Description |
| -a | The currently active limits |
| -c | The largest core dump size (in KB) |
| -d | The largest data segment size of a process (in KB) |
| -f | The largest file block size (in 512-byte blocks) |
| -l | The largest amount of memory that can be locked (in KB) |
| -m | The largest amount of physical memory (in KB) that can be used |
| -n | The number of files the process can have open at one time |
| -p | The number of processes the user can have active at the same time |
| -s | The largest stack size of a process |
| -t | The CPU time limit |
| -H | Display or set a hard limit |
| -S | Display or set a soft limit |

To display all of the currently set limits, use the -a parameter.

```
$ ulimit -a
time(seconds) unlimited
file(blocks) unlimited
data(kbytes) unlimited
stack(kbytes) 8192
coredump(blocks) 0
memory(kbytes) unlimited
locked(memory(kbytes)) unlimited
process
nofiles 1024
vmemory(kbytes) unlimited
locks unlimited
```

To set a limit, just add the number for the limit amount along with the appropriate parameter.

```
$ ulimit -f 2
$
```

548