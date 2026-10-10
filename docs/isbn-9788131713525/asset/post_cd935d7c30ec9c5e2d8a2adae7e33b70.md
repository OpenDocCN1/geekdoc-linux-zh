
Line 4 defines the macro name. Line 7 decides whether the input argument is a PID (numeric entry starting at zero and limited to a few million) or a `task_struct` address that must be greater than the end of the Linux kernel image itself, defined by the symbol `_end`.⁸ If it’s an address, the only action required is to cast it to the proper type to enable dereferencing the associated `task_struct`. This is done at line 8. As the comment in line 3 states, this macro returns a gdb convenience variable typecast to a pointer to a struct `task_struct`.

If the input argument is a numeric PID, the list is traversed to find the matching `task_struct`. Lines 12 and 13 initialize the loop variables (gdb does not have a for statement in its macro command language), and lines 15 through 17 define the search loop. The `find_next_task` macro is used to extract the pointer to the next `task_struct` in the linked list. Finally, if the search fails, a sane return value is set (the address of `init_task`) so that it can be safely used in other macros.

Building on the `find_task` macro in Listing 14-11, we can easily create a simple `ps` command that displays useful information about each process running on the system.

Listing 14-12 defines a gdb macro that displays interesting information from a running process, extracted from the struct `task_struct` for the given process. It is invoked like any other gdb command, by typing its name followed by any required input parameters. Notice that this user-defined command requires a single argument, either a PID or the address of a `task_struct`.

# Listing 14-12
gdb Macro: Print Process Information

```
1 define ps
2     # Print column headers
3     task_struct_header
4     set $t=$init_task
5     task_struct_show $t
6     find_next_task $t
7     # Walk the list
8     while $init_task!=$t
9         # Display useful info about each task
10        task_struct_show $t
11        find_next_task $t
12    end
13 end
15 document ps
16 Print points of interest for all tasks
17 end
```

⁸ The symbol `_end` is defined in the linker script file during the final link.

This `ps` macro is similar to the `find_task` macro, except that it requires no input arguments and it adds a macro (`task_struct_show`) to display the useful information from each `task_struct`. Line 3 prints a banner line with column headings. Lines 4 through 6 set up the loop and display the first task. Lines 8 through 11 loop through each task, calling the `task_struct_show` macro for each.

Notice also the inclusion of the gdb `document` command. This allows the gdb user to get help by issuing the `help ps` command from the gdb command prompt as follows:

```
(gdb) help ps
   Print points of interest for all tasks
```

Listing 14-13 displays the output of this macro on a target board running only minimal services.

# Listing 14-13
gdb ps Macro Output

```
(gdb) ps
Address    PID State    User_NIP    Kernel-SP device comm
0xc01D3750    0 Running    0x0FF6B85C 0xcC205B90 (none) swapper
0xc04ACB10    1 Sleeping   0x0FF6B85C 0xcC4FFCE0 (none) init
0xc04AC770    2 Sleeping   0xcC501E90 (none) ksoftirqd/0
0xc04AC3D0    3 Sleeping   0xcC0531E30 (none) events/0
0xc04AC030    4 Sleeping   0xcC0533E30 (none) khelper
0xc04ACBB0    5 Sleeping   0xcC0533E30 (none) kthread
0xc04CD790   23 Sleeping   0xcC05FD830 (none) kbiclockd/0
0xc04CD3F0   45 Sleeping   0xcC60EB50 (none) pdflush
0xc04CD050   46 Sleeping   0xcC06FF850 (none) kfifup
0xc045B7B0   48 Sleeping   0xcC0732E30 (none) aio/0
0xc045B850   47 Sleeping   0xcC0701E20 (none) kswapd0
0xc045B410   629 Sleeping  0xcC0781E60 (none) kswapd0
0xc0504B70   663 Sleeping  0xcCFC993E30 (none) rpidl0/0
0xc0FFD00D   675 Sleeping  0x0FF6EB85C 0xcCFC8DCE0 (none) udevd
0xcF955B1D   879 Sleeping  0x0FF0B85C 0xcCFC517DB0 (none) portmap
0xcFC24090   910 Sleeping  0x0FF0B85C 0xcCFC61BCE0 (none) syslogd
0xcFB4490   918 Sleeping  0x0FF6B9C 0xcCF65D070 (none) klogd
0xcFEB30B0   948 Sleeping  0x0FF0B85C 0xcCFC8E0 (none) rpc.statd
0xcFCFDE810   960 Sleeping  0x0FF6E85C 0xcCFC5C7CE0 (none) inetd
0x0CFC24B70 964 Sleeping 0x0FEBEBEAC 0xC44FDBD0 (none) mwltd
0x0CFCB3B90 973 Sleeping 0x0F0F66C7C 0xC4CF7CD0 ttyS1 getty
0x0CFCB57F0 974 Sleeping 0x0CF4B485C 0xC4CF5E850 (none) in.telnetd
0x0CFCB470 979 Sleeping 0x0F0E6950 0xC4CF675D80 tty0 bash
0x0CFCBDB80 982: Running 0x0FEFEBOC 0xC4CF73870 tty0 sync
(gdb)
```

