
## Listing 9.2
/* Cleanup Handler Example */
#include <pthread.h>

typedef struct my_queue_tag {
    pthread_mutex_t  mutex;      /* Protects access to queue */
    pthread_cond_t   cond;      /* Signals change to queue */
    int              get, put;  /* Queue pointers */
    unsigned char    empty, full; /* Status flags */
    q[Q_SIZE];                  /* the queue itself */
} my_queue_t;

my_queue_t data = {
    PTHREAD_MUTEX_INITIALIZER, PTHREAD_COND_INITIALIZER, 0, 0, 1, 0};

void cleanup_handler (void *arg)
/*
   Unlocks the mutex associated with a queue
*/
{
    pthread_mutex_unlock ((mutex *) arg);
}

int main (int argc, char *argv[])
{
    while (1)
    {
        pthread_cleanup_push (cleanup_handler, (void *) &data.mutex);
        pthread_mutex_lock (&data.mutex);
        if (queue is empty)
        {
            data.empty = 1;
            pthread_cond_wait (&data.cond, &data.mutex);
        }
        /* read data from queue */
        pthread_cleanup_pop (1);
        /* do something with the data */
    }
}

## Pthreads Implementations

Until kernel version 2.6, the most prevalent threads implementation was LinuxThreads. It had been around since about 1996, and by the time development began on the 2.5 kernel it was generally agreed that a new approach was needed to address the limitations in LinuxThreads. Among these limitations, the kernel represents each thread as a separate process, or *schedulable entity*, giving it a unique process ID, even though many threads exist within one process entity. This causes compatibility problems with other thread implementations. There is a hard coded limit of 8192 threads per process, and while this may seem like a lot, there are some problems that can benefit from running thousands of threads.

The result of this new development effort is the Native Posix Threading Library, or NPTL, which is now the standard threading implementation in 2.6 and 3.x series kernels. It too treats each thread as a separately schedulable entity, but takes advantage of improvements in the kernel that were specifically intended to overcome the limitations in LinuxThreads. The `clone()` call was extended to optimize thread creation. There is no longer a limit on the number of threads per process, and the new Completely Fair Scheduler can handle thousands of threads without excessive overhead. A new synchronization mechanism, the Fast Mutex or “futex”, handles the noncontention case without a kernel call.

In tests on an IA-32, NPTL is reportedly able to start 100,000 threads in two seconds. By comparison, this test under a kernel without NPTL would have taken around 15 minutes.

## Upgrading the Thermostat

We now have enough background to add a thread to our thermostat to monitor the serial port for changes to the parameters. We will use a very simple protocol to set parameters consisting of a letter followed by a space followed by a number. “s” represents the setpoint, “l” the limit, and “d” the deadband. So, to change the setpoint you would enter, for example:

```
s 65<Enter>
```

This sets the setpoint to 65 degrees.

Copy `thermostat.c` that currently resides in `src/measure/` to `src/posix/`. Create a new Eclipse project called “posix”, located in the `home/samples/src/posix/` directory. Again, be sure it is a makefile project, and import the project settings with the include paths. Open `monitor.c`. The first thing to notice is `#include <pthread.h>`. This header file prototypes the Pthreads API. Note the declarations of `paramMutex` and `monitor`. The latter will become the handle for our monitor thread.

Because the parameters, `setpoint`, `limit`, and `deadband`, are accessed independently by the two threads, the thermostat and monitor, we need a mutex to guarantee exclusive access to one thread or the other. In reality, this particular application probably does not absolutely require the mutex, because the shared resources are simple integers and access to them should be atomic. But it does serve to illustrate the point.

Note, incidentally, that `setpoint`, `limit`, and `deadband` are declared `extern` in `thermostat.h`. It is assumed that these variables are allocated in `thermostat.c`. If you happened to use different names for your parameters, you will need to change them to match.

Take a look at the `monitor()` function. It is just a simple loop that gets and parses a string from `stdin`. Note that `before monitor()` changes any of the parameters, it locks `paramMutex`. At the end of the switch statement, it unlocks `paramMutex`. This same approach will be required in your thermostat state machine.

Move down to the function `createThread()`. This will be called from `main()` in `thermostat.c` to initialize `paramMutex` and create the monitor thread. `createThread()` returns a nonzero value if it fails. `terminateThread()` makes sure the monitor thread is properly terminated before terminating `main()`. It should be called from `main()` just before `closeAll()`.

## Changes Required in Thermostat.c

Surprisingly little changes to make `thermostat.c` work with the monitor.

- include `pthread.h` and `thermostat.h`.
- call `createThread()`, and test the return value at the top of `main()`,
- lock `paramMutex` just before the switch statement on the state variable, and unlock it at the end of the switch statement.
- call `terminateThread()` just after the `running` loop.

That is it! The makefile supports both target and simulation builds, as described in the last chapter. The drivers for both builds come from the `measure/` directory, and it is assumed that they are built. Build the simulation and try it out.

## Debugging Multithreaded Programs

Multithreading does introduce some complications to the debugging process but, fortunately, GDB has facilities for dealing with those. Debug `thermostat_s` in Eclipse (be sure `devices` is running) using the host debug configuration, and set a breakpoint at the call to `createThread()` in `main()`. When it stops at the breakpoint, click Step into to go into the `createThread()` function.

Step over the `pthread_mutex_init()` call, and `CHECK_ERROR`. Now, when you step over the call to `pthread_create()`, a second thread appears in the Debug view. This is the monitor thread, and it is already inside the `fgets()` call.

Set a breakpoint in the `monitor()` function just after the call to `fgets()`. Now, enter a line of text in the `Console` view. It does not really matter if it is a valid command or not. All we want to do at this point is get the program to stop at the breakpoint. Let the program continue, and when it reaches the breakpoint note that `Thread [2]` is now the one suspended at a breakpoint. `Thread [1]` is most likely suspended inside the `sleep()` function.

Play around with setting breakpoints in various places in both `main()` and `monitor()` to verify that parameters get updated properly and the thermostat responds correctly to the new values.

When you are satisfied with the program running under the simulation, rebuild it for the target and debug it there. You will need to create a new make target, just as we did in the previous chapter for the measure project. You will also need to delete both `monitor.o` and `thermostat.o` for the target version to build properly.

When you start the debugger, you are likely to see some warning messages whiz by in the Console view. These are innocuous.

The debugger stops at the first line of `main()` as normal. Let the program execute to the breakpoint at `createThread()`. Step over, and the Debug view shows two threads just as we saw in the simulation version. From here on out, the target debugging process is essentially identical to the simulation mode.

With a basic understanding of threads, we are ready to tackle networking, the subject of the next chapter.

## Resources

The Open Group has made available free for private use the entire Posix (now called Single Unix) specification. Go to: `www.unix.org/online.html`

You will be asked to register. Don’t worry, it is painless and free. Once you register, you can read the specification on-line, or download the entire set of `html` files for local access.

This chapter has been little more than a brief introduction to Posix threads. There is a lot more to it. An excellent, more thorough treatment is found in,

Butenhof, David R., *Programming with POSIX Threads*, Addison-Wesley, 1997.
