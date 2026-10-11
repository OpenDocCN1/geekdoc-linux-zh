
# **14.** Given the following query output from V$DB_CACHE_ADVICE, what would be the optimal size of the database buffer cache without wasting resources?

| NAME | SIZE_FOR_ESTIMATE | ESTD_PHYSICAL_READS |
| :--- | :--- | :--- |
| DEFAULT | 10.1797 | 7686 |
| DEFAULT | 20.3594 | 6614 |
| DEFAULT | 30.5391 | 6028 |
| DEFAULT | 40.7188 | 5785 |
| DEFAULT | 50.8984 | 5497 |
| DEFAULT | 61.0781 | 5342 |
| DEFAULT | 71.2578 | 4915 |
| DEFAULT | 81.4375 | 4867 |
| DEFAULT | 91.6172 | 4866 |
| DEFAULT | 101.7969 | 4866 |
| DEFAULT | 111.9766 | 4866 |
| DEFAULT | 122.1563 | 4866 |
| DEFAULT | 132.3359 | 4866 |

- A. 70MB
- B. 50MB
- C. 100MB
- D. 132MB

**15.** Which of these parameters does *not* have an effect on the size of the Database Buffer Cache?

- A. DB_KEEP_CACHE_SIZE
- B. DB_BLOCK_SIZE
- C. DB_MAX_CACHE_SIZE
- D. DB_RECYCLE_CACHE_SIZE

**16.** Why does increasing the size of the Database Buffer Cache improve performance?

- A. Server Processes are more likely to find free buffers when needed.
- B. Buffers are less likely to be moved out of the cache prematurely by the LRU mechanism.
- C. Both of the above are correct.
- D. Neither of the above is correct.

**17.** Which of the following Buffer Pools can be used to cache segments you have determined to be frequently accessed?

- A. Kept
- B. Keep
- C. Cache
- D. Pin

**18.** Which of the following views can be used to determine which segments might make good candidates for the Keep Pool?

- A. V$BH
- B. DBA_OBJECTS
- C. V$CACHE
- D. Any of the above

**19.** Choose the three component pool types available in the database buffer cache.

- A. Default
- B. Common
- C. Keep
- D. Recycle

**20.** What are tables called whose buffers are placed at the most recently used end of the LRU List, even when full table scanned?

- A. Pinned tables
- B. Cache tables
- C. Kept tables
- D. None of the above

## Answers to Review Questions

1. D. The LRU list is used to keep frequently accessed buffers in memory. The Dirty List keeps track of buffers whose copy in memory has changed. Database Writer (DBW0) writes the dirty buffers to disk.
2. B. Table, index, cluster, LOB indexes, LOB segments, rollback segments, and temporary segments can all be cached in the Database Buffer Cache.
3. C. Each user’s Server Process copies the requested blocks into the Database Buffer Cache.
4. A. Segment blocks are copied into buffers that are placed at the most recently used end of the LRU List.
5. A. Once accessed, any cached buffers are moved from their current location on the LRU List to the beginning, or most recently used (MRU) end, of the LRU list.
6. C. Dirty buffers store data that has been changed by the application user but has not yet been written to disk by DBW0.
7. D. As the Server Process searches the LRU List for free buffers, dirty buffers are moved to the Dirty List where they are written to disk by DBW0 when the Dirty List reaches its threshold length.
8. D. In addition to these times, DBW0 also writes dirty buffers to disk when tablespaces that store blocks for those segments are placed in hot backup or offline mode and when segments are dropped.
9. C. The Database Buffer Cache hit ratio finds the percentage of buffer requests able to be satisfied using the existing cached buffers.
10. C. The V$SYSSTAT dynamic performance view contains statistics on the total number of buffers read and the number of those that were read from disk.
11. D. Hit ratios may be lower for non-OLTP systems.
12. B. Only the Default Pool is required. The Keep and Recycle Pools can be configured to enhance Buffer Cache performance after frequently and infrequently accessed segments have been identified, respectively.
13. B. Database Writer is responsible for writing blocks from the Database Buffer Cache to the datafiles on disk.
14. A. The best setting for the DB_CACHE_SIZE would be 70MB because any increases beyond this point yield only a small reduction of physical reads.
15. C. DB_MAX_CACHE_SIZE is not a valid initialization parameter.
16. C. Increasing the size of the Database Buffer Cache makes more free buffers available and cuts down on unwanted LRU flushing of buffers.
17. B. You can assign frequently accessed application segments in the Keep Buffer Pool by using the STORAGE (BUFFER_POOL KEEP) parameter with the ALTER command.
18. D. The V$BH and V$CACHE dynamic performance views can be used to determine which segments currently have their blocks cached in memory. Additionally, the DBA_OBJECTS data dictionary view can be joined to V$BH to determine the owner and name of each cached segment.
19. A, C, D. The Default, Keep, and Recycle pools are available in the Database Buffer Cache. You can specify which pool you want to place a segment into by utilizing the BUFFER_POOL syntax on the storage clause for the table or index segment when defining or altering the segment definition.
20. B. Tables that have been created or altered using the CACHE keyword, or accessed using the CACHE hint, will have their buffers placed at the most recently used end of the LRU list during a full table scan.

