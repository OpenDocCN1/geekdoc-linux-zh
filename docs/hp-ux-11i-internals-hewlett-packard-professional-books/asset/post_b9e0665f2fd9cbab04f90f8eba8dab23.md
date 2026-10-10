
you want to examine, how many of them to load, and how to find them. The simplest form of the `load` command is `load <type> from <address>`. The type can be any publicly visible kernel structure or typedef. If you're using a structure, you must include the `struct` keyword. The address can either be a numeric value or a symbol. For example, to load the first `mpinfo` struct from the `mproc_info` array, we would type

```
q4> load struct mpinfo from mproc_info
```

Because `struct mpinfo` is also typedefed to `mpinfo_t`, we could also say

```
q4> load mpinfo_t from mproc_info
```

## Displaying the Contents of a Pile

Once you've got a pile with a structure in it, you need to be able to look at the data. To print that pile, we use the `print` command. The `print` command with no arguments prints out the entire structure. If you're going to print a lot of elements, you probably want to add the `-t` flag to the `print` command. This option tells the command to print one element per line with the names on the left rather than print the data in columns with the names across the top. The `mpinfo` structure is very large—it has over 2,000 elements in it—so even with the `-t` option, you'll get over 2,000 lines of output. Fortunately, you don't have to see it all.

You can pipe `q4` commands through shell commands. So, after you've got your `mpinfo` pile loaded, you might want to do `print -t | more` to see it a page at a time. You could find out how many items there are in an `mpinfo` structure by doing `print -t | wc -l`. You can also tell `q4` exactly which items to print. If you type `print -t procindex prochnpa`, you'll get something like the following:

```
procindex       0
prochnpa        0xfffffffffed21000
```

## Using Skip to Load Structures

So far, we've loaded up the first `mpinfo` structure into a pile. But `mpinfo` is an array—what if you want to look at the `mpinfo` structures for other processors? The `skip` keyword tells `q4` how many array elements to skip over. If you want to look at the second entry (the entry for processor 1), for example, type

```
q4> load struct mpinfo from mproc_info skip 1
```

Now, if we look at `procindex` and `prochnpa`, we get

```
procindex       0x1
prochnpa        0xfffffffffed61000
```

## Loading Multiple Structures

Now we know how to load up a structure and examine its contents. But a pile can be more than one structure—you can load up a whole array of structures. We do this with the `max` keyword to the `load` command, which tells q4 the maximum number of structures to load; the default is one. Continuing with our `mpinfo` example, we can load the `mpinfo` structures for all of the processors by taking advantage of the global symbol `n_mpinfo`, which tells us how many there are:

```
q4> load struct mpinfo from mproc_info max n_mpinfo
loaded 2 struct mpinfo as an array (stopped by max count)
```

q4 tells us how many were loaded and what made it stop.

## Loading Linked Lists

The linked list is such a common structure in the kernel that q4 has knowledge of linked lists built in. To load a list of structures into a pile, you have to tell q4 which element in the structure points to the next structure in the list. You do this with the `next` keyword.

For an example, let’s look at the process table. Prior to HP-UX release 11.11, the process table was a statically allocated table of entries. Beginning with HP-UX 11.11, the process table is a linked list. The head of the list is pointed to by the symbol `proc_list`, and each entry in the list has a member called `p_factp`, which points to the next entry. To load up all of the current process table entries, we type

```
q4> load struct proc from proc_list next p_factp max 10000
loaded 155 struct proc as a linked list (stopped by null pointer)
```

q4 again tells us how many structures were loaded and why it stopped—in this case because it encountered a null pointer. q4 detects the end of a linked list either when it finds a null pointer or when it finds a pointer that points back to the first entry in the list.

Notice the large value for max. In this case, we wanted all of the `proc` structures, so we picked a `max` value large enough that it wouldn’t be exceeded. Without specifying `max` at all, we would get only one structure loaded.

## Using Values from a Pile

In addition to using global symbols, we can also specify the name of a member in the current pile as an address. Since there are so many cases where one data structure points to another, it makes sense to be able to use the member names rather than having to type in addresses. For example, in the `proc` structure there is a member named `p_firstthread` that points to the first thread in that process. Once you’ve got a `proc` structure on the pile, you can load the first thread for that process by typing

```
q4> load struct kthread from p_firstthread
```

## Manipulating Piles

Each time you execute a `load` command, a new pile is created. Previous piles are pushed onto a stack, so that at any time you will have access to all piles you've created. The `history` command lists the piles in the stack. For example,

```
q4> history
HIST NAME    LAYOUT  COUNT  TYPE      COMMENTS
  1 <none>    array   1      struct    mpinfo  stopped by max count
  2 <none>    array   2      struct    mpinfo  stopped by max count
  3 <none>    array   2      struct    mpinfo  stopped by max count
  4 <none>    list   155     struct    proc    stopped by null pointer
```

The highest numbered pile is the current pile. You can recall a previous pile with the `recall` command. The argument to the `recall` command is a pile number from the `HIST` column in the history display. A copy of the specified pile is pushed onto the stack and becomes the new current pile. Given the history in the previous example, we can recall the first `mpinfo` pile:

```
q4> recall 1
copied 1 item
q4> history
HIST NAME    LAYOUT  COUNT  TYPE      COMMENTS
  1 <none>    array   1      struct    mpinfo  stopped by max count
  2 <none>    array   2      struct    mpinfo  stopped by max count
  3 <none>    array   2      struct    mpinfo  stopped by max count
  4 <none>    list   155     struct    proc    stopped by null pointer
  5 <none>    array   1      struct    mpinfo  copy of 1
```

A pile can also be given a descriptive name that will be displayed in the history. The name is applied to the current pile with the `name` command. The syntax is just `name it <name>`. Continuing the above example, if we want to assign the name `proc1` to the pile we just recalled, we type

```
q4> name it proc1
so named
q4> history
HIST NAME    LAYOUT  COUNT  TYPE      COMMENTS
  1 <none>    array   1      struct    mpinfo  stopped by max count
  2 <none>    array   2      struct    mpinfo  stopped by max count
  3 <none>    array   2      struct    mpinfo  stopped by max count
  4 <none>    list   155     struct    proc    stopped by null pointer
  5 proc1     array   1      struct    mpinfo  copy of 1
```

Now we can use proc1 instead of the pile number if we want to recall the pile. This can be really handy if you have a lot of piles that are all the same data type—it can be hard to tell them apart.

Another handy pair of commands is keep and discard. For both of these commands, the argument is an expression. A new pile is created that contains either only those structures for which the expression is true (keep) or only for those for which the expression is false (discard). As an example, let's say we want to look at the process table entry for PID 1. We can recall the list of all processes we have in our stack, then keep just the one with p_pid equal to one:

```
q4> recall 4
copied 155 items
q4> keep p_pid == 1
kept 1 of 155 struct proc's, discarded 154
q4> history
HIST NAME   LAYOUT  COUNT  TYPE       COMMENTS
1 <none>     array   1 struct mpinfo stopped by max count
2 <none>     array   2 struct mpinfo stopped by max count
3 <none>     array   2 struct mpinfo stopped by max count
4 <none>     list   155 struct proc  stopped by null pointer
5 proc1      array   1 struct mpinfo copy of 1
6 <none>     list   155 struct proc  copy of 4
7 <none>     mixed?  1 struct proc   subset of 6
```

We now have a pile that contains the process table for process one.

## An Example: Getting the urea of a Process

Let's look at an example that goes through several of these steps. In this example, we get the urea of a process, PID 2003. Because of the way structures are interconnected, there are many ways to do this, and some of them are quicker and easier than this example, but the idea here is to show a variety of q4 commands. Following are the steps we go through:

- Load all processes.
- Keep process 2003.
- Get the VAS structure for the process from the p_vas pointer.
- Using the VAS region list, load all regions for the process.
- Keep the region that has a type of PT_UREA.
- Print the space and offset of that region.
- Load a struct user from that space and offset.

```
q4> load struct proc from proc_list next p_factp max 10000
loaded 150 struct proc as a linked list (stopped by null pointer)
q4> keep p_pid == 2003
kept 1 of 150 struct proc's, discarded 149
```
