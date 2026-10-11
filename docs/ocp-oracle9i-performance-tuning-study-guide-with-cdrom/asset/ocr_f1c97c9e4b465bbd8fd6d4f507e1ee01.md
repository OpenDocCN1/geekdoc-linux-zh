# ## Answers to Review Questions

+   1. A. Immediate latches continue processing while waiting for the latch to become available. Willing-to-Wait latches will sleep between attempts at acquiring the latch.

+   2. C. Willing-to-Wait latches sleep before trying to obtain a previously requested latch that was busy.

+   3. C. Latches are used to protect access to memory structures like the LRU lists and the Redo Log Buffer.

+   4. B. The GETS column of V$LATCH shows the number of times that a Willing-to-Wait latch was obtained without waiting.

+   5. D. The IMMEDIATE_GETS column of V$LATCH shows how often Immediate latches were obtained without waiting.

+   6. C. User Server Processes search the LRU list using the Cache Buffers LRU Chain latch when placing copies of blocks into the Database Buffer Cache.

+   7. D. The DROP TABLE statement would cause a DDL Lock to be obtained on the table to ensure that no session can access the table as it is being dropped. All the other statements would obtain some type of row level lock.

+   8. A. A hit ratio of at least 99 percent is desired for the Database Buffer Cache LRU List.

+   9. B. Segment blocks are taken off the Free List when they are filled to PCTFREE and placed back on the Free List when they are emptied to PCTUSED.

+   10. A, C, D. The V$SYSTEM_EVENT view contains statistics on the buffer busy waits event. V$WAITSTAT contains statistics about waits for Free List blocks. V$SESSION_WAIT can be joined to DBA_SEGMENTS to determine which segments are experiencing Free List contention.

+   11. C. The process will spin on the CPU a number of times until releasing the CPU. The spin process is a type of internal wait mechanism.

+   12. C. Oracle uses rollback segments and SCNs to ensure that users always see a read consistent view of the database.