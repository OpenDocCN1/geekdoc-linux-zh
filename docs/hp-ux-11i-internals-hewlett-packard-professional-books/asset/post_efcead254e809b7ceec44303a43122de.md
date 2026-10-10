
## C H A P T E R   1 3
### Kernel Services

In addition to managing the system hardware and scheduling processes, the kernel provides a variety of services to both user applications and kernel subsystems. The services we most commonly associate with the kernel—the system calls—are covered in Chapter 4, “Programs, Processes, and Threads.” The kernel also provides a variety of services to other subsystems within the kernel. In this chapter, we look at what some of those services are and how they are handled.

### The Callout Table

The kernel sometimes needs to be able to schedule events to happen in the future. For example, a driver might want a timeout on an I/O operation. The driver starts an I/O and is interrupted by the I/O system when the I/O completes, but if for some reason the I/O doesn’t complete, the driver needs to know about that too. The driver sets a callout for some number of ticks in the future, specifying a routine to be called at that time. If the I/O completes successfully, then the callout is cancelled. If the callout routine gets called, then the driver knows something went wrong.

### Interface

The basic function for setting a timeout is called `timeout()`. It takes three arguments: a pointer to a function to call, a `void*` argument to pass to the function, and an integer representing the number of ticks in the future at which the function should be called. There are also a few other variations on this routine, including `timeout_on_spu()`, which allows the caller to specify on which system processor unit (SPU) the timeout function should run.

There are also functions for canceling a timeout or for finding timeouts. The `untimeout()` function is passed a function pointer and an argument, just like the first two arguments to `timeout()`. If a timeout is registered for that function and that argument, then the timeout is cancelled and the return value will be the number of ticks remaining until the timeout expires. The `find_timeout()` function does the same, but removal of the timeout is optional. In fact, `untimeout` just calls `find_timeout` with the `remove` value set to one.

### Data Structures

The primary data structure used for callouts is the `struct callout`, or `callout_t`. The structure is used for two different things: either a “real callout” — that is, to represent a callout event — or a “callout header.” At boot time a fixed number of callout structures are allocated. The number is determined by the `ncallout` system tunable. These callout structures are divided between the SPUs so that each SPU has its own pool of callout structures. The reason we divide them into per-SPU pools is to reduce lock contention. If we had a single pool, then we’d have to have a single lock controlling access to the pool. Because a callout scheduled on one SPU is triggered by that SPU, it makes sense for each SPU to have its own pool of callouts. An SPU can access its pool without blocking operations on another SPU. In the `mpinfo` structure for the SPU there is a field called `callout_info`, which points to a `struct callout_info_spu` (typed `callout_info_spu_t`). This structure maintains information about the callouts that pertain to that SPU. This structure has (among other things) a pointer to the first `callout_t` in the pool (`ci_callout`), one past the last `callout_t` in the pool (`ci_calloutEND`), and a pointer to a linked list of free callouts (`ci_freelist`).

When a new callout is scheduled, the system gets an available callout structure from the `ci_freelist`, fills in the appropriate data, and then attaches it to a list of callouts that are scheduled. If an SPU runs out of free callouts, it can go to the pools belonging to the other SPUs and “borrow” callout structures from those free lists.

The `callout_info` structure also maintains three sets of linked lists of active events based on when they are scheduled to occur. These are the near-term list pointed to by `ci_time_nr`, the mid-term list pointed to by `ci_time_md`, and the far-future list pointed to by `ci_time_ff`. The division of events into groups like this avoids the overhead of having to search the entire list of callouts at every interrupt. We only have to search the near-term list to see if anything has expired. When the near-term list is empty, we migrate events from the other lists.

To enable us to find a particular callout, there is also a hashtable and hash chains. A hashing function determines which of several hash chains to search for a callout, then that chain is searched to see if the callout is on the list. Figure 13-1 shows the relationship of the callout information in the `mpinfo` structure and the various lists of callouts.

### Per-processor Callout Subsystem

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_368_0.png)

Figure 13-1 Per-Processor Structures for Callouts

### Callout Processing and Expiration

In the previous section we mentioned the three sets of callouts—the near term, the midterm, and the far future. While the far future is a single linked list, the midterm and near term are both collections of lists. The code is designed such that the near and the midterm can have a different number of lists, but currently both have 128 lists. These sets of lists are arranged as a circular array, as shown in Figure 13-2.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_369_0.png)

Figure 13-2 Callout Table Headers

You can think of these as analogous to a clock. On a clock each time the minute hand makes a complete revolution, the hour hand moves forward one tick. Similarly, each list in the midterm wheel represents the same amount of time as the entire near-term wheel. On the near-term wheel all callouts that expire in a particular tick are on the same tick. With 128 lists in the wheel, that means anything expiring in the next 128 ticks is near term. The `ci_time_nr_next` pointer keeps track of which list is the next one due to expire. The `ci_time_nr_futurelist` pointer is the end of the queue—the callouts that expire the latest of those considered near term. Each time we get a clock tick interrupt, we check the expiry time for those callouts pointed to by `ci_time_nr_next`. If the callout is due (or past due), we call the callout functions and then move `ci_time_nr_next` to the next list.

In the midterm wheel, each list represents 128 ticks. When the near-term wheel makes one full revolution—that is, when `ci_time_nr_next` catches up to `ci_time_nr_futurelist`—all of the callouts pointed to by `ci_time_md_next` get moved onto the near-term wheel. We've essentially moved the hand on the midterm wheel up a tick. When the midterm wheel has made a full revolution we go to the far-future list.

The far-future list is just a single list, kept in sorted order. As the midterm wheel needs replenishing, callouts are moved from the far-future list.

All of this magic happens every clock interrupt. The clock interrupt calls `per_spu_hardclock()`, which in turn calls `expire_callouts_spu()`. `Expire_callouts_spu()` calls `redistribute_buckets()` to handle the moving of callouts from one wheel to the next.

While all this sounds like a lot of work, it's actually much less overhead than the alternative. It used to be that all callouts were kept in one big linked list, sorted by expiry time. With that method, you only had to check the head of the list to see if the next callout was due to expire. The problem was the process of keeping the list sorted. With the possibility of thousands of callouts on the list, it becomes very expensive in terms of processing power to walk down the list and find the right place to insert a new callout.

### Kernel Memory Allocation

In Chapter 3, “The Kernel: Basic Organization,” we talked about how the kernel manages virtual and physical memory. Memory is divided into pages of 4 KB each. The kernel’s page allocator handles allocating pages of memory to processes that need them. However, the kernel itself needs dynamic memory too, and it uses a different process. The memory allocations for the kernel are frequently for small areas of memory—the size of a proc structure or the size of a network buffer, for example. It would be impractical to just call the page allocator and request a page each time we need a small piece of memory. That’s where the kernel memory allocator comes in. It handles requests for memory from the kernel, getting pages from the page allocator as needed. It then divides these pages into smaller pieces so that it can be used efficiently.

Beginning with HP-UX version 11.11, the method of tracking and allocating kernel memory has changed. Prior to 11.11 HP-UX, a scheme known as the McKusick & KareI memory allocator, also called the “bucket allocator,” was used. In release 11.11, this was replaced by the new arena allocator.

Although our focus in this book is on HP-UX version 11.11, the bucket allocator is pervasive enough that it’s worth a brief look. Without going into too much detail, we look at the bucket allocator before examining the newer arena allocator.

### The Bucket Allocator

The bucket allocator divides memory requests into buckets by size, where each size is a power of two. Thus, we have a 32-byte bucket, a 64-byte bucket, a 128-byte bucket, and so on. When a kernel subsystem needs to allocate memory, the request is rounded up to the next power of two. So, for example, if a request is for 100 bytes, it will come from the 128-byte bucket.

The arrays bucket_32bit[] (for 32-bit kernels) and bucket_64bit[] (for 64-bit kernels) contain the head of a list of free areas of memory. The index into the array is the power of two of the size of the buckets: 2⁵ is 32, so the head of the 32-byte bucket list is at bucket_64bit[5], and so on.

Memory is allocated using the MALLOC macro. This macro checks the freelist pointer to see if an area of memory of the requested size is on the list. If so, then the first address off the list is returned. If not, then a new page is requested from the page allocator by calling kmal_loc(). This page then is broken into pieces, the pieces are put on the free list, and the first of them is returned to the requester.

When the memory is no longer needed, it is returned to the bucket lists by use of the FREE macro. If a lot of memory allocations are made and then freed, this can leave many pages of
