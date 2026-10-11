+   11. D. All of these areas can provide useful statistics and timings. Each of these areas will be discussed in much greater detail later in the book.

+   12. D. CPU, memory, and I/O are all affected by tuning changes. For example, changes made to reduce I/O generally increase the demands on memory and CPU.

+   13. B. The System Global Area and its associated PMON, SMON, DBW0, LGWR, and CKPT background processes make up the Oracle instance.

+   14. C. An Oracle database consists of the control files, Redo logs, and datafiles. The trace files, archived Redo logs, password file, and init.ora are not considered part of the database.

+   15. B. Disk read/write activity and controller caching efficiency are two important server statistics that can be gathered using vendor-supplied tools.

+   16. B. Having a proper starting benchmark measurement and a target tuning objective are both key elements of a goal-oriented tuning technique.

+   17. B. The Database Buffer Cache holds the data, index, and rollback blocks that users are accessing via the application. Database Writer (DBW0) writes these blocks to the database datafiles.

+   18. C. Although moving files around to distribute I/O is generally a good exercise if your system is I/O bound, it will probably yield very little benefit if your system is CPU bound.

+   19. A. TIMED_STATISTICS is required to be set to TRUE if you want the Oracle Server to capture and maintain performance related statistics.

+   20. C. The probable cause is that the system is running short on memory. Two possible remedies would be to reduce the size of the SGA or increase the available memory on the Server.