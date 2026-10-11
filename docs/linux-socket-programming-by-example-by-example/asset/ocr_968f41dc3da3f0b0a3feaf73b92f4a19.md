![](bbox=[0.19, 0.1, 0.7, 0.18])

> Figure 1.2: Without the telephone network, each endpoint of a telephone line is nothing more than a plastic box.

A socket under Linux, is quite similar to a telephone. Sockets represent endpoints in a line of communication. In between the endpoints exists the data communications network.

Sockets are like telephones in another way. For you to telephone someone, you dial the telephone number of the party you want to contact. Sockets have network addresses instead of telephone numbers. By indicating the address of the remote socket, your program can establish a line of communication between your local socket and that remote endpoint. Socket addresses are discussed in Chapter 2, “Domains and Address Families.”

You can conclude then, that a socket is merely an endpoint in communication. There are a number of Linux function calls that operate on sockets, and you learn about all of them in this book.

# ### Using Sockets

You might think that Linux sockets are treated specially, because you’ve already learned that sockets have a collection of specific functions that operate on them. Although it is true that sockets have some special qualities, they are very similar to file descriptors that you should already be familiar with.

> NOTE
> 
> Any reference to a function name like pipe(2) means that you should have online documentation (man pages) on your Linux system for that function. For information about pipe(2), for example, you can enter the command:
> 
> $ man 2 pipe
> 
> where the 2 represents the manual section number, and the function name can be used as the name of the manual page. Although the section number is often optional, there are many cases where you must specify it in order to obtain the correct information.

For example, when you open a file using the Linux open(2) call, you are returned a file descriptor if the open(2) function is successful. After you have this file descriptor, your program uses it to read(2), write(2), lseek(2), and close(2) the specific file that was opened. Similarly, a socket, when it is created, is just like a file descriptor. You can use the same file I/O