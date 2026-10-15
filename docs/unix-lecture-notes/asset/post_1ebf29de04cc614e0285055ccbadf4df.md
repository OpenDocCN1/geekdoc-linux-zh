
```c
int main( int argc, char *argv[] )
{
    pthread_t child_thread;
    void *status;
    char *planet = "Pluto";

    if ( 0 != pthread_create(&child_thread, NULL,
        hello_world, ( void* ) planet) ) {
        perror("pthread_create");
        exit(-1);
    }
    pthread_join(child_thread, (void**) (&status));
    printf("Child exited with status %ld\n", (long) status);
    return 0;
}
```

Any thread in a process can join with any other thread. They are peers in this sense. The only obstacle is that to join a thread, it needs its thread ID.

## 10.5.5 Detached Threads

Because pthread_join() must be able to retrieve the status and thread ID of a terminated thread, this information must be stored someplace. In many Pthread implementations, it is stored in a structure that we will call a Thread Control Block (TCB). In these implementations, the entire TCB is kept around after the thread terminates, just because it is easier to do this. Therefore, until a thread has been joined, this TCB exists and uses memory. Failing to join a joinable thread turns these TCBs into waste memory.

Sometimes threads are created that do not need to be joined. Consider a process that spawns a thread for the sole purpose of writing output to a file. The process does not need to wait for this thread. When a thread is created that does not need to be joined, it can be created as a detached thread. When a detached thread terminates, no resources are saved; the system cleans up all resources related to the thread.

A thread can be created in a detached state, or it can be detached after it already exists. To create a thread in a detached state, you can use the pthread_attr_setdetachstate() function to modify the pthread_attr_t structure prior to creating the thread, as in:

```
pthread_t      tid; /* thread ID          */
pthread_attr_t attr; /* thread attribute */

pthread_attr_init(&attr);
pthread_attr_setdetachstate(&attr, PTHREAD_CREATE_DETACHED);

/* now create the thread */
pthread_create(&tid, &attr, start_routine, arg);
```

An existing thread can be detached using pthread_detach():

```
int pthread_detach(pthread_t thread);
```

The function pthread_detach() can be called from any thread, in particular from within the thread itself! It would need to get its thread ID using pthread_self(), as in

```
pthread_detach(pthread_self());
```

Once a thread is detached, it cannot become joinable. It is an irreversible decision. The following listing shows how a main program can exit, using pthread_exit() to allow its detached child to run and produce output, even after main() has ended. The call to usleep() gives a bit of a delay to simulate computationally demanding output being produced by the child.

### Listing 10.2: Example of detached child

```
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

void *thread_routine(void * arg)
{
    int i;
    int bufsize = strlen(arg);
    int fd = 1;

    printf("Child is running...\n");
    for (i = 0; i < bufsize; i++) {
        usleep(500000);
        write(fd, arg+i, 1);
    }
    printf("\nChild is now exiting.\n");
    return(NULL);
}

int main(int argc, char* argv[])
{
    char * buf = "abcdefghijklmnopqrstuvwxyz";
    pthread_t thread;
    pthread_attr_t attr;

    pthread_attr_init(&attr);
    pthread_attr_setdetachstate(&attr , PTHREAD_CREATE_DETACHED);

    if (pthread_create(&thread, NULL, thread_routine, (void *)(buf))) {
        fprintf(stderr, "error creating a new thread \n");
        exit(1);
    }

    printf("Main is now exiting.\n");
    pthread_exit(NULL);
}
```

## 10.5.6 Thread Cancellation

Threads can be canceled as well. Cancellation is roughly like killing a thread. When a thread is canceled, its resources are cleaned up and it is terminated. A thread can request that another thread be canceled by calling pthread_cancel(), the prototype for which is

```
int pthread_cancel(pthread_t thread);
```

This is just a request; it is not necessarily honored. When this is called, a cancellation request is sent to the thread given as the argument. Whether or not that thread is canceled depends upon the thread's cancelability state and type. A thread can enable or disable cancelability, and it can also specify whether its cancelability type is asynchronous or deferred. If a thread's cancelability type is asynchronous, then it will be canceled immediately upon receiving a cancellation request, assuming it has enabled its cancelability. On the other hand, if its cancelability is deferred, then cancellation requests are deferred until the thread enters a cancellation point. Certain functions are cancellation points. To be precise, if a thread is cancelable, and its type is deferred, and a cancellation request is pending for it, then if it calls a function that is a cancellation point, it will be terminated immediately. The list of cancellation point functions required by POSIX can be found on the man page for pthreads in section 7.

A thread's cancelability state is enabled by default and can be set by calling pthread_setcancelstate():

```
int pthread_setcancelstate(int state, int *oldstate);
```

The two values are PTHREAD_CANCEL_ENABLE and PTHREAD_CANCEL_DISABLE. The new state is passed as the first argument and a pointer to an integer to store the old state, or NULL, is the second argument. If a thread disables cancellation, then a cancellation request remains queued until it enables cancellation. If a thread has enabled cancellation, then its cancelability type determines when cancellation occurs.

A thread's cancellation type, which is deferred by default, can be set with pthread_setcanceltype():

```
int pthread_setcanceltype(int type, int *oldtype);
```

To set the type to asynchronous, pass PTHREAD_CANCEL_ASYNCHRONOUS in the first argument. To make it deferred, pass PTHREAD_CANCEL_DEFERRED.

## 10.5.7 Thread Properties

### 10.5.7.1 Stack Size

The POSIX standard does not dictate the size of a thread's stack, which can vary from one implementation to another. Furthermore, with today's demanding problems, exceeding the default stack limit is not so unusual, and if it happens, the program will terminate, possibly with corrupted data.

Safe and portable programs do not depend upon the default stack limit, but instead, explicitly allocate enough stack for each thread by using the pthread_attr_setstacksize() function, whose prototype is
