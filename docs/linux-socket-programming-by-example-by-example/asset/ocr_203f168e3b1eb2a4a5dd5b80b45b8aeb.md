# # Applying FILE Streams to Sockets

Now it is time to introduce some source code that makes use of the concepts that have been discussed so far. The server program that will be presented next implements a Reverse Polish Notation (abbreviated RPN) calculator. It accepts arbitrarily long integer values, stacks them, and then permits operations to be performed upon the stacked numbers. The result of the operation is placed on the top of the stack.

The integer arithmetic will be performed by the GNU Multi-Precision (GMP) library. This library permits virtually unlimited sized integer numbers to be evaluated. Space does not permit the GMP library to be described here. The purpose of this code is simply to illustrate some server concepts using **FILE** streams. This same server will help illustrate some advanced topics that will be covered in the nextchapter.

# ## Presenting the mkaddr() Function

The **mkaddr.c** subroutine function will be presented here, to make this project easier to read. The **mkaddr()** function being presented, accepts an input string that consists of an IP number and an optional port number, or a hostname and optional port number. The port number can also be a symbolic Internet service name such as “telnet” or “ftp.” The function synopsis of the function is as follows:

```
int mkaddr(void *addr, int *addr_len, char *str_addr, char *protocol);
```

The function arguments can be described as follows:

+   1.  The argument *addr* points to the receiving socket address structure. This is the socket address, which is being returned. This value must not be null.
+   2.  The argument *addr_len* is a pointer to an integer value, which will be filled with the length of the address created in *addr* when the function returns. The input value that is pointed to must contain the maximum size in bytes of the area pointed to by *addr*.
+   3.  Argument *str_addr* is the symbolic hostname and optional port number (or service). This will be more fully described later. A null pointer implies a string value of “*”.
+   4.  The *protocol* argument specifies the protocol that this service will be using. A null pointer implies the protocol string “tcp”.

The *str_addr* input string is designed to be as flexible as possible. It contains two components, separated by a colon character:
host_name:service

![](bbox=[0.08, 0.58, 0.15, 0.68])