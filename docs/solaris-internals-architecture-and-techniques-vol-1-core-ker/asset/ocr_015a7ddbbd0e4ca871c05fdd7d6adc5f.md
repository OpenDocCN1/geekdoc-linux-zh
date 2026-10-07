# The Hardware Address Translation Layer

However, user applications had no way to take advantage of the large-page-page support until Solaris 2.6. With that release, Sun enabled the use of 4-Mbyte pages for shared memory segments. This capability primarily benefits databases, since databases typically use extremely large shared memory segments for database data structures and shared file buffers. Shared memory segments ranging from several hundred megabytes to several gigabytes are typical on most database installations, and the 8-Kbyte page size means that very few 8-Kbyte shared memory page translations fit into the TLB. The 4-Mbyte pages allow large contiguous memory to be mapped by just a few pages.

Starting with Solaris 2.6, System V shared memory created with the intimate shared memory flag, SHM_SHARE_MMU, is created with as many large 4-Mbyte pages as possible, greatly increasing the performance of database applications. Table 5-23 shows a sample of the performance gains from adding large-page shared memory support.

# Table 5-23 Large-Page Database Performance Improvements

| Database | Performance Improvement |
| --- | --- |
| Oracle TPC-C | 12% |
| Informix TPC-C | 1% |
| Informix TPC-D | 6% |