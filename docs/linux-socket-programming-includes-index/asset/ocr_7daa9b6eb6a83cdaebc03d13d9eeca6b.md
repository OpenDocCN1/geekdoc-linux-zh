![](bbox=[0.1, 0.11, 0.44, 0.28])

# Asynchronous Writes

You program the asynchronous write a bit differently because of the kernel’s buffers. When your program first calls send(), it’s likely that the kernel’s buffers can store the entire data block. But it’s also possible that it can’t, and the kernel caches only a part.

So, check the return value of every write() to make sure that all the data gets sent. It may even be essential for you to keep all outgoing data for a channel in a single queue. This reduces the code complexity involved with multiple buffers. Still, making the buffering flexible is important as well, so that the queue may grow and shrink as needed.

A database query example serves well in this situation. It generates lots of data that can be processed or gathered while sending the reply, as shown in Listing 8.5.

LISTING 8.5 Asynchronous Writer Algorithm

```
/***** Database Query Async Writer Example: process query `***/
/** while generating results. `*/
/*******...*******/
int ready=0, bytes, size=0, pos=0;
...
int sig_io(int sig)
{
    if ( size > 0 )
    {
        bytes = send(client, buffer, size+pos, 0);
        if ( bytes > 0 )
        {
            pos += bytes;
            ready = 1;
        }
    }
}
...
```