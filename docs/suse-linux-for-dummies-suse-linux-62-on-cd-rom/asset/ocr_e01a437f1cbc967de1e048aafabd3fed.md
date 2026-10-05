# 238 Part IV: Maintaining Your System

+   - The character and block devices are listed, each with its major device number. (Note that the IDE disk has a major number of 3.)

+   - Finally, the file systems are listed. Note that the only file system that doesn't need a device hooked up to it is proc, which is indicated by the brackets and its name.

In all those numbers and pieces of data, we are concerned about the page in and page out numbers as the swap in and swap numbers in real memory. Although these numbers (particularly the page in and page out numbers) may never be zero, having numbers that are gigantic or increasing at a fast rate is not good because would mean your system memory starved and your CPU is waiting for virtual memory to be brought into real memory before it can continue processing. How much can this slow your computer day? In a particularly bad (and, luckily, rare) case, memory shortages made a program that would normally run in three minutes run ten hours.

![](bbox=[0.115, 0.415, 0.165, 0.485])

In general, if your system seems to be very slow, at the paging and swapping numbers to see whether the system is constantly paging or swapping. More main memory can help the solution.

# Enhancing Disk Performance

After your system has enough main memory, you may want to look at how well your disks are performing. Linux (like a lot of UNIX operating systems) is very disk oriented. Many programs that Linux users execute from disk, execute for a short time (creating swap space on the disk and releasing it), and then terminate. In particular, when you create a pipeline in shell programming, the last few programs on the command line may not do any work because they depend on data flowing through them before they do anything. If no data reaches the last programs in the pipeline, they can't do anything and terminate. Suppose that the last program is the sort program. Its job is to sort the output into a particular order and then allow the display of the output on the screen. If no data comes through the pipeline to sort, the sort program's job is very short (kind of nonexistent), and all the work the sort program did preparing

Linux also does a lot of work with temporary files. The C compiler generates many temporary files while it is compiling a program, and the sort routine does the same thing while sorting (that sort routine). All these temporary files flush data out to the disk or bring data from the disk, creating a bottleneck through the disk subsystem.

Linux sets aside a certain amount of main memory in its dynamic buffer cache to hold data moving from the disk to the CPU and vice versa. When data is read from the disk, it goes into the disk cache. Usually,