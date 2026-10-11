
## Listing 2.3: continued

```c
47: /*
48:     unlink(pth_unix);
49:
50:     /*
51:      * Form an AF_UNIX Address:
52:      */
53: memset(&adr_unix,0,sizeof adr_unix);
54:
55:     adr_unix.sun_family = AF_UNIX;
56:
57:     strncpy(adr_unix.sun_path,pth_unix,
58:             sizeof adr_unix.sun_path-1)
59:     [sizeof adr_unix.sun_path-1] = 0;
60:
61:     len_unix = SUN_LEN(&adr_unix);
62:
63:     /*
64:      * Now bind the address to the socket:
65:      */
66:     z = bind(sock_unix,
67:         (struct sockaddr *)&adr_unix,
68:         len_unix);
69:
70:     if ( z == -1 )
71:         bail("bind");
72:
73:     /*
74:      * Display all of our bound sockets:
75:      */
76:     system("netstat -pa -unix 2>/dev/null | "
77:            "sed -n '/Active UNIX,/Proto/p | "
78:            "/af_unix/p/");
79:
80:     /*
81:      * Close and unlink our socket path:
82:      */
83:     close(sock_unix);
84:     unlink(pth_unix);
85:
86:     return 0;
87: }
```

The steps used in Listing 2.3 are as follows:

- 1. Variable `sock_unix` is defined in line 28 to hold the file descriptor for the created socket.
- 2. The local address structure is defined in line 29 and named `adr_unix`. The program will populate this structure with an `AF_LOCAL` socket address.
- 3. A socket is created in line 37 by calling upon the function `socket(2)`. Errors are tested in line 39 and reported if necessary.
- 4. The `unlink(2)` function is called in line 48. Because the `AF_UNIX` address results in a file system object being created, it must be removed when it is no longer required. This statement attempts to remove it, in case it was not removed the last time this program was run.
- 5. The address structure `adr_unix` is cleared to zero bytes in line 53.
- 6. The address family is initialized as `AF_UNIX` in line 55.
- 7. Lines 57 to 59 copy the pathname "/tmp/my_sock" into the address structure. The code used here, also places a null byte into the structure, because a Linux-provided macro `SUN_LEN( )` in line 61 needs it.
- 8. The length of the address is computed in line 61. The program presented uses the Linux-provided macro for this. The macro depends upon a null-terminated string being present in the `adr_unix.sun_path[ ]` structure member, however.
- 9. The function `bind(2)` is called (lines 66 to 68) to assign the address that was formed to the socket that was created in line 37.
- 10. The `netstat(1)` command is invoked in line 76 to prove that our address was bound to our socket.
- 11. The socket is closed in line 83.
- 12. The UNIX pathname created for the socket when `bind(2)` was called in line 66 is removed (`unlinked`).

The length that is assigned to `len_unix` in line 61, using the `SUN_LEN()` macro, does not count the null byte that was copied into the `adr_unix.sun_path[ ]` character array. However, it was necessary to place the null byte there, because the `SUN_LEN( )` macro calls upon `strlen(3)` to compute the string length of the UNIX pathname.

To compile and run the program, you can take advantage of the supplied Makefile. Perform the following:

```bash
$ make af_unix
gcc -c -D_GNU_SOURCE -Wall af_unix.c
gcc af_unix.o -o af_unix
$
```

After the program has been compiled, you can simply invoke it as follows without any arguments:

```bash
$ ./af_unix
```

Listing 2.4 shows a modified view of the output you would receive from running the command.

![](img/961a0296fe36074690a9847b79332eff_61_0.png)

## Listing 2.4: The Output from the af_unix Demonstration Program

```bash
$ ./af_unix
Active UNIX domain sockets (servers and established)
Proto RefCnt Flags Type State I-Node PID/Program name Path
unix 0 [ ] STREAM 104129 000/af_unix /tmp/my_sock
$
```

Listing 2.4 shows that there was a unix socket created, of type STREAM (SOCK_STREAM), and that af_unix was the name of the program that created it. At the right end of the line, you will see that indeed the socket name was /tmp/my_sock as it was expected to be.

## Forming Abstract Local Addresses

