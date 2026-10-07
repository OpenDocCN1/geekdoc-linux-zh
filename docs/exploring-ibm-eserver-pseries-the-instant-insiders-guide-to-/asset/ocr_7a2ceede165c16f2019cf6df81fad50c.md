# Application Programs and Operating Systems 235

| Number of Bits | Addressable Bytes | Theoretical Memory Limit |
|---|---|--|
| 8 | 2 raised to the power 8 | 256 bytes |
| 16 | 2 raised to the power 16 | 64 KB |
| 32 | 2 raised to the power 32 | 4 GB |
| 64 | 2 raised to the power 64 | 16 million TB |

**Figure 3.12.** Memory addressability for operating systems with varying numbers of bits.

Let's assume that you are a manufacturing firm and that you have a relatively large database of, say 30 GB, which you make available to your enterprise applications as human resources, accounting, and distribution. If you have a UNIX system with 16 GB of main memory, you can load large segments of your database into real memory, increasing the likelihood that the data you require will be in main memory. This allows you to avoid the performance hit of going to the disks for the information, swapping or paging this data into real memory, and writing the replaced data back to the disk.

The preceding example assumed a 64-bit database as well as operating system and hardware, allowing big “chunks” (more than 4 GB) to be manipulated at one time. However, even if an individual database is not that large, performance advantages can still be realized by having a 64-bit operating system and large memory available. In this case, you may have several applications and many processes running more than, say, 2 GB or 3 GB of memory (or even considerably), greater amounts of total memory will reduce memory contention between the processes that are running.

AIX 5L gives the application developer and the end user a full 64bit environment. It supports 64-bit hardware, which includes all pSeries systems and currently available RS/6000 systems except Models B550 and 150, and 64-bit applications, such as Oracle 8 and IBM DB2. AIX 5L has preserved full binary compatibility with previous hardware and applications. Existing 32-bit applications will run absolutely unchanged and without performance degradation on AIX 5L. It will run on all of the existing 32-bit RS/6000 systems that are still supported. This is important to many users because they prefer, for ease of management, to have all of the systems in their enterprise the same