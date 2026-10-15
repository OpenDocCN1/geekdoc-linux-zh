handling to work correctly. For this purpose, the relevant signal handlers include the code for resetting signals for future signal handling. For the signals.c program to work correctly on such systems, you need to modify the nicetry() function, the handler for SIGINT, as follows:

```
void nicetry(void)
{
    signal(SIGINT, nicetry);
    printf("Nice try! Sorry you cannot terminate me like this.\n");
}
```

# EXERCISE 19.15

Replicate the preceding sessions on your system. Does the signals.c program work as expected?

Several Internet services such as ftp are offered via server processes that provide services to client processes through multiple slave processes, one for each client. Slaves are precreated and/or created dynamically by the main server when needed. The main server is also known as the master server. Such servers are known as multiprocess servers or concurrent servers. A concurrent server runs in an infinite loop with the following code structure:

```
while (1) {
    wait for a client request
    create a slave process when a client request arrives
    slave handles the client request
}
```

Because concurrent servers keep creating slave processes as client requests arrive, it is important to terminate a slave process properly and remove it from the system after it has provided its service to a client process. This is done by using the exit() and wait() calls in tandem, in the slave and master processes, respectively. If the master server process does not remove the slave processes after they have provided their services, a large number of zombie processes will be created in the system. We would want the server to spawn a child, wait, and then when returned to, kill the child, but we can't do that with a concurrent server since it has to continue to process further client requests.

Recall that when a process terminates, the UNIX kernel sends the SIGCHLD signal to its parent. A concurrent server process uses this feature to intercept all SIGCHLD signals to remove the terminating slave processes from the system by using the following code structure:

```
...
int main(...)
{
    ...
```