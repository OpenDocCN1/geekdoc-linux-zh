# Using TCP/IP Networking to Communicate with the Server

Opening a connection to the RPlay server is done by creating a *socket*, which is an endpoint for network communication. A socket is similar to a file descriptor in C; we conceptually open it, write to or read from it, and close it. In this sense, socket functions similar to a file, except the data comes from the network. This is similar in spirit to character special files, which look like files but which actually send and receive data to and from devices.

We create a socket with the *socket* system call, then call *connect* to connect the socket with the RPlay server at address 127.0.0.1 and port *5556*. The Internet address 127.0.0.1 is a special address which always represents the local host. After opening the socket, we can use the *send* function to send data to the socket. In our case, we don't need to worry about receiving data from the server, so we only need to write to the socket.

The data we write to the socket to control the RPlay server are simple ASCII strings. RPlay supports a number of commands; see the RPlay online documentation for a comprehensive list. The only command we are interested in for now is the command to play a sound file. The simplest form of this command looks as follows:

```
play count=1 volume=64 sound=crash.
```

The *count* parameter specifies how many times the specified sound should be played. The *volume* parameter specifies the volume, with 0 being the lowest and 255 being the highest. The *sound* parameter is the full path to the sound file to be played. The sound file must be accessible to the RPlay server, which is why it is advisable to specify a full path name. Alternatively, a path name relative to the directory in which the server was started may be specified. Yet another possibility would be to stream the actual sound data over the socket to the server.

The next sample program *playtest* creates a socket and connects it to the RPlay server. Run the program as follows. First, change to the program's source code directory \$13d/source/app/audio. Compile the program with *make*. Next, kill any previous running copies of the RPlay server: type *killall -9 rplay* and press *Enter*. Then, start the RPlay server from this directory: type *rplay* and press *Enter*. (We start the server in this directory to allow the sample program to specify just the filename of the desired file, without the full pathname.) Next, start the sample program: type *playtest* and press *Enter*. The program waits for you to press *Enter*; each time you do, a command is sent via a socket to the RPlay server to play the file *crash.au*, located in the same directory.

# Listing 8-2: *playtest.cc*

```
#include <sys/socket.h>
#include <sys/types.h>
#include <netdb.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <unistd.h>
#include <errno.h>
#include <stdio.h>

main() {
    int mysocket;
```