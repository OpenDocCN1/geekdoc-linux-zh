```
0x0CFC24B70 964 Sleeping 0x0FEBEBEAC 0xC44FDBD0 (none) mwltd
0x0CFCB3B90 973 Sleeping 0x0F0F66C7C 0xC4CF7CD0 ttyS1 getty
0x0CFCB57F0 974 Sleeping 0x0CF4B485C 0xC4CF5E850 (none) in.telnetd
0x0CFCB470 979 Sleeping 0x0F0E6950 0xC4CF675D80 tty0 bash
0x0CFCBDB80 982: Running 0x0FEFEBOC 0xC4CF73870 tty0 sync
(gdb)
```

The bulk of the work done by this ps macro is performed by the task_struct_show macro. As shown in Listing 14-13, the task_struct_show macro displays the following fields from each task_struct:

+   • Address—Address of the task_struct for the process
+   • PID—Process ID
+   • State—Current state of the process
+   • User_NIP—Userspace Next Instruction Pointer
+   • Kernel_SP—Kernel Stack Pointer
+   • device—Device associated with this process
+   • comm—Name of the process (or command)

It is relatively easy to modify the macro to show the items of interest for your particular kernel debugging task. The only complexity is in the simplicity of the macro language. Because function equivalents such as str1en do not exist in gdb's user-defined command language, screen formatting must be done by hand.

Listing 14-14 reproduces the task_struct_show macro that produced the previous listing.

# ## Listing 14-14

```
gdb task_struct_show Macro

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
```