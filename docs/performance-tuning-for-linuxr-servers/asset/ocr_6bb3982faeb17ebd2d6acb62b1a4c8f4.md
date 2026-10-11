+   - Multiple read and write operations can be issued to multiple open file descriptors.
+   - Both sequential and random access devices can handle I/O requests.
+   - Outstanding I/O requests can be canceled.
+   - The process can be suspended to wait for I/O completion.
+   - I/O requests can be tracked when the request is queued, in progress, and completed.

The following functions perform and manage asynchronous I/O operations:

| Function | Description |
|---|---|
| aio_cancel | Cancels one or more requests pending against a file descriptor. |
| aio_error | Returns the error status of a specified operation. |
| aio_fsync | Asynchronously writes system buffers containing a file's modified data to permanent storage. |
| aio_read | Initiates a read request on the specified file descriptor. |
| aio_return | Returns the status of a completed operation. |
| aio_suspend | Suspends the calling process until at least one of the specified requests has completed. |
| aio_write | Initiates a write request to the specified file descriptor. |
| lio_listio | Initiates a list of requests. |