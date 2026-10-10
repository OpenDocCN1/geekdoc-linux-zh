
should be sufficient in this case, because there is only one client that will be connecting to this server.

Now we are ready to *accept* connection requests. The arguments to *accept*() are:

- The socket descriptor.
- A pointer to a *sockaddr* structure that *accept*() will fill in.
- A pointer to an integer that currently holds the length of the structure in argument 2. *accept*() will modify this if the length of the client’s address structure is shorter.

*accept*() blocks until a connection request arrives. The return value is a socket descriptor to be used for data transfers to/from this client. In this example, the server simply echoes back text strings received from the client until the incoming string begins with “q.”

### The Client

Now look at `netclient.c`. `netclient` determines at run time whether it is connecting to a server locally or across the network. We start by creating a socket and an address structure in the same manner as in the server. Then we *connect* to the server by calling *connect*(). The arguments are:

- The socket descriptor.
- A pointer to the *sockaddr* structure containing the address of the server we want to connect to.
- The length of the *sockaddr* structure.

When *connect*() returns, we are ready to transfer data. The client prompts for a text string, writes this string to the socket, and waits to read a response. The process terminates when the first character of the input string is “q.”

### Try it Out

We will need to create make targets for the server and client. Take a look at the makefile to see how these targets are specified. This project includes a number of make targets. You can create them all now, or wait until they are needed. Note, incidentally, that there is no all target “at all.” Make both the client and the local server. Set up the host debug configuration to debug the server, and start a debug session. Step through the code up to and through the call to *accept*(), which will block until the client initiates a connection.

In a shell window, `cd` to the `network/` directory and execute `./netclient`. Type in a few strings and watch what happens. To terminate both processes, enter a string that begins with “q” (“quit” for example).

Next, we will want to run `netserve` on the target with `netclient` running on the host. Delete `netserv.e.o`, and build the make target for the remote server.

In the terminal window connected to the target (the one running `ssh`), `cd` to the `network/` directory and execute `./netserve`. Back in the original window, execute `./netclient remote`.

### A Remote Thermostat

Moving on to a more practical example, our thermostat may very well end up in a distributed industrial environment where the current temperature must be reported to a remote monitoring station, and setpoint and limit need to be remotely settable. Naturally we will want to do that over a network.

Copy `monitor.c` and `thermostat.c` from the `Posix/` directory to `network/`, and do a Refresh on the network project to bring those files into Eclipse. Actually, `thermostat.c` does not require any changes. Here are the modifications required in `monitor.c`:

1. Isolate the process of setting up the net server and establishing a connection in a separate function called `createServer()`, which consists roughly of lines 18 to 55 from `netserv.e.c`. The reason for doing it this way will become apparent soon. `createServer()` takes no arguments, and returns an `int` that is the socket number returned by `accept()`. It should return a `-1` if anything fails.
2. Call `createServer()` from `monitor()` just before the `while (1)` loop, and check the return value for error.
3. Replace `fgets()` with `read()` on the socket returned by `createServer()`.
4. Add a new command to the `switch` statement, “?”, that returns the current temperature over the network. Actually, we might want to query any of the thermostat’s parameters. Think about how you might extend the command protocol to accomplish that.
5. The `netclient` expects a response string for every string it sends to the server. So return `"OK"` for every valid parameter change command, and return `"???"` for an invalid command.

Create make targets for both the simulation and target versions of the thermostat. Build the simulation version, and point the host debug configuration at `network/thermostat_s`. You will need two shell windows to exercise the thermostat; one for the `devices` program and the other for `netclient`.

When you are satisfied with the simulation, build the target version, and try it there. Remember to delete `thermostat.o` and `monitor.o` before rebuilding. Also remember to execute `netclient remote`, to get the client talking to the server on the target.

> There should be a way to do this automatically in the makefile, but I haven’t figured it out yet.

## Multiple Monitor Threads

As the net thermostat is currently built, only one client can be connected to it at a time. It is quite likely that in a real application, multiple clients might want to connect to the thermostat simultaneously. Remember from our discussion of sockets that the server process may choose to spawn a new process or thread in response to a connection request so it can immediately go back and listen for more requests.

