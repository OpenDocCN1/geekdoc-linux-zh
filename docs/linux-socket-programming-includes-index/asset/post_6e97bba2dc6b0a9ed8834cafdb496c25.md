
The connection requires a specific format to define which computer and how to connect. The IP address likewise identifies the computer. Just as telephone numbers have a specific format, the connection requires a specific format to define which computer and how to connect.

- The connection provides the channel for messages. Once the telephone is answered, there is a channel through which two or more people may converse. Your telephone number is not important unless the person has to call you back.
- The path back to your handset is hidden inside the telephone system. The telephone network has several shared paths, like a computer network. So having a reverse path is important for getting the messages back to your handset. The destination peer or server gets the address and port of your program so that it can reply using a similar path.

Your telephone number has to be published for others to call you. If your program is going to accept calls, you must specify a unique channel (or port) and publish it to your clients.

The `connect()` system call's definition follows:

```c
#include <sys/socket.h>
#include <resolv.h>
int connect(int sd, struct sockaddr *server, int addr_len);
```

The first parameter (sd) is the socket descriptor that you created with the `socket()` call. The last parameter is the length of the `sockaddr` structure. The second parameter points to different types and sizes of structures. This is important, because this is what makes the `socket()` calls different from the file I/O calls.

Recall that the `socket()` system call supports at least two different domains (**PF_INET** and **PF_IPX**). Each network domain (**PF_* **) has its own structure to describe the address. They all have one common parent—the one you see in the `connect()` definition—**struct sockaddr**. For a complete list of all the structure declarations, see Appendix A.

## Sockaddr Data Abstraction

The **sockaddr** interface uses data abstraction. Data abstraction simplifies interfaces by asserting that while the data types may change, the algorithms remain the same. For example, a stack can contain different data types, but the function of the stack remains the same: push, pop, and so forth. To use an abstract interface, the first field of the **sockaddr** structure must have the same meaning. All structures have one common field: `..._family`. The field's type is an unsigned 16-bit integer. The value this field holds determines what kind of network domain to use.

## Matching the Socket Type with sockaddr Family Field

> The domain type you had set in the `socket()` system call must be the same value as the first field in the sockaddr family. For example, if your program created a PF_INET6 socket, the structure field must be AF_INET6 in order for the program to work correctly.

For now, here is the generic record and the INET record for comparison (from the header files):

```c
struct sockaddr {
    unsigned short int sa_family;
    unsigned char sa_data[14];
};
```

```c
struct sockaddr_in {
    sa_family_t sin_family;
    unsigned short int sin_port;
    struct in_addr sin_addr;
    unsigned char __pad[1];
};
```

Note that *sa_family* and *sin_family* are common between the two structures. The task every procedure call executes when it receives this record is to check the first field. Please notice that this is the only field that is in *host byte ordering* (See Chapter 2). The padding field (named *sa_data* and *__pad*) may be common for each in the sockaddr family. By convention, the generic *sockaddr* structure and the INET *sockaddr_in* structure have to be 16 bytes long (the IPv6 structure, *sockaddr_in6*, is 24 bytes). So, the padding field fills out with any unused bytes.

You may notice that the length of the padding field in *sockaddr_in* is missing. This is merely a convention. Since the padding has to be set to zero, the actual size is not important. (In the case of this *sockaddr_in* definition, it is 8 bytes wide.) Some implementations may define additional fields for internal computations. Don't worry about them—and don't use them, because you can't guarantee the field's availability from system to system and version to version. Any changes may break your code when you use nonstandard fields. In all cases, initializing the entire structure instance to zero is best.

The following table describes each field. It also gives examples of possible values.

| Field Name | Description | Byte Ordering | Example |
| :--- | :--- | :--- | :--- |
| *sin_family* | The protocol family | Host, Native | AF_ |
| *sin_port* | The server's port number | Network | 13 (time of day) |
| *sin_addr* | The server's numeric IP address | Network | 127.0.0.1 (localhost) |

Before calling the `connect()` system call, the program fills each field. Linux has masked the system call slightly, so it is not necessary to cast `sockaddr_in` to be a `sockaddr`. For portability, you may still want to follow conventions and add the casts.

## Casting `sockaddr` Types

With other UNIX-compatible OSs, you can cast any of the `sockaddr_*` family members to `sockaddr` to avoid warnings. The examples here don’t use any casting merely for space (and because Linux allows it).

The code may look like Listing 1.2.

### LISTING 1.2 `Connect()` Example

```c
/*** Code snippet showing initialization and calling of *** */
/*** the connect() system call. *** */

#define PORT_TIME     13
struct sockaddr_in dest;
char *host = "127.0.0.1";
int sd;
/*** Create the socket & do other work *****/

bzero(&dest, sizeof(dest));      /* start with a clean slate */
dest.sin_family = AF_INET;       /* select the desired network */
dest.sin_port = htons(PORT_TIME); /* select the port */
inet_aton(host, &dest.sin_addr);         /* remote address */

if ( connect(sd, &dest, sizeof(dest)) == 0 )  /* connect! */
{
        perror("Socket connection");
        abort();
}
...
```

The `connect()` system call in this code requires several preparatory steps before you connect the socket to the server. First, create a `sockaddr_in` structure. Use the server address for the second line. If you want to connect to a different server, place the appropriate IP address in this string. The program proceeds with other initializations, including the `socket()` system call. When you start working with the structure, zero it out with `bzero()`. The program sets the family to `AF_INET`. Next, the program sets the port and the IP address. The `htons()` and `inet_aton()` conversion tools used here are covered in Chapter 2.

The next call is the connection to the server. Please note that the code fragment checks the return values for every procedure call. That policy is one of many keys to making your network programs robust.

After the program establishes the connection, the socket descriptor, sd, becomes a read/write channel between the two programs. Most servers we are accustomed to offer single transactions and then hang up (for example, an HTTP 1.0 server sends the requested file, then closes the connection). To interface with these types of server, your program has to send the request, get the reply, and close the connection.

## Getting the Server's Reply

The socket is open and the channel is established. Now, you can get the first "hello." Some servers initiate the conversation like the person answering the phone. This message may include the server's name and some instructions for connection. Once your connection is open, you can use the standard library low-level I/O calls for communication. Here is the `read()` system call:

```c
#include <unistd.h>
ssize_t read(int fd, void *buf, size_t count);
```

You're probably familiar with this call. Other than its special capability to use the socket descriptor (sd) instead of the file descriptor (fd), everything else is almost the same as reading from a file. You can even use the `read()` system call as in the following code fragment:

```c
...
int sd, bytes_read;
sd = socket(PF_INET, SOCK_STREAM, 0);    /* create socket */

/**** Connect to host ****/

bytes_read = read(sd, buffer, MAXBUF);  /* read the message */
if ( bytes_read < 0 )
    /* report connection error; exit routine */
...
```
