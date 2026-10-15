# SUMMARY

We discussed a number of important topics, primarily related to UNIX IPC, between related processes on the same machine, using related or unrelated processes on the same machine and related or unrelated processes on the same or different machines on a network. In doing so, we covered the use of pipes, named pipes (FIFOs), and sockets as communication channels and the related data structures, system calls, macros, and library functions. These calls and data structures deal with the creation of a communication channel, preparing it for communication where required, and using it for reading and writing messages between processes.

We discussed the issue of client-server design in detail, both for connectionless and connection-oriented communication between client and server processes. Our focus in this regard was the transport-level protocols, UDP and TCP. We described the need for different types of servers, including iterative and concurrent servers.

We explained the working of the various types of client-server models by designing and implementing application-level services similar to the well-known Internet services ECHO, TIME, and DAYTIME. We also discussed the design and implementation of a concurrent server using slave processes. Throughout the chapter, our discussions included algorithms for the client and server processes, call graphs, and interaction sequences. The call graphs describe the sequence of system calls for implementing client and server software individually, and interaction sequences describe the interaction between the client and server processes to implement the application protocol at hand.

We then covered the design of servers that offers multiple services using the select() system call. We built a simple concurrent server using the select() system call to implement the TIME and ECHO services for the UDP protocol. We also described how the UNIX superserver, inetd, works. Finally, we discussed the need for concurrent clients and how they work.

# QUESTIONS AND PROBLEMS

+   1. What are little endian and big endian byte orders? Are these for data storage, data transmission, or both? What is network byte order? Give one example each of the processors that use these byte orders.

+   2. Show the contents of memory locations for the 32-bit hex number F9327CA5 using the little endian and big endian byte orders. Assume that the main memory is byte oriented.

+   3. What byte orders are used by the following CPUs: AMD64, Intel i7, Sun SPARC, Motorola 68000, IBM, PDP, and VAX? How did you obtain your answers?