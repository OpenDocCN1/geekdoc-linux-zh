remember the good old days when the “process” was the indivisible dispatchable unit of work under AIX V3? Each process neatly lined up by priority in serial 
r run queues awaiting a turn on the CPU. There were parent processes, children, 
grandchildren, with each process generation spawning the next. All members of one 
big happy init family. As in most families, it was often difficult to get family members 
to talk to each other or share their belongings. When you did get them to communicate 
or share, everyone tried to talk or grab a resource at the same time. You had to get heavy-
handled and resort to locks and semaphores to keep everyone in line. Process life could 
be difficult, but it was simple and understandable.

Then in AIX V4 came multiprocessing. AIX developers decided to speed up the pace 
of life in process city. Rather than make all processes wait on just one CPU, they added 
the capability to dispatch across multiple CPUs. More CPUs mean that the work gets 
done faster. They also decided to break up the process structure into components called 
threads. Each thread is a dispatchable unit of work. Multiple threads can be executing 
simultaneously on multiple CPUs. These new features improved system throughput, 
but they didn’t come without additional complexity and some overhead.

With AIX 5L, comes a scalable 64-bit kernel that can support very large application 
workloads that are executing on 64-bit hardware. The scalability of the 64-bit kernel is 
primarily due to the larger kernel address space. The kernel supports both 64-bit and 
32-bit applications.

# # KERNEL ARCHITECTURE

The AIX kernel fundamentally started as a System V.2 kernel. However, the System V 
architecture represents only AIX’s roots, not its whole. The AIX kernel design includes a 
number of features and extensions that set it apart from other SVSv5-based kernels. AIX 
V3 introduced most of these features when the POWER architecture hit the marketplace 
in 1990. Now we have progressed over the years through POWER 2 and POWER 3 to the 
current POWER 4 processor. With the introduction of the POWER 4 chip, IBM is planning 
for a huge increase in processing power as the newer versions of the POWER 4 chip are 
released. This first rendition has dual processors in same package, with each processor 
having its own L1, L2, and RAM caches. The next release will have four processors, 
and the one to follow will have eight processors per package. The goal is to have a Teraflop of 
processing power in a single four-inch-square package of 32 processors.

The progression of the AIX kernel was in keeping with the progression of the 
hardware. We started AIX with a 32-bit kernel. Then the address space of a particular 
process was limited to $2^{32}$ bytes (4GB). With the advent of the 64-bit kernel came huge 
amounts of address space in the multi-terabyte range. A 64-bit application can, in theory, 
address $2^{64}$ bytes of data; however, AIX is currently limited to a more realistic span of $2^{50}$ 
bytes. The largest impact of this extended address space is with mathematical applications. 
Now long integers are 64 bits, but integers are still 32 bits. With the 64-bit long integers, the 
application can make twice as many calculations in the same time frame.