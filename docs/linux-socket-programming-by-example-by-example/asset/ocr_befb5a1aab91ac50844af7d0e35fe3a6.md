# Testing the select(2)-Based Server

The source code for the select(2) version of the RPN calculating server can be compiled as follows:

```
$ make rpnsrv2

```
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type rpnsrv2.c
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type rpneg2.c
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type makaddr.c
gcc rpnsv2.o rpneg2.o makaddr.o -o rpnsv2 -lgmp
```
```

The server executable rpnsv2 will execute as one single process, even when many clients connect to the server. To allow this to be tested, you will first want to start the server itself. The following launch of the server permits it to be contacted on any allowable interface on your system:

```
$ ./rpnsv2 `*:9009` &

```
[1] 730
```
```

The server is launched and placed into the background. The command-line argument of `*:9009' tells the server to specify a wild IP number, but to listen on TCP/IP port number 9009 for connects.

In order to properly test that this select(2) logic is operational, it is necessary to connect to the server with at least two simultaneous sessions. Without X Window sessions, this can be done from multiple console sessions. Using the X Window interface, you can easily start multiple terminal sessions for testing purposes.

Listing 11.6 shows one example xterm session using telnet to connect to the server. While this session is going on, another session, shown in Listing 11.7, is also created at the same time. It is only important that both sessions are connected to the server at the same time. Switching back and forth between sessions, the server should respond to each session as commands are provided to it.

# Listing 11.6: First telnet Session with rpnsv2

```
$ telnet localhost 9009

```
Trying 127.0.0.1...
Connected to localhost.
Escape character is `]'.
```
```

```
```
#:::?:?:::???::???::???
1:

```
genprime
```

```