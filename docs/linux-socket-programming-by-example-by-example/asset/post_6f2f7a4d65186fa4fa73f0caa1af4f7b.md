
The address argument must be a pointer to the address structure. You will note that the *generic address type used* is the *sockaddr* structure type. This means that you will need to apply a C language cast operator to satisfy the compiler that you have passed the correct pointer type. Listing 5.1 shows a program that calls up `bind(2)` to establish an Internet address. Note the use of the `inet_aton(3)` and `bind(2)` function calls.

![](img/961a0296fe36074690a9847b79332eff_134_0.png)

```c
/* af_inet.c: */
/* Demonstrating the bind(2) function
 * by establishing a Specific AF_INET
 * Socket Address:
 */

#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <errno.h>
#include <string.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

/*
 * This function reports the error and
 * exits back to the Shell:
 */
static void
bail(const char *on_what) {
    perror(on_what);
    exit(1);
}

int
main(int argc, char **argv, char **envp) {
    int z;                    /* Status return code */
    int sck_inet;             /* Socket */
    struct sockaddr_in adr_inet;/* AF_INET */
    int len_inet;             /* Length */

    /* Create an IPv4 Internet Socket */
    sck_inet = socket(AF_INET, SOCK_STREAM, 0);

    if ( sck_inet == -1 )
        bail("socket()");

    /* Create an AF_INET address */
    memset(&adr_inet, 0, sizeof adr_inet);

    adr_inet.sin_family = AF_INET;
    adr_inet.sin_port = htons(9000);
    inet_aton("127.0.0.24", &adr_inet.sin_addr);

    len_inet = sizeof adr_inet;

    /* Now bind the address to the socket */
    z = bind(sck_inet,
             (struct sockaddr *)&adr_inet,
             len_inet);

    if ( z == -1 )
        bail("bind()");

    /* Display all of our bound sockets */
    system("netstat -pa -tcp 2>/dev/null | "
           "sed -n '/1:'/Proto/p;/bind/p'");

    close(sck_inet);
    return 0;
}
```

> **NOTE**
> If the `netstat(1)` command on your system does not support the options used in lines 60 and 61 of Listing 5.1, substitute the following call if you have the `lsof` command installed:
>
> `system("lsof -i tcp | sed -n '/lp:/bind/p'");`

The program in Listing 5.1 is much like the ones you saw in Chapter 2. The steps used in the program are:

- 1. Variable `sck_inet` will receive the socket when it is created (line 31).
- 2. Variable `adr_inet` will hold the socket's address that will be bound to it (line 32).
- 3. Variable `len_inet` will hold the length of the socket address in bytes (line 33).
- 4. The socket is created by `socket(2)` in line 36.
- 5. Step 4 is checked for errors in lines 38 and 39. If an error is detected, the function `bail()` is called. `bail()` reports the error and exits the program.
- 6. Lines 42 to 47 initialize the new socket address that is to be bound to the socket.
- 7. Variable `len_inet` is set to the size of the socket address (line 49).
- 8. The `bind(2)` function is called in lines 52 to 54. The value `sck_inet` represents the socket that is to be bound to the socket address `adr_inet`. This address is of length `len_inet` bytes. Note the use of the cast operator `(struct sockaddr *)` which is used to satisfy the compiler. This prevents a warning from being reported at compile time.
- 9. Step 8 is checked for errors in line 56. If an error occurs, `bind(2)` returns the value -1 instead of zero.
- 10. The `system(3)` call invokes the `netstat(1)` command to prove that our socket has an address bound to it (lines 60 and 61).

The following output shows how to compile and run this program:

![](img/961a0296fe36074690a9847b79332eff_136_0.png)

The output shows that when it was run, the address 127.0.0.24:9000 was bound to the socket. The 9000 part represents the arbitrary port number that was chosen for this example program.

If you ran the program using the `lsof` command instead (see prior note), the output will appear slightly different:

```
$ ./bind
COMMAND PID USER FD TYPE DEVICE SIZE NODE NAME
bind 16616 root 4u inet 142319 TCP 127.0.0.24:9000 (CLOSE)
$
```

