# 1082

# ppgsz — Set Preferred Stack and/or Heap Page Size

# Synopsis

```
/usr/bin/ppgsz [-F] -o option,[option] cmd -p pid... 
```

# Use

Use the ppgsz command, new in the Solaris 9 Operating Environment, to set the preferred stack and/or heap page size for the target process(es), that is, the launched cmd or the process(es) in the pid list. ppgsz stops the process(es) while changing the page size. See memcntl(2).

Because of resource constraints, setting the preferred page size does not necessarily guarantee that the target process(es) gets the preferred page size. Use pmap(1) to view the actual heap and stack page sizes of the target(es). See pmap -s.

You must map large pages at addresses that are multiples of the size of the large page. Given that the heap is typically not large-page aligned, the starting portions of the heap (below the first page aligned address) are mapped to the system memory page size. See getpagesize(3).

# Options

+   -F Preferred page page size for target process(es) even if controlled by other process(es). Exercise caution when using the -p option. See proc(1).

+   -p Set the preferred page size option(s) for the target process(es) in the process-ID (pid) list following the -p option. The pid list can also consist of names in the /proc directory. Only the process owner or superuser is permitted to set page size.

cmd is interpreted if you do not specify -p. ppgsz launches cmd and applies page size option(s) to the new process.
The heap and stack preferred page sizes are inherited. Child process(es) created (fork(2)) from the launched process inherit the preferred heap and stack page sizes. The preferred page sizes are set back to the default system page size (see getpagesize(3)) on exec(1) (see exec(2)).

+   -o option,[option] You must specify at least one of the following options

+   heap=size Specify the preferred page size for the heap of the target process(es), heap is defined to be the bss (uninitialized data) and the brk area that immediately follows the bss (see brk(2)). The preferred heap page size is set for the existing heap and for any additional heap memory allocated in the future.