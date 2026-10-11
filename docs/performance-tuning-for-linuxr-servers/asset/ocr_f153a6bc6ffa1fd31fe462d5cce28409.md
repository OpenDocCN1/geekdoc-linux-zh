# ## Database Tuning Areas to Consider

Consider the following areas within a database that can be tuned for improved performance:

+   - I/O
+   - Queue length and response times
+   - Load balancing
+   - Global memory
+   - Logging device

Each of these sections gives an in-depth look at things to consider.

# ## I/O Tuning

You must make many decisions when it comes to *I/O* tuning. Will you use raw devices or file systems? What about direct I/O? What blocksizes should you choose for your database? If you are running strictly an OLTP (online transaction processing, characterized by small, random reads/writes) workload, you want to choose a smaller blocksize for example, 2K. For DSS long running queries, a database that implements a sophisticated query optimizer and complex memory (sort/hash area) parameter controls, a larger blocksize improves database scans 8K (or larger if the database provides). What if your workload entails both OLTP and DSS? Careful database parameter tuning needs to be considered; in some instances, compromise is the way to go, perhaps settling with a 4K blocksize.

# ## Queue Length and Response Times

On Linux, *vmstat* is a good tool for measuring I/O bandwidth. Two columns under the I/O section are labeled bi and bo. These columns are supposed to be blocks in and blocks out from a block device, as described in the man pages for vmstat. However, in various Linux distributions these columns actually report transfer rate in KBps from character devices (raw) or a block device (file system) during the measurement interval. For both workloads, if queue length is greater than 1, there is likely some contention. For OLTP, response times over 50ms are a concern.

# ## Load Balancing