One of the annoyances of the traditional AF_UNIX socket name was that a file system object was always involved. This was often unnecessary and inconvenient. If the original file system object was not removed and the same name was used in a call to bind(2), the name assignment would fail.

Linux kernel version 2.2 has made it possible to create an abstract name for a local socket. The trick to this is to make the first byte of the pathname a null byte. Only the bytes that follow that first null byte in the pathname then become part of the abstract name.

![](img/961a0296fe36074690a9847b79332eff_61_1.png)

The example in Listing 2.5 shows a modified version of the last program. This program takes some different steps to create the abstract name.

## Listing 2.5: af_unix2.c—Program Creating an Abstract Named AF_LOCAL/AF_UNIX Socket

```c
1: /* af_unix2.c:
2: *
3: * AF_UNIX Socket Example:
4: */
5:
6: #include <stdio.h>
7: #include <unistd.h>
8: #include <stdlib.h>
9: #include <errno.h>
10: #include <string.h>
11: #include <sys/types.h>
12: #include <sys/stat.h>
13: #include <sys/socket.h>
14: #include <sys/un.h>
15:
16:   /*
17:    * This function reports the error and
18:    * exits back to the shell:
19:    */
20:   static void
21:   bail(const char *on_what) {
22:      perror(on_what);
23:      exit(1);
24:   }
25:
26:   int
27:   main(int argc,char **argv,char **envp) {
28:      int z;             /* Status return code */
29:      int sock_unix;    /* Socket  */
30:      struct sockaddr_un adr_unix;/* AF_UNIX */
31:      int len_unix;     /* Length */
32:      const char pth_unix[]       /* Abs. Name */
33:         = "Z*MY-SOCKET";
34:
35:      /*
36:       * Create an AF_UNIX (aka AF_LOCAL) socket:
37:       */
38:      sock_unix = socket(AF_UNIX,SOCK_STREAM,0);
39:
40:      if ( sock_unix == -1 )
41:         bail("socket()");
42:
43:      /*
44:       * Form an AF_UNIX Address:
45:       */
46:      memset(&adr_unix,0,sizeof adr_unix);
47:
48:      adr_unix.sun_family = AF_UNIX;
49:
50:      strncpy(adr_unix.sun_path,PTH_UNIX,
51:             sizeof adr_unix.sun_path-1)
52:             [sizeof adr_unix.sun_path-1] = 0;
53:
54:      len_unix = SUN_LEN(&adr_unix);
55:
56:      /* Now make first byte null */
57:      adr_unix.sun_path[0] = 0;
58:
59:      /*
60:       * Now bind the address to the socket:
61:       */
62:      z = bind(sock_unix,
63:          (struct sockaddr *)&adr_unix,
64:          len_unix);
65:
66:      if ( z == -1 )
67:         bail("bind()");
68:
69:      /*
70:       * Display all of our bound sockets:
71:       */
72:      system("netstat -pa -unix 2>/dev/null | "
73:             "sed -n '/Active UNIX,/Proto/p | "
74:             "/af_unix/p/");
75:
76:      /*
77:       * Close and unlink our socket path:
78:       */
79:      close(sock_unix);
80:      return 0;
81:   }
```

To make and run the program in Listing 2.5, perform the following commands:

```bash
$ make af_unix2
gcc -c -D_GNU_SOURCE -Wall af_unix2.c
gcc af_unix2.o -o af_unix2
$ ./af_unix2
```

The output from the running the program is shown in Listing 2.6.

### Listing 2.6: Output of the af_unix2 Example Program

```bash
$ ./af_unix2
Active UNIX domain sockets (servers and established)
Proto RefCnt Flags   Type    State   I-Node PID/Program name Path
unix  0   STREAM  104143 5186/af_unix2     @*MY-SOCKET*
$
```

From Listing 2.6, you can see the socket address appears as the name @*MY-SOCKET*. The leading @ sign is used by netstat(1) to indicate abstract UNIX socket names. The remaining characters are the ones that were copied into the rest of the character array. Notice that the @ character appears where our placeholder 'Z' character was (see line 32 in Listing 2.5).

The overall program steps were the same as the earlier program in Listing 2.3. However, the address initialization steps were a bit different in Listing 2.5. Those steps will be described here:
