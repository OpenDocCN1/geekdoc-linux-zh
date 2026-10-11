Although limited, you can see that Listing 10.6 is a simple server loop that keeps accepting client connections in single-file fashion. Later, you’ll learn how to write a higher-performance server that can concurrently process several clients at one time.

# Trying Out the RPN Server

To compile all the related source modules for the RPN server, you can perform the following make command:

```
$ make rpngrv

gcc -c -D_GNU_SOURCE -Wall -Wreturn-type rpngrv.c
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type rnpeng.c
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type mkaddr.c
gcc rpngrv.o rnpeng.o mkaddr.o -o rpngrv -lgmp
$ 
```

After the executable rpngrv for the server has been created, you can start the server as follows:

```
$ ./rpngrv &
[1] 13321
$ 
```

In the output shown, the server was started with a process ID of 13321, and run in the background.

To keep things simple at this point, you’ll just use the telnet command to try out the server. The next chapter will fully outline this server’s functions. For now, just try some simple tests.

> The server presented is not a production-grade server. Some forms of incorrect input can provoke the server to abort.

The RPN calculator computes based upon numbers that are pushed onto the stack. To perform the add operation, for example, requires at least two numbers to exist on the stack. To push a number onto the stack, you will enter a line as follows:

```
#:970976453
```

After you press Enter, the server will respond with something like this: 0:

This tells you that the number has been stacked at the bottom of the stack (entry number zero). To stack another number, simply do the same, as follows:

```
#:2636364
```