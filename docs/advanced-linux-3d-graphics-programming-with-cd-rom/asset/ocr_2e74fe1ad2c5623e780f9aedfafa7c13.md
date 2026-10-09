server. The server's response to your input is then displayed. This continues indefinitely. This model of communication is quite general: any information is sent to the server; the server does something with the information; and then the server returns some other information. This program is very similar to the RPlay client we saw earlier. The only real change is that it displays the server's responses to our messages. Let's now discuss the program structure in a bit more detail.

The address of the server is specified in a C structure of type `sockaddr_in`, where the `in` stands for Internet. We set the `sin_family` of this address structure to be `AF_INET`, the address family for Internet addresses. The `sin_port` member of the address structure specifies the port number to connect to. We must specify the port number using function `htons`, which changes the byte ordering of the specified number from host to network order, explaining the "h" and the "n" in `htons`; the "s" denotes the data type, a short integer. The `sin_addr` member of the address structure contains the actual Internet address of the machine to connect to. We set this member using the `inet_aton` function, which converts an IP address in dotted quad notation (such as 127.0.0.1) to binary data in network byte order.

We then create a socket with the function call `socket`, specifying the following parameters: `PF_INET` to specify the Internet Protocol family, `SOCK_STREAM` to specify a sequenced and reliable connection stream (as opposed to unreliable or non-sequenced messages such as ping requests), and `getprotobyname("IP")` to specify the Internet Protocol for communication over the socket.

The `connect` function then connects the given Internet socket with the Internet address and port we previously stored in the address structure. The `send` and `recv` functions send or receive data from the socket, using a buffer to facilitate the transfer of data. These functions normally return the number of characters processed. If we notice that the number of characters processed at any stage is zero or negative, then some error occurred, and we shut down the socket with `shutdown`.

# Listing 8-6: client.cc

```
```
#include <sys/socket.h>
#include <sys/types.h>
#include <netdb.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <unistd.h>
#include <errno.h>
#include <stdio.h>
#include <sys/time.h>

main() {
int mysocket;

struct sockaddr_in addr;
struct sockaddr_in bounaddr;

addr.sin_family = AF_INET;
addr.sin_port = htons(5559);
inet_aton("127.0.0.1", &addr.sin_addr);
mysocket = socket(PF_INET, SOCK_STREAM, getprotobyname("IP"))->p_proto);
if(connect(mysocket, (sockaddr *)&addr, sizeof(addr))) {
```

```