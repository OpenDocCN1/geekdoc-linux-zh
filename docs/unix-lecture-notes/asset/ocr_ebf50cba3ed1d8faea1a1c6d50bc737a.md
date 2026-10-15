# 10.5.4 Thread Joining and Joinability

When a thread is created, one of the attributes defined for it is whether it is joinable or detached. By default, created threads are joinable. If a thread is joinable, another thread can wait for its termination using the function pthread_join(). Only threads that are created as joinable can be joined.

Joining is a way for one thread to wait for another thread to terminate, in much the same way that the wait() system calls lets a process wait for a child process. When a parent process creates a thread, it may need to know when that thread has terminated before it can perform some task. Joining a thread, like waiting for a process, is a way to synchronize the performance of tasks.

However, joining is different from waiting in one respect: the thread that calls pthread_join() must specify the thread ID of the thread for which it waits, making it more like waitpid(). The prototype is

```
int pthread_join(pthread_t thread, void **value_ptr);
```

The pthread_join() function suspends execution of the calling thread until the target thread terminates, unless the target thread has already terminated. If the target thread already terminated, pthread_join() returns successfully.

If value_ptr is not NULL, then the value passed to pthread_exit() by the terminating thread will be available in the location referenced by value_ptr, provided pthread_join() succeeds.

Some things that cause problems include:

+   - Multiple simultaneous calls to pthread_join() specifying the same target thread have undefined results.
+   - The behavior is undefined if the value specified by the thread argument to pthread_join() does not refer to a joinable thread.
+   - The behavior is undefined if the value specified by the thread argument to pthread_join() refers to the calling thread.
+   - Failing to join with a thread that is joinable produces a "zombie thread". Each zombie thread consumes some system resources, and when enough zombie threads have accumulated, it will no longer be possible to create new threads (or processes).

The following listing shows a simple example that creates a single thread and waits for it using pthread_join(), collecting and printing its exit status.

# Listing 10.1: Simple example of thread creation with join

```
int exitval;

void* hello_world( void * world)
{
    printf("Hello World from %s.\n", (char*) world);
    exitval = 2;
    pthread_exit((void*) exitval);
}
```