# Listing 14-10

Simple gdb Initialization File

```
$ cat - ./.gdbinit
set history save on
set history filename -/.gdb_history
set output-radix 16

define connect
# target remote bdi:2001
target remote /dev/ttyS0
b panic
b sys_sync
end
```

This simple `.gdbinit` file enables the storing of command history in a user-specified file and sets the default output radix for printing of values. Then it defines a **gdb user-defined command** called *connect*. (User-defined commands are also often called macros.) When issued at the **gdb** command prompt, **gdb** connects to the target system via the desired method and sets the system breakpoints to *panic*() and *sys_sync*(). One method is commented out; we discuss this method shortly in Section 14.4.

There is no end to the creative use of **gdb** user-defined commands. When debugging in the kernel, it is often useful to examine global data structures such as task lists and memory maps. Here we present several useful **gdb** user-defined commands capable of displaying specific kernel data that you might need to access during your kernel debugging.

# 14.3.4 Useful Kernel gdb Macros

During kernel debugging, it is often useful to view the processes that are running on the system, as well as some system attributes of those processes. The kernel maintains a linked list of tasks described by `struct task_struct`. The address of the first task in the list is contained in the kernel global variable `init_task`, which represents the initial task spawned by the kernel during startup. Each task contains a `struct list_head`, which links the tasks in a circular linked list. These two ubiquitous kernel structures are described in the following header files:

```
struct task_struct            .../include/linux/sched.h
struct list_head              .../include/linux/list.h
```