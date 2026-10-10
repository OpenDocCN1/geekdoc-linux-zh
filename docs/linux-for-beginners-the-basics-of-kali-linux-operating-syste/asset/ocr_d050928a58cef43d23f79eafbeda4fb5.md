```
```
append_to_buffer (item); // add about ' object item to the clipboard
up (lock); // exit critical section
up (full _items ); // inform consumers that there is a new object
}

// consumer
void consumer ()
{
    item_t item;
down (full _items ); // not empty buffer?
down ( lock ); // enter the critical section
item = receive_from_buffer (); // pick about ' Object item from the clipboard
up ( lock ); // exit critical section
up ( empty _items ); // notify manufacturers of the location
consume ( item ); // consume the object
}
```
```

# **Mutexes**

The concept of mutex largely coincides with the notion of blocking defined previously (Section 5.2). Synchronization primitives called Mutexes are the ones that prevent the execution of a piece of code in more than one stream. In fact, the mutex is an implementation of OS-level blocking. Mutex, as its name implies, eliminates mutual exclusion. Its main task is to block all threads trying to access the code when that code is already executing a thread. A mutex can be in two states: the free and the busy. The initial state is "free" and has two possible atomic operations.

+   - **Take mutex** (`mutex _ lock`): if mutex was free, he is busy, and the flow continues its execution (entering the critical section); if the mutex was busy, the stream enters a standby state (said to be a "wait on a mutex" or "locked on a mutex"), the execution continues another stream. Stream, which took mutex called the owner of the mutex: