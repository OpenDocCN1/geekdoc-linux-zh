
## 7.1.6 Swap Space

Solaris swap space has two important states that we must observe: swap reservation and physical swap allocation. (See “The swapfs Layer” on page 156 for details about the Solaris swap implementation.) Two important measures of Solaris swap space are these:

- The amount of virtual swap space that is configured and available for swap reservations
- The amount of physical swap space that is configured and available for physical page-outs

We need to ensure that neither of these two types of swap space is exhausted. When we exhaust virtual space, malloc() and related calls fail, which means our programs start to fail. When we exhaust physical swap space, programs do not fail, but since there is no longer any space left to page them out to, the Solaris kernel begins locking down pages of memory that would normally be paged out.

### 7.1.6.1 Virtual Swap Space

The amount of virtual swap space configured is the sum of the amount of physical swap space (disk swap space) plus the amount of memory that Solaris can use for swap. We can use the `swap -s` command to see if enough virtual swap space is configured. When the “available” column falls to zero, programs will start to fail. We can add virtual swap by simply adding more physical swap space.

```text
# swap -s

total: 251232k bytes allocated + 25544k reserved = 276776k used, 514992k available
```

### 7.1.6.2 Physical Swap Space

The amount of physical swap space configured is simply the amount of physical disk or file-based swap configured through /etc/vfstab or by the swap command. The amount of physical swap space affects the amount of virtual swap space available for reservations, as just discussed, but it also affects the amount of physical space available that pages can be paged out to. Even if there is sufficient total virtual space for reservations, we may still have insufficient space for physical page-outs. The physical swap configuration and the amount of physical swap available for pages to be paged out to can be seen with the `-l` option of the `swap` command. The amount of physical swap space available for paging out to is shown in the free column (note that the free column is not the amount of physical swap available for reservations, it’s the amount of space available for physical page-outs). If free physical swap is zero, then pages will no longer be paged out to swap and memory will effectively start being locked down.

```text
# swap -l
swapfile             dev   swaplo blocks   free
/dev/dsk/c1t2d3s1    118,105   16 1048784 47204
```

Ensure that both `swap -s` “available” and `swap -l` “free” are nonzero.

## 7.2 Memory Monitoring Tools

To understand the memory behavior and requirements of a particular system, we need to be able to measure the activity and operation of the virtual memory system. In this section, we look at the current tools bundled with the Solaris kernel, and we discuss some other unbundled tools that allow us to look a little deeper into the virtual memory system.

We have two basic objectives in looking at Solaris memory: to find out where all of the memory is allocated and to look at memory (or paging) activity. Table 7-1 lists the tools we discuss and the capabilities of each.

**Table 7-1** *Solaris Memory Monitoring Commands*

| Tool | Location of Tool | Capabilities for Memory Utilization Reporting | Paging Activity Reporting |
| --- | --- | --- | --- |
| `vmstat` | `/usr/bin` | Basic | Systemwide only |
| `ps` | `/usr/bin` | Process size | — |
| `swap` | `/usr/bin` | Swap allocation | — |
| `wsm` | Engineering/free | Working set size | — |
| `ipcs` | `/usr/bin` | SysV shared memory | — |
| MemTool | Engineering/download | Process/file system cache | — |
| `memstat` | Engineering/download | Same as vmstat | Breakout of paging for file systems, applications, and libraries |
| `pmap` | `/usr/proc/bin` | Process address map | — |
| `pmap -x` | `/usr/proc/bin` | Process physical memory utilization, including the amount of memory shared among processes | — |
| `crash` | `/usr/bin/crash` | Kernel memory utilities | — |
| `dbx` | `SPARCworks` | Memory leaks | — |

## 7.3 The vmstat Command

The Solaris vmstat utility summarizes various functions within the virtual memory system, including systemwide free memory, paging counters, disk activity, system calls, and CPU utilization. The output of vmstat is shown below with explanations of the various fields. Let’s take a look at how we can use vmstat to get a quick summary of what is happening on our system. Note that the first line of output from vmstat shows a summary since boot, followed by the output over the last 3 seconds for each additional line.

![](img/220ae4af07df2fe8e5be69d27f885d1b_282_0.png)

### 7.3.1 Free Memory

