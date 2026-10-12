
There are (as always) exceptions. Power users, programmers, and systems administrators fall outside of both the high-end server range and home hacking system low-end range. They all have special needs that vary. More often than not, however, all of those three have a pretty fair idea based on experience of what they need. For a systems administrator, a machine powerful enough to at least prototype some of the software that will be on servers is desirable. Usually about half of the RAM the servers have will suffice for testing (since you will be doing the testing). Power users may opt for fancier graphics and different X Window Managers, so a healthy 64MB may be in order. Linux programmers usually require about 32–64MB of RAM to run and compile programs.

## Additional RAM

Getting additional RAM is an altogether different situation. It really depends on how bottlenecked the memory currently is on a system. If it is nearly swap thrashing all of the time, buy at least twice as much RAM to just get out of an obviously bad situation. Otherwise, take a backward incremental approach to buying additional RAM. If excessive swapping is happening at certain times, make sure it is indeed the RAM that is causing it and buy close to twice as much. If the system is marginally swapping it is probably alright, but if you discover it is constantly paging at around 50% or so, it wouldn’t hurt to pick up 20%–30% more RAM just to be on the safe side.

## Purchasing RAM for a New System

The good thing about buying additional RAM is that you have a base to go from. When buying RAM for a new and unused system, it is unclear as to how much you should get. Always err on the high side with systems that are going to be used in an organizational setting. On a final note, when transferring a system, the normal capacity plan is to double the current system and add roughly 20% to the result of doubling. Although that formula is normally used for disk capacity, I have found it works well with RAM also.

To summarize, single-user or few-user systems with basic Web server processes running need 64MB of RAM. Above that, look at 0.5 to 1GB of memory. A strange gap, yes, but not unrealistic. It draws parallel to previous UNIX systems and should be no surprise to the seasoned systems administrator. The great thing about Linux is that user processes are not directly proportionate to RAM. If you as a single user need 32MB of RAM, that does not mean that two users on a multi-user system require 64MB of RAM; as a matter of fact, in that instance no change would be required.

As a disclaimer, it should be noted that there are systems out there that operate in the terabyte range for memory, such as large On Line Transaction Processing Systems. Linux has not yet reached that level; however, one day it will. The measurement techniques for such systems are vastly different than those for small to mid-range systems.

Once the amount of RAM is determined, the next obvious step is swap space, which is covered in the next section.

## Swap Space Priorities

RAM is obviously not the only consideration when piecing together or adding to a Linux system. Swap space is also another great priority. While many UNIX pundits will advise using the following formula:

```
2 * RAM = swap space
```

there are many alternatives to help you preserve disk space and use a practical amount of swap space.

## Calculating Swap Space

Following is a method I have heard of that many Linux administrators use, and it is quite practical:

- 1. Estimate your total memory needs. Consider the largest amount of space you will need at any given time. Consider what programs you will be running simultaneously. The easiest way to do this is to set up bogus swap space and load up all of the programs you will be using at once. Then see how much memory is being used.
- 2. Add a couple of megabytes as a buffer for programs you may have missed or think may in fact be used.
- 3. Subtract the amount of physical memory you have from this total. The amount left over will be the amount required to run your system while it is in full use.
- 4. If the total in step 3 is three times the amount of physical memory you have, you will have problems. Consider getting more RAM.

If using this method shows you use less than the amount of physical memory, you might assume that you do not need any swap space. You should add some swap space anyway because the system will use it on a convenience basis by swapping out any data that is not in use. In this case, create about the same amount of swap space as you have physical memory (or a little lower).

Of course, swap space, like all other performance issues in Linux, becomes much more complicated when large groups of users come into play. When dealing with large groups of users for whom the betterment of your system is beholden to err on the high side, provide physical RAM times two in swap space (the default method mentioned above).

While Pitt’s method can be used for determining how much swap space is needed on larger systems, within the context of large systems it is a much more prudent practice to use the maximum recommended swap space to ensure users will not run into any problems.

## Assigning Swap Space

Once you have decided how much swap is actually going to be used, the task of assigning it comes into play. Most Linux distributions (and Red Hat is no exception) provide a means to set up swap during the installation. It is also a good practice to try to actually create most of the swap space on the first portion of the first drive within the system. This means that the drive heads will have a smaller distance to travel while paging data in and out of RAM. Another practice is to divide up swap to reduce I/O contention. Again, keeping the swap space near the beginning of each physical drive is recommended to keep the distance traveled by the heads to a minimum. When using multiple disks, try to keep the swap space assigned as equal as possible. For instance, say you have three 8GB disks and 128MB of RAM. You have determined that you will actually require 256MB of swap space. The first swap area should be 86MB, the second 85MB, and the last one 85MB.

> **Note**
> 
> There may be instances that take exception to equally distributing swap space. For example, you can apply the first method and set up the first (and highest priority) swap area to match “expected” use, then divide up the rest into other lower priority swap areas.

## Swap on/Swapoff

Let’s take a quick glance at the swap on/swap off commands. By definition, swap on and swap off are used to specify devices on which paging and swapping are to take place or be disabled. At boot time, swap on is used in /etc/rc to specify the system’s swap areas. swap on is interesting in that you can look at paging activity with it as well as assign priority and space. The syntax for looking at activity is:

```
$ swap on -s device_name
```

To allocate swap space, let us again use the aforementioned example of 86MB for our first swap partition running at default priority (changing or starting with a different priority will be discussed a little later).

First, using either the fdisk utility, disk druid, or some other utility, we create the swap partition at:

```
/dev/hda6 with a size of 86MB
```

### Note

The command mkswap can also be used to set up swap space. The syntax is:

```
$ mkswap -c device_filename blocksize
```

Next, we tell the system to use it:

```
$ swapon /dev/hda6
```

### Note

For a swap file versus partition, we would simply allocate the filename:

```
$ swapon /my_swap_file
```

Once the actual swap areas have been allocated, you may want to peruse swap prioritization. For instance, with the preceding example, you probably would like the first swap area to have the highest priority and the other two some lower priority value. For the example, let's say our swap has already been built and allocated according to this list:

```
/dev/hda6 86MB
/dev/hda7 85MB
/dev/hda8 85MB
```

And we want our general priorities to look like this:

```
/dev/hda6 highest
/dev/hda7 second highest
/dev/hda8 third highest
```

The basic premise is that /dev/hda6 must be exhausted before using /dev/hda7, and so on. Since there are only three swap areas, it makes sense to set the highest priority to 2, and not set a priority for /dev/hda8 (leaving it at the low default priority of 0). Here is the syntax for changing the priority for /dev/hda6 and 7:

```
$ swapon -p 2 /dev/hda6
$ swapon -p 1 /dev/hda7
```
