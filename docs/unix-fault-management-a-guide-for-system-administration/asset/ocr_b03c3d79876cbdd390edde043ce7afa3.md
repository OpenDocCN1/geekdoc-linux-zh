For monitoring real and virtual memory, vmstat shows page faults and paging activity, including reclaimed pages and swapping rates.

For the CPU, you can see more detailed information with vmstat than that provided by iostat. vmstat shows faults, including device interrupts, system calls, and context switches. vmstat also includes the breakdown of CPU utilization by user, system, and idle time.

For processes, vmstat shows the number of processes in various states, including the following: currently in the run queue, blocked on an I/O operation, and swapped out to disk.

The statistics that you see vary depending on the command option that you specify. By specifying a time interval, you can have vmstat run continuously, so that you can see how the values vary over time. As shown in Listing 4-12, using the -s option prints paging-related activity.

# who

The who command tells you who is logged in to the system, and how long each user has been connected. This command can be useful if a performance problem arises, because you can

# Listing 4-12   Output from the vmstat command showing paging activity.

```
$ vmstat -s
5431 swap ins
5431 swap outs
1376 pages swapped in
426 pages swapped out
9704169 total address trans. faults taken
2159795 page ins
9236 page outs
136606 pages paged in
21451 pages paged out
2064504 reclaims from free list
2097094 total page reclaims
773 intransit blocking page faults
6040874 zero fill pages created
3925703 zero fill page faults
1457303 executable fill pages created
76804 executable fill page faults
0 swap text pages found in free list
735656 inode text pages found in free list
185 revolutions of the clock hand
105428 pages scanned for page out
16850 pages freed by the clock daemon
50286274 cpu context switches
90662460 device interrupts
2732863 traps
229976779 system calls
```