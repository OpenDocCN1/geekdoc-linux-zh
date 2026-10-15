It is useful to distinguish between public and private FIFOs. A public FIFO is one that is known to all clients. It is not that there is a specific function that makes a FIFO public; it is just that it is given a name that is easy to remember and that its location is advertised so that client programs know where to find it. Some authors call these well-known FIFOs, because they are analogous to well-known ports used for sockets, which are covered later. A private FIFO, in contrast, is given a name that is not known to anyone except the process that creates it and the processes to which it chooses to divulge it. In our first example, we will use only a single public FIFO. In the second example, the server will create a public FIFO and the clients will create private FIFOs that they will each use exclusively for communicating with the server.

# 8.4.2.1 Example

This is a simple example that demonstrates the basic principles. In it, the server creates a public FIFO and listens for incoming messages. When a message is received, it just prints it on the console. Client programs know the name of the FIFO because its pathname is hard-coded into a publicly available header file that they can include. In fact, for this example, the server and the clients share this common header file. Ideally the FIFO's name should be chosen so that no other processes in the system would ever choose the same file name, but for simplicity, we use a name that may not be unique.

The server will execute a loop of the form

```
while ( 1 ) {
    memset(buffer, 0, PIPE_BUF);
    if ( ( nbytes = read( publicfifo, buffer, PIPE_BUF)) > 0 ) {
        buffer[nbytes] = '\0';
        printf("Message %d received by server: %s", ++count, buffer);
        fflush(stdout);
    }
    else
        break;
}
```

In each iteration, it begins by zeroing the buffer into which it will copy the FIFO's contents. It reads at most PIPE_BUF bytes at a time into the buffer. When read() returns, if nbytes is positive, it null-terminates the buffer and writes what it received onto its controlling terminal. Because the input data may not have a terminating newline, it forces the write by calling fflush(stdout). If nbytes is negative, there was an error and the server quits. If nbytes is 0, it means that read() returned without any data, and so there is nothing for it to write. We could design the loop so that it does not exit in this case but just re-executes the read(), but there are reasons not to, as we now explain.

The server has to perform blocking reads (the O_NONBLOCK and O_NDELAY flags are clear), otherwise it would continually run in a loop, needlessly calling read() until a client actually wrote to the FIFO. This would be a waste of CPU cycles. By using a blocking read, it relinquishes the CPU so that it can be used for other purposes. The problem is that the read() call will return 0 when

3 There are programs that can generate unique keys of an extremely large size that can be used in the name of the file. If all applications cooperate and use this method, then all pipe names would be unique.