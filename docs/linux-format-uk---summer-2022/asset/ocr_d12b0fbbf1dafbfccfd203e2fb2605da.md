# CODING ACADEMY  Multi-threaded code

![](bbox=[0.05, 0.08, 0.13, 0.17])

**Quick tip**

**Encouraging a new component or module to be thread-safe by providing it with its own locks.** For example, if you’re building a new widget that interacts with a global object, you should always use the global object’s lock to ensure thread safety.

**Part of a global object may be volatile.** If the object is volatile, a thread must use a lock when accessing that specific part. The example at the bottom of the left-hand column shows how you should use the `pthread_mutex_lock` and `pthread_mutex_unlock` functions to create a lock.

```
```c
void myFunction()
{
    pthread_mutex_lock(&myLock);
    // Access global variable
    globalVariable = 100;
    pthread_mutex_unlock(&myLock);
}
```
```

**pthread_join()** After the start of the thread is signalled with the second argument to `pthread_create()`, you use this function to wait for the thread to finish. **Note that if the thread has already finished, `pthread_join()` will return immediately.**

+   *   **pthread_t** is a type definition for a thread ID
+   *   **pthread_create()** is the function that creates a new thread, where the arguments are:
+       *   `pthread_t` for the thread ID of the newly created thread
+       *   attributes, which are usually set to `NULL`
+       *   a function pointer, which is the function to execute in the new thread
+       *   an argument, which is passed to the function
+   *   **pthread_join()** is the function that blocks a thread until another thread terminates

**Mutexes**

Once you have two threads accessing the same global resource, there’s the danger that a race condition will arise, where they both try to access it at the same time. This is where the second argument to `pthread_mutex_lock()` and the third argument to `pthread_mutex_unlock()` become important. These are used to prevent race conditions and ensure that only one thread is accessing the resource at a time.

**Message channels**

Threads can be used for sending asynchronous communication messages through a message channel. This can be used for inter-process communication, such as between a server and client, or for inter-thread communication within a process. The message channel is implemented as a queue, where messages are added to the end and removed from the beginning.

```
```c
void messageChannel(int* queue, int* readIndex, int* writeIndex, int* size)
{
    // Implementation details
}
```
```

**This code is not using any mutexes** – there’s a good chance that the global resource will be accessed by multiple threads at the same time. This is a race condition, and it’s very likely that it will cause a bug in your program. It’s important to keep this in mind when writing multi-threaded code.

**Semaphores**

Semaphores are a more general mechanism than mutexes for synchronizing threads. They can be used to limit the number of threads that can access a shared resource at the same time. This is useful when you have a limited number of resources, such as database connections.

**Condition variables**

Condition variables are used to wait for a specific condition to become true. They are often used together with mutexes to synchronize access to shared resources. A thread can wait on a condition variable and be woken up when the condition becomes true.

**Deadlocks**

A deadlock is a situation where two or more threads are blocked indefinitely while waiting for resources that are being held by other threads. This can happen if threads acquire locks in a different order. It’s important to avoid deadlocks by designing your code carefully.