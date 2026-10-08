# Multitask with your Pi

Learn how to add multitasking to your own Python code – perfect for those with multiple projects on the go

The majority of programmers will learn single-threaded programming as their first computational model. The basic idea is that instructions for the computer are processed sequentially, one after the other. This works well enough in most situations, but you will reach a point where you need to start multitasking. The classical situation for writing multi-threaded applications is to have them run on a multi-processor machine of some persuasion. In these cases, you would have some heavy, compute-bound process running on each processor. Since your Raspberry Pi is not a huge 16-core desktop machine, you might be under the assumption that you can't take advantage of using multiple threads of execution. This isn't true, though.

There are lots of problems that map naturally to the multiple thread model. You may also have IO operations that take a relatively large amount of time to complete. In these cases, it is well worth your programming effort to break your problem down into a multi-threaded model. Since Python is the language of choice for the Raspberry Pi, we will look at how you can add threads to your own Python code. For those of you who have looked into multi-threaded programming in Python, you may have run into the GIL (Global Interpreter Lock) before. This lock means that only one thread can actually be running at a time, so you don't get true parallel processing. But on the Raspberry Pi, this is actually okay.

The first bit of code we need is to import the correct module. For this article, we will be using the threading module. Once it is imported, you have access to all of the functions and objects that you would need to write your code. The first step is to create a new thread object with the constructor:

```
t = threading.Thread(target=my_func)
```

The thread object takes some function that you have created, my_func in the above example, as the target code that needs to be run. When the

thread object has finished its initialisation, it is alive but not running. You need to explicitly call the new thread's start() method. This will begin running the code within the function handed to the thread.

You can check to verify that this thread is alive and active by calling its is_alive() method. Normally, this new thread will run until the function exits normally. The other way a thread can exit is if an unhandled exception is raised. Depending on your experience of parallel programs, you may already have some ideas on what types of code you want to write. For example, in MPI programs, you typically use the same overall code running in multiple threads of execution. You use the thread's ID and a series of if or case statements to have each thread execute a different section of the code. To do something similar, you can use something like:

```
def my_func():
    id = threading.get_ident()
    if (id == 1):
        do_something()
thread1 = threading.Thread(target=my_func) thread1.start()
```

This code works in Python 3, but the get_ident() function doesn't exist in Python 2. Threading is one of those modules that is a moving target when moving from one version of Python to another, so always check the documentation for the version of Python you are coding for.

Another common task in parallel programming is to farm out time-intensive IO to separate threads. This way, your main program can continue on with the core work and all of the computing resources are kept as busy as possible. But how do you figure out if the child thread is done yet or not? You can use the is_alive() function mentioned above, but what if you can't continue without the results from the child thread? In these cases, you can use the join() method of the thread object you

are waiting on. This method blocks until the thread in question returns. You can include an optional parameter to have the method time-out after some number of seconds. This allows you to not get trapped into a thread that will never return due to some error or code bug.

Now that we have more than one thread of execution happening at the same time, we have a new set of issues to start worrying about. The first is accessing global data elements. What might happen if we had two different threads that want to read, or even worse write, to the same variable in global memory? You can have situations where changes to the value of variables can get out of sync with what you were expecting them to be.

These types of issues are called race conditions, because the different threads are racing with each other to see in what order their updates to variables will happen. There are two solutions to this type of problem. The first is to control access to these global variables and only allow one thread at a time to be able to work with them. The generic term describing this control is to use a mutex to control this access. A mutex is an object that a thread needs to lock before working with the associated variables. In the Python threading module, this object is called a lock. The first step is to create a new Lock object with:

```
lock = threading.Lock()
```

This new lock is created in an unlocked state, ready to be used. The thread interested in using it must call the acquire() method for the lock. If the lock is currently available then it changes state to the locked state and your thread can run the code that is meant to be protected. If the lock is currently in a locked state, then your thread will sit in a blocked state, waiting for the lock to become free. Once you are done with the protected code, you need to call the release() method to free the lock and make it available for the next thread. You could control a variable containing the sum of a series of results with: