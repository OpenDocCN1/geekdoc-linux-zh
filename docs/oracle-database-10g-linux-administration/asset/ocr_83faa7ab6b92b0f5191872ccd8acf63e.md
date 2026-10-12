on the type and number of operations being done during that period, and as such is very difficult to predict.

So, what do you do in order to size the memory for the type of application that you are running? Well, there are several ways to do this. The easy way out is to simply get as much memory as you can afford and allocate it to the Oracle processes and SGA. On one hand, this is cheating, since you haven't really sized the memory subsystem at all. However, since memory is relatively cheap compared to memory prices a few years ago, this is now a practical thing to do.

Remember that the memory Oracle uses can actually be thought of as two separate pieces. The SGA is kept in shared memory, which is governed by Linux kernel parameters that limit the size of shared memory. Shared memory is allocated out of a special pool of memory and is not swappable. The Oracle processes memory, however, can be swapped out. When considering how big to make the SGA, remember that the Oracle processes can require a large amount of memory. The more processes you have running, the more memory they will consume.

Keep in mind that with 32-bit processor-based systems, it is not usually very efficient to purchase more than 4GB of RAM since this is all the memory that a 32-bit processor can use without using memory extensions that have a lot of overhead. Going from 4GB to 5GB of RAM might be slower, due to the overhead involved in using memory above 4GB, but using 8GB of RAM will be faster than 4GB of RAM.

In addition, with the PGA_AGGREGATE_TARGET parameter you can now dial in the amount of memory used by all of the processes, thus taking advantage of available memory without running the risk of paging.

If you are not using Oracle9i or later, the manual method of sizing memory is to monitor the system and try to interpolate the amount of memory necessary with additional processes being used. For example, take a snapshot of the memory being used with 100 users connected and then again with 200 users connected. This should allow you to estimate the amount of memory used per user. However, the PGA_AGGREGATE_TARGET parameter will nullify use of this method, since the sum of all PGA memory should remain constant regardless of the number of users.

# ## I/O Subsystem Sizing

The I/O subsystem has unique sizing characteristics due to the nature of the makeup of the components. Why is this important? A properly configured I/O subsystem will allow Oracle to perform optimally. A poorly configured I/O subsystem can easily become a bottleneck and can severely affect performance. Let's look at the I/O subsystem starting with the basic component—the disk drive—and then look at RAID controllers and RAID levels.

# ### The Disk Drive

The basic component of the I/O subsystem is the disk drive, also commonly known as the hard disk drive or hard disk. Anyone who has anything to do with computers knows what a disk drive is. In this section, you will be given a brief overview of how the disk drive operates and what the limiting factors are.