The bulk of the work done by this ps macro is performed by the task_struct_show macro. As shown in Listing 14-13, the task_struct_show macro displays the following fields from each task_struct:

- Address—Address of the task_struct for the process
- PID—Process ID
- State—Current state of the process
- User_NIP—Userspace Next Instruction Pointer
- Kernel_SP—Kernel Stack Pointer
- device—Device associated with this process
- comm—Name of the process (or command)

It is relatively easy to modify the macro to show the items of interest for your particular kernel debugging task. The only complexity is in the simplicity of the macro language. Because function equivalents such as str1en do not exist in gdb's user-defined command language, screen formatting must be done by hand.

Listing 14-14 reproduces the task_struct_show macro that produced the previous listing.

# Listing 14-14
gdb task_struct_show Macro

```
1  define task_struct_show
2     # task_struct addr and PID
3     printf "0x%08X %5d", $arg0, $arg0->pid
4
5     # Place a `<` marker on the current task
6     if ($arg0 == `current`)
7     # For PowerPC, register r2 points to the `current` task
8     if ($arg0 == $r2)
9       printf "<"
10     else
11       printf " 
12end

13

14# State

15if ($arg0->state == 0)

16  printf "Running "

17else

18  if ($arg0->state == 1)

19    printf "Sleeping "

20  else

21    if ($arg0->state == 2)

22      printf "DiskSleep "

23    else

24      if ($arg0->state == 4)

25        printf "Zombie "

26      else

27        if ($arg0->state == 8)

28          printf "Stopped "

29        else

30          if ($arg0->state == 16)

31            printf "WPaging "

32          else

33            printf "%2d       ", $arg0->state

34          end

35        end

36      end

37    end

38  end

39

40

41# User NIP

42if ($arg0->thread_regs)

43  printf "0x%08X ", $arg0->thread_regs->nip

44else

45  printf "*"

46end

47

48# Display the kernel stack pointer

49printf "0x%08X ", $arg0->thread.ksp

50

51# device

52if ($arg0->signal->tty)

53  printf "%s  ", $arg0->signal->tty->name

54else

55  printf "(none)"

56end

57

58# comm

59printf "%s\n", $arg0->comm

60end
```

Line 3 displays the address of the `task_struct`. Lines 8 through 12 display the process ID. If this is the current process (the process that was currently running on this CPU at the time the breakpoint was hit), it is marked with a < character.

Lines 14 through 39 decode and display the state of the process. This is followed by displaying the user process next instruction pointer (NIP) and the kernel stack pointer (SP). Finally, the device associated with the process is displayed, followed by the name of the process (stored in the ->comm element of the `task_struct`).

It is important to note that this macro is architecture dependent, as shown in lines 7 and 8. In general, macros such as these are highly architecture- and version- dependent. Any time a change in the underlying structure is made, macros such as these must be updated. However, if you spend a lot of time debugging the kernel using `gdb`, the payback is often worth the effort.

For completeness, we present the `find_next_task` macro. Its implementation is less than obvious and deserves explanation. (It is assumed that you can easily deduce the `task_struct_header` that completes the series necessary for the `ps` macro presented in this section. It is nothing more than a single line arranging the column headers with the correct amount of whitespace.) Listing 14–15 presents the `find_next_task` macro used in our `ps` and `find_task` macros.

# Listing 14-15
gdb find_next_task Macro

```
define find_next_task
# Given a task address, find the next task in the linked list
set $t = (struct task_struct *)$arg0
set $offset=( (char *)&$t->tasks - (char *)$t)
set $t=(struct task_struct *) ( (char *)$t->tasks.next- (char *)$offset)
end
```

The function performed by this macro is simple. The implementation is slightly less than straightforward. The goal is to return the ->next pointer, which points to the next task_struct on the linked list. However, the task_struct structures are linked by the address of the struct list_head member called tasks, as opposed to the common practice of being linked by the starting address of the task_struct itself. Because the ->next pointer points to the address of the task structure element in the next task_struct on the list, we must subtract to get the address of the top of the task_struct itself. The value we subtract from the ->next pointer