# Chapter 6

# Tuning Other SGA Areas

**ORACLE9i PERFORMANCE TUNING EXAM OBJECTIVES COVERED IN THIS CHAPTER:**

- Describe the UGA and session memory considerations
- Set the Large Pool
- Identify issues associated with managing users in a Shared Server environment
- Diagnose and resolve performance issues with Oracle Shared Server processes
- Configure the Oracle Shared Server environment to optimize performance
- Monitor and size the Java Pool
- Control the amount of Java session memory used by a session

> Exam objectives are subject to change at any time without prior notice and at Oracle’s sole discretion. Please visit Oracle’s Certification website (http://education.oracle.com/certification/) for the current exam objectives listing.

![](img/832fbc6aca8b6075843ca6f2356c0a8d_329_0.png)

![](img/832fbc6aca8b6075843ca6f2356c0a8d_330_0.png)

So far, you have examined tuning techniques for two SGA components: the Shared Pool and the Database Buffer Cache. These two SGA components, and the Redo Log Buffer discussed in Chapter 7, “Tuning Redo Mechanisms”, are used by every Oracle application. This chapter, however, will focus on tuning three areas within the SGA that may or may not be utilized in all environments:

- Shared Pool architectural components
- Large Pool
- Java Pool

Because some Oracle environments do not make use of these SGA components, this chapter will discuss the essential concepts related to each of these areas before introducing the techniques used to monitor and enhance their performance.

## Shared Server Concepts

Each Oracle application user has two processes associated with their connection to the database: a User Process, which executes on the user’s client machine or on the application’s web server, and a Server Process, which executes on the Oracle Server machine.

In the default Oracle9i configuration, called Dedicated Server, each user’s Server Process is dedicated to servicing requests for that user’s session only. On Unix systems these Server Processes execute on the Oracle server as individual OS processes. If there are 50 connected users, then there will be 50 corresponding Server Processes running on the Oracle server machine to service their database activities.

A second optional configuration, called Shared Server, is also available. In this configuration, several Shared Server processes are created on the Oracle

![](img/832fbc6aca8b6075843ca6f2356c0a8d_331_0.png)

server machine. These Shared Server processes can be used to send application SQL statements to, or return data from, the instance by any User Process that needs them.

In versions prior to Oracle9i, the Shared Server option was referred to as the Multithreaded Server (MTS) option.

### Oracle Objective

Identify issues associated with managing users in a Shared Server environment

You can think of the difference between Dedicated Servers and Shared Servers as being much like the difference between owning your own automobile and using taxicabs when traveling from place to place. If you own your own vehicle, you can go wherever you want to go, whenever you want to go there, without having to wait for access to an automobile. However, when you are not using your vehicle, when you're asleep for example, that expensive resource goes completely unused. Conversely, if you use taxicabs as your mode of transportation, you may or may not have access to the vehicle precisely when you want it, but you will eventually get to where you want to go. However, other patrons can continuously utilize the taxicab during the times that you do not need it, making good use of that resource.

These distinctions are also true of Dedicated and Shared Servers. The Dedicated Server configuration provides for efficient communication between the User Process and the Server Process, because the user's Server Process is dedicated to sending application SQL statements to, or returning data from, the instance for only that single user. However, just as with automobiles, Dedicated Servers have the disadvantage of consuming memory and CPU resources on the Oracle server machine—even when the user is idle. This can lead to scalability problems when the number of application users is large because the server resources required to support the user Server Processes are often not utilized efficiently.

The Shared Server configuration solves the scalability concerns of the Dedicated Server configuration by better utilizing the Oracle server machine's available memory and CPU to support the activities of the application users. But, just as with taxicabs, Shared Servers can also negatively impact
