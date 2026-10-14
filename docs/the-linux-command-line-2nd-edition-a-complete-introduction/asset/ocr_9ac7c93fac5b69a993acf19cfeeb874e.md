```
Parent: launching child script...
Parent: child (PID= 6741) launched.
Parent: continuing...
Child: child is running...
Parent: pausing to wait for child to finish...
Child: child is done. Exiting.
Parent: child is finished. Continuing...
Parent: parent is done. Exiting.
```

# Named Pipes

In most Unix-like systems, it is possible to create a special type of file called a named pipe. Named pipes are used to create a connection between two processes and can be used just like other types of files. They are not that popular, but they’re good to know about.

There is a common programming architecture called client-server, which can make use of a communication method such as named pipes, as well as other kinds of interprocess communication such as network connections.

The most widely used type of client-server system is, of course, a web browser communicating with a web server. The web browser acts as the client, making requests to the server and the server responds to the browser with web pages.

Named pipes behave like files, but actually form first-in first-out (FIFO) buffers. As with ordinary (unnamed) pipes, data goes in one end and emerges out the other. With named pipes, it is possible to set up something like this:

```
process1 > named_pipe
```

and

```
process2 < named_pipe
```

and it will behave as if:

```
process1 | process2
```

# Setting Up A Named Pipe

First, we must create a named pipe. This is done using the mkfifo command:

```
[me@linuxbox ~]$ mkfifo pipe1
[me@linuxbox ~]$ ls -l pipe1
prw-r--r-- 1 me me 0 2009-07-17 06:41 pipe1
```