From this output, you can verify that the program named `bind` (under the heading “COMMAND”) had a socket open on file unit 4 (column “FD”), and was bound to the TCP address 127.0.0.24, port 9000.

## Obtaining the Socket Address

If a C library function that you wrote receives a socket as an input argument, then you will not know what the socket address of that socket is. This is because your function did not create the socket; and, unless the socket address is also passed to your function as input, you will not know what the address is. The function `getsockname(2)` permits your function to obtain it.

The function synopsis for `getsockname(2)` is as follows:

```c
#include <sys/socket.h>

int getsockname(int s, struct sockaddr *name, socklen_t *namelen)
```

This function takes the following three input arguments:

- 1. The socket `s` to query for the socket address.
- 2. The pointer to the receiving buffer (argument `name`).
- 3. Pointer to the maximum length variable. This variable provides the maximum length in bytes that can be received in the buffer (argument `namelen`). This value is updated with the actual number of bytes written to the receiving buffer.

Note that like the `bind(2)` function, `getsockname(2)` uses the generic address structure `sockaddr_t` because it can be used for any type of socket address. This will mean that you will likely need to apply the C language casting operator on the pointer supplied in this argument.

The length argument `namelen` specifies the maximum number of bytes that can be received into argument two (`name`). Prior to returning to the caller, however, the value of `namelen` is overwritten to indicate how many bytes were actually returned in the receiving buffer. This will be less than or equal to the original value supplied.

> **CAUTION**
>
> Never supply the address of a constant for the socket address length in a call to `getsockname(2)`. This should not be done because the length variable is updated with the actual number of bytes placed into the receiving address structure.
>
> If you do supply the address of a constant, the value of the constant will be overwritten. This will cause havoc in your program. On some CPU platforms, you might experience a program fault instead.

The function returns zero if it is successful. If an error occurs, the return value -1 is returned, and the reason for the error is posted to the variable `errno`.

## Writing a `sock_addr()` Function

To illustrate the use of `getsockname(2)`, a small function has been presented in Listing 5.2, which accepts as input a socket descriptor. The function obtains the socket's address by calling `getsockname(2)`, and then formats a string to be returned to the caller which can be used in a `printf(3)` call.

![](img/961a0296fe36074690a9847b79332eff_138_0.png)

```c
Listing 5.2: sckname.c — The getsockname(2) Function Call
/* sckname.c:
 *
 * Demonstrate getsockname(2):
 */
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <errno.h>
#include <string.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

/*
 * This saves lines of code later:
 */
static void
bail(const char *on_what) {
    perror(on_what);  /* Report error */
    exit(1);          /* Exit Program */
}

/*
 * This function accepts as input a socket
 * for which a socket address must be
 * determined for it. Then the address
 * is converted into a string and returned.
 *
 * If an error occurs, NULL is returned.
 */
char *
sock_addr(int s, char *buf, size_t bufsiz) {
    int z;            /* Status return code */
    struct sockaddr_in addr_in; /* AF_INET */
    int len_inet;    /* length */

    /*
     * Obtain the address of the socket:
     */
    len_inet = sizeof adr_inet;

    z = getsockname(s,
        (struct sockaddr *)&adr_inet,
        &len_inet);

    if ( z == -1 )
        return NULL;    /* Failed */

    /*
     * Convert address into a string
     * form that can be displayed:
     */
    snprintf(buf, bufsiz,
        "%s:%u",
        inet_ntoa(adr_inet.sin_addr),
        (unsigned)ntohs(adr_inet.sin_port));

    return buf;
}

/*
 * Main Program:
 */
int
main(int argc, char **argv, char **envp) {
    int z;            /* Status return code */
    int sck_inet;    /* Socket */
    struct sockaddr_in adr_inet;/* AF_INET */
    int len_inet;    /* length */
    char buf[64];    /* Work buffer */

    /*
     * Create an IPv4 Internet Socket:
     */
    sck_inet = socket(AF_INET, SOCK_STREAM, 0);

    if ( sck_inet == -1 )
        bail("socket()" );

    /*
     * Create an AF_INET address:
     */
```
