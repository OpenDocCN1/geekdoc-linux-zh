# 6.12.1 Non-polling I/O Using the O_ASYNC Flag

When you set the O_ASYNC flag on a file descriptor, it causes input from the descriptor's file connection to be partially delivered asynchronously. To be precise, it means that when input is available on the device, it is copied by the kernel into a location in the kernel's address space, after which the kernel sends a SIGIO signal to the process. To set up signal-driven input by this method, the program must do the following:

+   1. Tell the kernel which process should be sent the SIGIO signal when the data is ready to read by calling
+   
+       fcntl(F_SETOWN, getpid());

The SETOWN operation makes the process-id in the second argument the owner of the signal to be received. Usually the program wants to receive the signal itself, so it calls this with getpid().

+   2. Retrieve the existing flags on the standard input device with
+   
+       fcntl(0, F_GETFL);

+   3. Set the O_ASYNC flag on the connection with
+   
+       fcntl(0,F_SETFL,(fd_flags|O_ASYNC));

+   4. Assuming that on_input() is the function that will handle the SIGIO signal, register that signal handler:

```
struct sigaction newhandler;
sigset_t          blocked;
newhandler.sa_handler = on_input;
newhandler.sa_flags = SA_RESTART;
sigemptyset(&blocked);
newhandler.sa_mask = blocked;
sigaction(SIGIO, &newhandler, NULL);
```

The on_input() handler can call the NCurses getch() function and will be guaranteed to receive the single character input by the user. This way it does not have to be in a loop doing a blocking read and can instead do other things in the loop.

This is all put together in the program bouncestr_async.c. The first three of the above steps can be put into a function called enable_keybd_signals():

```
void enable_keybd_signals()
{
    int fd_flags;

    fcntl(0, F_SETOWN, getpid());
    fd_flags = fcntl(0, F_GETFL);
    fcntl(0, F_SETFL, (fd_flags|O_ASYNC));
}
```