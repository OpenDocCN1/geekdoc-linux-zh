
Although limited, you can see that Listing 10.6 is a simple server loop that keeps accepting client connections in single-file fashion. Later, you’ll learn how to write a higher-performance server that can concurrently process several clients at one time.

### Trying Out the RPN Server

To compile all the related source modules for the RPN server, you can perform the following make command:

```
$ make rpngrv

gcc -c -D_GNU_SOURCE -Wall -Wreturn-type rpngrv.c
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type rnpeng.c
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type mkaddr.c
gcc rpngrv.o rnpeng.o mkaddr.o -o rpngrv -lgmp
$ 
```

After the executable rpngrv for the server has been created, you can start the server as follows:

```
$ ./rpngrv &
[1] 13321
$ 
```

In the output shown, the server was started with a process ID of 13321, and run in the background.

To keep things simple at this point, you’ll just use the telnet command to try out the server. The next chapter will fully outline this server’s functions. For now, just try some simple tests.

> The server presented is not a production-grade server. Some forms of incorrect input can provoke the server to abort.

The RPN calculator computes based upon numbers that are pushed onto the stack. To perform the add operation, for example, requires at least two numbers to exist on the stack. To push a number onto the stack, you will enter a line as follows:

```
#:970976453
```

After you press Enter, the server will respond with something like this: 0:

This tells you that the number has been stacked at the bottom of the stack (entry number zero). To stack another number, simply do the same, as follows:

```
#:2636364
```

The server will respond with 1:

This indicates that the number 2636364 was stacked at position 1, although the original number 970976453 still sits at the bottom of the stack at position 0. You can list the current contents of the stack by entering the following: `dump`

The following example shows what the session and its output might look like this:

```
$ telnet localhost 9990  
Trying 127.0.0.1...  
Connected to localhost.  
Escape character is '^]'.  
#:970976453  
0:  
#:2636364  
1:  
dump  
1:2636364  
0:970976453  
E:end of stack dump
```

To perform a binary operation, you simply enter the name of the operation or its symbol. For example, to add these numbers, you would just enter the + character and press return. The session repeated without entering the dump command would appear as follows if the + operation was performed, and then followed by the = operation:

```
$ telnet localhost 9990  
Trying 127.0.0.1...  
Connected to localhost.  
Escape character is '^]'.  
#:970976453  
0:  
#:2636364  
1:  
+  
0:  
=  
0:973612817  
^]  
telnet> c  
Connection closed.  
$
```

The `+` operation caused the two stacked numbers to be added together, and the result replaced the two original values. The `=` operator here pops the result off the stack and displays it for you.

To exit the server, type `CTRL+J` and you will be prompted with the prompt: `telnet>`

From there, enter a `c` to indicate that you want the session closed, and press Enter. To terminate the server, just use the `kill` command.

Take a few minutes now to have some fun with the new RPN calculating server program. Restart the server, and see whether you can figure out how to compute the equation $(3 + 2) * (2 + 4)$ using the calculating server just presented.

After your experiment, you deserve a break. The server will be more fully explored in the next chapter as you look at more advanced server issues. For now, just take stock of the concepts you have mastered in this chapter.

### What’s Next

This chapter has introduced you to the idea of using FILE streams with your sockets. You can readily appreciate how streams will make certain tasks much simpler for your code, such as the input and output of text lines.

You also learned to be aware of the `EINTR` problem if the `glibc` library should change or if your code is ported to another UNIX platform.

The next chapter will teach you how servers can service multiple client connections at the same time. This is not as trivial as you might imagine.

## Concurrent Client Servers

All of the servers presented in this text so far have processed one client's request in total before accepting a connection to the next client. This design is effective and simple for servers that reply swiftly. However, if the processing takes a long time, or there are periods of inactivity, then this will prevent other clients from being serviced without lengthy delays. Because servers are usually required to service as many clients as possible, with a minimum of delay, a fundamental design change is needed at the server end of the connection.

In this chapter you will learn how to use the following:

- The fork(2) function in order to handle multiple client connections
- The wait(2) and waitpid(2) functions
- The select(2) function for handling multiple client connections

Mastering these concepts will permit you to write professional-grade servers, which can service large numbers of clients at once.

### Understanding the Multiple-Client Problem

Figure 11.1 shows several clients, which have contacted one server. The client connections conceptually form spokes around the central server.

![](img/961a0296fe36074690a9847b79332eff_287_0.png)

Figure 11.1: Several clients attached to one server can be graphically represented as spokes attached to a hub.

The server, acting as the central hub in Figure 11.1, must balance its resources among several connected clients. The server is normally designed to behave such that each client thinks that it has dedicated server access. In reality, however, the server services all clients in a concurrent manner.

There are a few ways of achieving this. They are:

- Forked server processes (multi-process method)
- Threaded server processes (multi-thread method)
- One process and a select(2) call
- One process and a poll(2) call

The first method of using the fork(2) system call is perhaps the simplest way to service multiple-client processes. However, it suffers from the disadvantage that sharing information becomes more complex. This usually requires the use of message queues, shared memory, and semaphores. It also suffers from the disadvantage that it requires more CPU to start and manage a new process for each request.

The threaded server method is relatively new to UNIX, and is now a viable option for Linux. Kernel versions 2.0.0 and later support threads, provided that the appropriate thread-safe libraries are used. Threads offer the light-weight advantages of the multi-process method, without hampering centralized communication. Threaded processes can be very difficult to debug, however, especially for beginning programmers. For this reason, threads will not be explored in this text.

> **TIP**
>
> Frequently Asked Question (FAQ) documents that describe threads in more detail under Linux are available on the Internet for your viewing. Some references to these are:
>
> http://metalab.unc.edu/pub/Linux/docs/faqs/Threads-FAQ.html
>
> http://linas.org/linux/threads-faq.html
>
> http://pauliillac.inria.fr/~xleroy/linuxthreads
>
> http://www.globenet.it/~ermmau/Threads

The last two methods listed involve the use of the select(2) or poll(2) function calls. Each of these functions offers a different way to block execution of the server until an event occurs. The select(2) function will be examined in detail within this chapter. The interested reader is encouraged to read the man pages for poll(2) after completing this chapter.

### Overview of Server Functions

Chapter 10, “Using Standard I/O on Sockets,” introduced the Reverse Polish Notation (RPN) calculating server. Only its most primitive functions were described, however. Before you dive into the server’s design aspects in this chapter, you should get to know some of the server’s capabilities first. In this manner, you’ll be able to give the server a better workout.

The most basic functions are listed in Table 11.1. These describe the most rudimentary arithmetic and operator functions available.

**Table 11.1: The Rudimentary RPN Server Functions**

| Function | Argument | Description |
| :------- | :------- | :---------- |
| #        | Integer  | An integer value to push onto the stack. |
| +        | N/A      | Add the two numbers on the top of the stack. The numeric resulting number replaces these two values on the top of the stack. |
| -        | N/A      | Subtract the top number from the next to last number on the stack. The result replaces the two values on the top of the stack. |
| *        | N/A      | Multiply the two numbers on the top of the stack. The resulting value replaces the two numbers on the top of the stack. |
