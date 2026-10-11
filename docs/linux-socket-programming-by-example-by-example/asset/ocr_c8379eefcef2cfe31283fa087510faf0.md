# ### Using Out-of-Band Data

Although you probably still have many questions about out-of-band data, fret not. Some simple example programs will help illustrate the concepts more clearly than a lot of text. An explanation will be provided as you progress through the demonstrations.

A few more basics about out-of-band I/O must be covered in the next short sections. After that is out of the way, the fun begins.

# ### Writing Out-of-Band Data

A call to write(2) will simply write the normal “in-band” data that you are already accustomed to doing. Consequently, a new function must be used to write out-of-band data. The send(2) function’s prototype is shown here for this purpose:

```
#include <sys/types.h>
#include <sys/socket.h>

int send(int s, const void *msg, int len, unsigned int flags);
```

This function requires four arguments, which are

+   1. The socket s to write to.
+   2. The message buffer msg to write from.
+   3. The length (len) of the message.
+   4. Sending option flags.

The send(2) function is like the write(2) call except that it has the additional flags argument provided. This is the essential ingredient. The send(2) function returns the number of characters written or −1 if an error occurred (check errno for the cause of the error).

To send out-of-band data, you use the first three arguments as you would in a call to write(2). If you supply the C language macro MSG_OOB for the flags argument, the data is sent as out-of-band data instead of the normal “in-band” data, as follows:

![](bbox=[0.06, 0.84, 0.14, 0.95])

```
char buf[64]; /* Data */
int len; /* Bytes */
int s; /* Socket */
... 
send(s, buf, len, MSG_OOB);
```

If the flags argument is supplied without the MSG_OOB flag bit, then the data is written as normal in-band data. This allows you to write both in-band and out-of-band data with the same function call. You simply change the flags argument value under program control to accomplish this.