Our vmstat example shows that we have 2,096 Kbytes of memory free, which seems low for a system with 128 Mbytes. Recall from the introduction that free memory is low because the VM system has used all of it for file system caching, which means that free memory has fallen to approximately the value of lotsfree. (See “The Page Scanner” on page 178 for the meaning of lotsfree.) Although free memory is almost zero, plenty of memory is still available for applications. We will look at how to observe how much of our memory is being used for file system caching when we later discuss MemTool in detail.

### 7.3.2 Swap Space

The `vmstat` command reports the amount of virtual swap space that is free and available for reservation. This is the sum of the total amount of physical swap space available plus the amount of memory swap space. It is equivalent to the “available” column in `swap -s`.

### 7.3.3 Paging Counters

The `vmstat` paging counters show us the systemwide virtual memory paging activity. The counters include paging activity to/from program memory (anonymous memory) and to/from file systems. The fields are shown in Table 7-2.

**Table 7-2** — *Statistics from the vmstat Command*

| Counter | Description |
| --- | --- |
| re | Page reclaims — The number of pages reclaimed since the last sample. Some of the file system cache is in the free list, and when a file page is reused and removed from the free list, a reclaim occurs. File pages in the free list can be either regular files or executable/library pages. |
| mf | Minor faults — The number of pages attached to an address space since the last sample. If the page is already in memory, then a minor fault simply reestablishes the mapping to it. |
| pi | Page-ins — The number of pages paged in since the last sample. A page-in occurs whenever a page is brought back in from the swap device or brought from a file system into the file system cache. |
| po | Page-outs — The number of pages paged out and freed. A page-out is counted whenever a page is written and freed. Often, this is as a result of the pageout scanner, fsflush, or file close. |
| fr | Page frees — The number of pages that have been freed by either the page scanner or by the file system (free behind). |
| de | The precalculated, anticipated, short-term memory shortfall. Used by the page scanner to free ahead enough pages to satisfy requests. |
| sr | The number of pages scanned by the page scanner per second. |

### 7.3.4 Process Memory Usage, ps, and the pmap Command

The memory usage of a process can be categorized into two classes: its virtual memory usage and its physical memory usage. The virtual memory size is the amount of virtual address space that has been allocated to the process, and the physical memory is the amount of real memory pages that has been allocated to a process. We refer to the physical memory usage of a process as its resident set size, often abbreviated RSS. We can use the `ps` command to display a process’s virtual and physical memory usage.

```text
# ps -e -o pid,vsz,rss,args
  PID  VSZ  RSS COMMAND
11896 1040  736 ps -e -o pid,vsz,rss,args
11892 1032  768 sh
13603 1032  768 sh
 2695 1896 1432 telnet donah
 2693 1920 1456 telnet donah
 2433 1920 1440 telnet firefly
 3143 1920 1456 telnet devnull
 2429 1920 1440 telnet firefly.eng
 2134 1920 1440 telnet devnull
```

From the ps example, we can see that the /bin/sh shell uses 1,032 Kbytes of virtual memory, 768 Kbytes of which have been allocated from physical memory. We can also see that two shells are running. ps reports that both shells are using 768 Kbytes of memory each, but in fact, because each shell uses dynamic shared libraries, the total amount of physical memory used by both shells is much less than 768K x 2.

To ascertain how much memory is really being used by both shells, we need to look more closely at the address space within each process. Figure 7.1 shows how the two shells share both the /bin/sh binary and their shared libraries. The figure shows each segment of memory within the shell’s address space. We’ve separated the memory use into three categories:

- **Private** — Memory that is mapped into each process and that is not shared by any other processes.
- **Shared** — Memory that is shared with all other processes on the system, including read-only portions of the binary and libraries, otherwise known as the “text” segments.
- **Partially shared** — A segment that is partly shared with other processes. The data segments of the binary and libraries are shared this way because they are shared but writable, and within each process are private copies of pages that have been modified. For example, the /bin/sh data segment is mapped shared between all instances of /bin/sh but is mapped read/write because it contains initialized variables that may be updated during the execution of the process. Variable updates must be kept private to the process, so a private page is created by a “copy on write” operation. (See “Copy-on-Write” on page 152 for further information.)
