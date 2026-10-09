```
Thread t = new Thread(this);
t.start();
}

```

The **bold text** indicates two changes to the source. The first is the inheritance of `Frame` and the implementation of `Runnable`. This declares the relationships we need to get the right program behavior. The second change is the creation of a thread. The `Thread` class has an additional constructor that accepts any object that implements the `Runnable` interface and makes a `Thread` object out of it. Calling `start()` does the same thing as if the class were derived from `Thread`.

All threads that run in a class can actually be unrelated to the class's base functionality. You really don't have any restriction. But if you encounter different groups of responsibilities, be certain that in reality you don't have two different classes. Two ways to determine whether you really have disparate classes include how much the separate threads (parent and child) share and whether the child-thread could exist without the parent's data or features.

Creating a separate class for each primary responsibility is good object design, and it really helps in a multiprogramming environment. If you need access to each object's methods or resources, create property control methods (`set()`/`get()`). By centralizing all the attribute control through methods, you really build on encapsulation and make thread synchronization easier.

# Synchronizing Methods

One primary advantage of threads is the capability to share resources. This causes the same mutual exclusion problems that [Chapter 7](#) describes. Java solves this problem by using `synchronized` methods.

The `synchronized` method replaces the semaphores used in `pthread`. The declaration is

```
public synchronized changeSomething()
{
    /\*\*\* Manage contended resource \*\*\*/
}
```

The `synchronized` keyword forces all entries in the method to happen one at a time. Before another thread can enter the method, the first has to complete its call.

Sometimes you need a little more control. For example, suppose you have three threads (parent and two children) that control the incoming and outgoing of buffers through a socket. You don't want to send a buffer until it is full, and the child threads control the outgoing buffers. A synchronized method grabs control of a buffer, but it is not full enough. The method could return a fail-value, forcing the child to retry the call. Alternatively, the method could hold on to the resource and force the thread to yield control temporarily.

Stepping back for a minute, when threads contend for a controlled resource, they enter a waiting queue. When the current resource owner exits the synchronized method, the next thread in the queue grabs control of the resource. This continues as long as the threads contend.