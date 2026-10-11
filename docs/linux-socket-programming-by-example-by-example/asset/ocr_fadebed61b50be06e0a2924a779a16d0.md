For example, `fgetc(3)` will fetch one character from a buffer. Only when the input buffer is empty will it request more data to be read in using the `read(2)` system call. This, again, is done to improve the I/O efficiency.

When the underlying file descriptor of a stream is a terminal device, the I/O under Linux will be line buffered. Files, on the other hand, are usually fully buffered (buffered in large blocks).

There are three basic modes of buffering to choose from using FILE streams under Linux. These are

+   - Fully buffered (or "block" buffered)
+   - Line buffered
+   - Unbuffered

Choosing "unbuffered" mode might be appropriate for some socket programs, although no efficiency from buffering can be gained this way. This does save you, however, from worrying about when to call `fflush(3)`.

# TIP

> If your network application is experiencing hangs, the cause might be output buffering. Change the buffering on your output streams to "unbuffered mode" for testing. If the problem vanishes, then you need some calls to `fflush(3)` added to the appropriate places. Alternatively, you could reconsider the buffering mode being used by the application.

Line buffered mode is often useful when your socket interaction is text line based. Using line buffered mode means that you are never forced to call upon `fflush(3)` to force the last text line to be written to the socket.

If you choose to use the "fully" buffered mode, then you must apply `fflush(3)` at the point where you want a physical write to take place to the socket. Otherwise, your data might sit in an output buffer, while your application waits in vain for a response, because the output data was never sent.

The function synopses of the buffer control functions are shown in Listing 10.3.

![](bbox=[0.06, 0.8, 0.15, 0.9])

```
Listing 10.3: Stream I/O Buffer Functions
```c
#include <stdio.h>

int setbuf(FILE *stream, char *buf);

int setbuffer(FILE *stream, char *buf, size_t size);

int setlinebuf(FILE *stream);

int setvbuf(FILE *stream, char *buf, int mode, size_t size);
```
```