In our case, we can create a new monitor thread. That is the idea behind the `createServer()` function. It can be turned into a server thread whose job is to spawn a new monitor thread when a connection request comes along. So give it a try.

Here, in broad terms, are the steps required to convert the net thermostat to service multiple clients:

1. Copy `monitor.c` to `multimon.c` and work in that file.
2. Recast `createServer()` as a thread function.
3. In the `createThread()` function, change the arguments of the `pthread_create()` call to create the server thread instead of the monitor thread.
4. Go down to the last four lines in `createServer()`, following the comment “Accept a connection.” Bracket these lines with an infinite while loop.
5. Following the `printf()` statement, add a call to `pthread_create()` to create a monitor thread.
6. Add a case "q": to the switch statement in the monitor thread. “q” says the client is terminating (quitting) the session. This means the monitor thread should exit.

Now, here are the tricky parts. The `client_socket` will have to be passed to the newly-created monitor thread. Where does the thread object come from for each invocation of `pthread_create()`? A simple way might be to estimate the maximum number of clients that would ever want to access the thermostat, and then create an array of `pthread_t` that big. The other, more general, approach is to use dynamic memory allocation, the `malloc()` function.

But the biggest problem is how do you recover a `pthread_t` object when a monitor thread terminates? The monitor thread itself cannot return it, because the object is still in scope, that is, still being used. If we ignore the problem, the thermostat will eventually become unresponsive either because all elements of the `pthread_t` array have been used, or we run out of memory because nothing is being returned to the dynamic memory pool.

Here are some thoughts. Associate a flag with each `pthread_t` object, whether it is allocated on a fixed array or dynamically allocated. The flag, which is part of a data structure that includes the `pthread_t`, indicates whether its associated `pthread_t` is free, in use, or “pending,” that is, able to be freed. The server thread sets this flag to the “in use” state when creating the monitor. The structure should probably also include the socket number. It is this “meta” `pthread_t` object that gets allocated and passed to the monitor thread.

Now the question is, when can the flag be set to the “free” state? Again, the monitor cannot do it, because the `pthread_t` object is still in use until the thread actually exits. Here is where the third state, PENDING, comes in.

The monitor sets the flag to PENDING just before it terminates. Then we create a separate thread, call it “resource” if you will, that does the following:

1. Wakes up periodically and checks for monitor threads that have set their flags to PENDING.
2. Joins the thread.
3. Marks the meta pthread object free.
4. Goes back to sleep.

Remember that when one thread joins another, the “joiner” (in this case resource) is blocked until the “joinee” (monitor) terminates. So, when resource continues from the `pthread_join()` call, the just-terminated monitor’s `pthread_t` object is guaranteed to be free. The semantics of `pthread_join()` are:

```c
int pthread_join (pthread_t thread, void **ret_value)
```

It is quite likely that by the time the resource thread wakes up, the monitor thread has already exited, in which case `pthread_join()` returns immediately with the error code `ESRCH`, meaning that `thread` does not exist.

The `createThread()` function now needs to create the server thread and the resource thread. Likewise, `terminateThread()` needs to cancel and join both of those. And of course, any monitor threads that are running also need to be cancelled. That is, when the resource thread terminates, it needs to go through the list of meta pthreads checking for running monitors. Ah, but the resource thread doesn’t know it is being cancelled.

Here is a good use for a cleanup handler. Write a cleanup handler that runs through the list of meta pthreads looking for any that are in the IN USE state. Cancel and join the corresponding thread. Call `pthread_cleanup_push()` just before the main loop in the resource thread. Add a call to `pthread_cleanup_pop()` just after the loop. It will never be called, but it closes the block opened by `pthread_cleanup_push()`.

If you do not feel up to writing this yourself, you may have already noticed that there is an implementation of `multimon.c` in the `samples/working/` directory.

There is a separate makefile called `Makefile.multi` to build the multiple client versions of `netthermo`. The build command for the Eclipse target is:

```
make -f Makefile.multi
```
