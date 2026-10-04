# 3.4 Input/Output in Tcl

```
# read the output of the ls command:
while {![eof $pipe]} {
    set length [gets $pipe lsLine]
    puts "$lsLine"
}
```

# Script Output

Gets returned 14 characters in the string: This is line 1
Read: This is line 2
This is line 3

# Opening a Pipe

```
bin
boot
bsd
dev
```

###. Client Sockets
The socket command returns a channel for use with socket-based I/O.
The socket command can return a client or server socket.

Using the socket command to establish a client socket is as straightforward as opening a file. Server sockets and event-driven code are discussed in the bonus book on the CD-ROM. See the chapter about controlling a National Instruments I/O card.

The first example in Chapter 4 will show how the socket and flush commands can be used.

```
Syntax: socket ?options? host port
```

+   * socket Open a socket connection.
* options? Options to specify the behavior of the socket.
* -myaddr Defines the address (as a name or number) of the client side of the socket. This is not necessary if the client machine has only one network interface.