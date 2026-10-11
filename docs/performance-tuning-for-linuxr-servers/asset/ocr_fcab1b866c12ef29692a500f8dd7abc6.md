# ## Vectored I/O

The 2.6 Linux kernel provides a full implementation of vectored I/O (also referred to as scattered I/O) through the readv and writev interfaces. The vectored read interface, readv, reads contiguous pages on disk into noncontiguous pages in memory. Conversely, the vectored write interface, writev, writes noncontiguous pages in memory onto disk in a single function call. This I/O mechanism is advantageous for database servers that frequently perform large sequential I/Os. Without a proper vectored read and write implementation, an application performing sequential I/Os does one of the following:

+   - Issues database page size I/Os

+   - Issues large block I/Os and uses the memcpy function to copy data pages between the read/write buffers and the database buffers

Both of these approaches incur expensive computational overhead when scanning terabytes of data, which is a common database size in today’s data warehouses.

# ## Asynchronous I/O

The asynchronous I/O mechanism gives an application the capability to issue an I/O request without having to block until the I/O is complete. This mechanism is ideal for database servers. Other platforms have provided asynchronous I/O interfaces for quite some time, but this feature is relatively new to Linux. To drive I/O throughput without an asynchronous I/O mechanism, database servers usually create many processes or threads that are dedicated to performing I/O. With many processes/threads doing the I/O activity, the database application is no longer blocked on a single I/O request. The downside of using so many processes/threads is the extra overhead costs associated with creating, managing, and scheduling these processes/threads.

The GNU C Library (GLIBC) asynchronous I/O interface utilizes user-level threads to perform blocking I/O operations. This approach simply makes the request appear asynchronous to the application. However, it is no different from the approach previously described and suffers from the same performance drawbacks. To eliminate the problem, the 2.6 kernel introduced a kernel asynchronous I/O (KAI/O) interface. KAI/O implements asynchronous I/O in the kernel rather than in user space via threads and guarantees true asynchrony.

# ## Direct I/O

Direct I/O provides performance comparable to raw I/O, but with the added flexibility of a file system. As such, it is attractive to database administrators who want to leverage the flexibility of maintaining their databases when using file systems as the storage medium.