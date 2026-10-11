# ## Threading a Class

To create a threadable class, you can either derive from the Thread class or implement the Runnable interface. In both cases, you must define the run() method where the thread actually begins running. In the first case, you can simply write the following:

```
```
public class TestThread extends Thread
{
    public void run()
    {
        /**** thread runs here ***/
    }
}
```

Extending Thread lets you create the thread based on the class. The run() method determines where the thread begins to run. When the method exits, the thread terminates. The next few lines create the thread and run it.
```

```
```
public static void main(String[] args)
{
    start(); // <-- start the thread and call run()
    /**** do something while the thread runs ***/
}
```

If you want to create several threads, call start() each time. As the name implies, all threads share all the data. To create a separate workspace for a thread, you can create a new object:
```

```
```
Thread t = new TestThread();
t.start();
```
```

> **Play Fair with Java Threads**
> 
> In the same way tasks can take over the computer, Java threads can easily dominate the CPU time (this is more true of Windows than of Linux/UNIX). Be sure that you follow the guidelines listed in Chapter 7, “Dividing the Load: Multitasking,” so that other tasks have a chance to run.

Any part of your program, including event and exception handlers, can create and start a thread. However, remember that you want to hold on to the reference to any created object. Otherwise, when a random garbage collection occurs, your dangling thread may suddenly terminate.