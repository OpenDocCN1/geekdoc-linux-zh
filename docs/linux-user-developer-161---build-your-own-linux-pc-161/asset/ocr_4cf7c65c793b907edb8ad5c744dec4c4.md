# It is worth the effort to break your problem down into a multi-threaded model

```
lock.acquire()
sun_var = curr_var
lock.release()
```

The last topic we will look at is synchronising threads so that they can work together effectively. There will be times when a number of threads need to talk to each other after working on a particular problem. The problem is how to share their individual results. You can use a barrier to ensure that all threads have finished calculating. Each thread will wait until all of the other threads have reached it. It will provide a point when the barrier is released.

Then there is another common issue in parallel programs deadlock. Issues occur when multiple locks are associated with different variables. Say you have variables A and B, and you need to lock both of them. If thread one tries to get lock A, and thread two tries to get lock B, they will both get their first requested lock, and then wait for the second requested lock.

If you need to actually have true parallel code that has the ability to run on multiple cores: because Python has the GIL, you need to move away from threads and go to separate processes to handle the different tasks. Luckily, Python provides a multiprocessing module that provides this. As with the threading module, you need to create a new process and hand in an array as a target function to run. To share data, it is trivial because memory is global and everybody can see everything.

The best way to avoid this is to be very careful. Unfortunately, people are not perfect and can create messy code. You can try to avoid this by including a timeout parameter when you call the acquire method. This will try to get the lock for a certain amount of time. If the timeout expires, the acquire method returns false. You can then tell or not it was successful by checking the return value. If it failed, return. Otherwise, return true.

However, since memory is not shared between processes you need to explicitly set up some forms of communications. You can create a queue object where you can transfer objects between processes objects on the queue, and other processes can use the get() method to pull objects off. If you want a more complex solution you can use a pipe to create a two-way communication channel between processes.

Another way to share data is by moving variables that you can access within the local scope of the individual threads. The ideal idea is to have a local copy of any version of variables that nobody else can see. This is done by copying all attributes to an object and using them as local variables. When being run by your thread, you would have code that looks like:

Because you need to tell the barrier how many threads will be in the area, you specify a count. If you create a barrier for three threads, it will wait until all have reached the barrier. The synchronization is then done by the barrier, and so a function can run after some amount of time. As with the barrier, the barrier can take a (start) argument in order to start the function.

You should make your code even more efficient by farming out intensive tasks to other methods of execution. The main part of your program remains free to interact with the end user and you can keep all parts of your Raspberry Pi as busy as possible.

The processing module also includes the idea of a process pool that is different from the threading pool. Processes can be used in a map function. This kind of construct is useful if you are applying the same function to a number of different inputs. For example a pool might be more of an intuitive method to use if you are writing your Python code.

```
my_local = threading.local()
my_local.x = 2
```

# Python column

![](bbox=[0.6, 0.11, 0.92, 0.36])