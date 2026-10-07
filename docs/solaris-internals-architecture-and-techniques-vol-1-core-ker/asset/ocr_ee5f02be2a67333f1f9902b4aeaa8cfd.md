# Asynchronous I/O

have raw device entry points through the /dev/vx/rdsk and /dev/md/rdsk device-special files, and the pseudorandom implemented for these volume managers include async I/O routines for kaio support. You can also use the kaio test described below to establish whether your underlying device supports kaio.

If kaio support is available, here is what happens:

+   - The kernel allocates an aio req structure from the queue (or creates a new one in kernel memory with kmmem_alloc) and calls the async I/O routine in the appropriate device driver.

+   - Inside the driver, the required kernel data structures are set up to do the I/O, and an async-I/O-specific physical I/O routine, aphysio, is entered.

+   - Synchronous raw I/O uses the kernel physio function, whereby kernel buffers are set up, and the driver strategy routine is called to do the actual I/O.

+   - The physic routine waits for the driver strategy routine to complete the buffer biowait() kernel code.

+   - The aphysio routine sets up the async I/O support structures and signal mechanism, then calls the driver strategy without waiting for the I/O to complete.

The presence of ENOTSUP error signals that kaio support is unavailable. That is, when the libaio (or libposix for the POSIX interfaces) makes a kaio system call, the kaio returns an ENOTSUP error if kaio is not supported. If kaio support is not available, the code path then is very different.

+   - Generally, the original user-thread asio facility performs the I/O in an async I/O queue and hands off the aiore and aiwrite to a worker thread that was created when the libaio library was initialized (or on after this example below).

+   - The thread assigned to do the I/O on behalf of the calling process uses the read(2) and write(2) system calls to enter the kernel.

Essentially, the thread-implementation of async I/O makes the I/O appear asynchronous to the calling process by creating a thread to do the I/O and allowing the caller to return to other work without waiting. The implementation uses the traditional synchronous Solaris system calls (pread(2) and write(2)) to do the I/O.

In either case (kaio or non-kaio), the underlying mechanics of doing the actual I/O are no different than if the I/O was initiated by a simple read(2) or write(2). Once the read or write has been completed, the result (error or success) is set in a data structure that was passed by the code that initiated the I/O, and a signal (SIGIO) is sent to the calling process to indicate that the I/O has completed or cannot be completed because of an error condition. It is up to the programmer to write a handler for the SIGIO signal and deal with the condition as required by the application.

Internal benchmarking and testing at Sun have that the implementation of kaio was truly a worthwhile effort. The reductions in overhead and dedi-