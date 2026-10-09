Note that the `read` table is much simpler than the `write` table, because there’s never a guarantee of atomicity or of a complete read. `reads` work like this:

+   - If all writing file descriptors are closed, a `read` on an empty pipe always immediately returns 0, which most programs treat as an end-of-file.
+   - If a writing file descriptor is open, a `read` on an empty pipe blocks or not depending on whether `O_NONBLOCK` is set.
+   - A `read` on a nonempty pipe always returns immediately, no matter what the relationship between the requested amount and the amount of data in the pipe. The amount actually read is returned.
+   - Because there is no guarantee of atomicity, you must never allow multiple readers unless you have another concurrency-control mechanism (e.g., an interprocess semaphore) to prevent simultaneous reading. (In practice, you will seldom do this—you’ll use something like message queues instead.)

Here are additional guidelines to keep in mind:

+   - If you have one writer and one reader (e.g., a shell pipeline) and the reader is prepared for partial reads (e.g., uses Standard C I/O functions), write whatever amount you like, although multiples of the block size are most efficient, as we saw in Section 2.12.
+   - If you have multiple writers (and one reader), always write `PIPE_BUF` or less. There’s no practical way to get pipes to work correctly with a greater amount, unless you use another synchronization mechanism, such as a semaphore (Section 7.8).
+   - Don’t assume anything about the value of `PIPE_BUF` other than that it is at least 512. If you really need to know what it is, use `fpathconf`.
+   - Even though the standard doesn’t require atomic reads, essentially all implementations make them atomic if the requested amount is `PIPE_BUF` or less. Use this fact at your own risk.
+   - Remember that to get an end-of-file (0 return from `read`) all writing file descriptors must be closed, including any in the process that’s doing the reading. This point will be clearer later on, when we show how to connect two processes with a pipe.

# 6.2.3 Pipe Examples

(Now I’m talking once again only about *unnamed* pipes; FIFO examples are in the next chapter.)