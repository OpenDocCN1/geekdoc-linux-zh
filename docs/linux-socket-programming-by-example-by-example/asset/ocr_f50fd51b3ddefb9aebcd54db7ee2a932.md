Include code to handle `EINTR` if any of the following applies to your situation:

+   - The source code might be ported to other UNIX platforms in addition to Linux.
+   - You are experiencing sporadic `EINTR` errors in your application (this is always a strong indication).
+   - The GNU C library has changed direction on its policy of hiding the `EINTR` error from the application.

If your application does not process signals, or it has established signals that are to be ignored, you might never need to be concerned about the `EINTR` error code.

# ## Handling `EINTR` for Other Functions

It should be noted at this point that `EINTR` is potentially a problem for a host of other functions that you might use for socket programming. The functions affected by signals include

+   connect(2)
+   accept(2)
+   read(2)
+   write(2)
+   readv(2)
+   write(2)
+   recvfrom(2)
+   sendto(2)
+   select(2)
+   poll(2)

The list presented is not meant to be an exhaustive list, and some of these functions have not been covered yet. It is a list of commonly used functions, however, which are affected by signal handling.

The examples that are shown in this text will largely ignore this issue of `EINTR`, in favor of keeping the example programs small and easier to understand. However, you must allow for the occurrence of `EINTR` for any production-level code.

> **CAUTION**
> Always test for the `EINTR` error when calling functions affected by signal handling in production-level code.

# ## Defining Buffer Operation

When you make use of the `stdio(3)` facilities, you generally make use of some buffering behind the scenes. Buffered writes, for example, reduce the frequency that the system function `write(2)` is called. This increases the overall system output efficiency. Likewise, read requests are also buffered.