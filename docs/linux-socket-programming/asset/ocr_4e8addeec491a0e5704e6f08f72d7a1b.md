```
}
```

Extending Thread lets you create the thread based on the class. The `run()` method determines where the thread begins to run. When the method exits, the thread terminates. The next few lines create the thread and run it.

```
public static void main(String[] args)
{
start(); // <-- start the thread and call run()
/**** do something while the thread runs ****
}
}
```

If you want to create several threads, call `start()` each time. As the name implies, all threads share all the data. To create a separate workspace for a thread, you can create a new object:

```
Thread t = new TestThread();
t.start();
```

# NOTE

# Play Fair with Java Threads

In the same way that tasks can take over the computer, Java threads can easily dominate the CPU time (this is more true of Windows than of Linux/UNIX). Be sure that you follow the guidelines listed in Chapter 7, "Dividing the Load: Multitasking," so that other tasks have a chance to run.

Any part of your program, including event and exception handlers, can create and start a thread. However, remember that you want to hold on to the reference to any created object. Otherwise, when a random garbage collection occurs, your dangling thread may suddenly terminate.

# Adding Threads to a Class

Sometimes, however, inheriting from Thread is not possible. The typical example is when you are writing a class that derives from Frame. Java does not allow multiple inheritance, so inheriting from both Frame and Thread is impossible. In this case, you can use the second technique of implementing the Runnable interface. The results are the same, and the program changes only slightly.

```
public class TestFrameThread extends Frame
implements Runnable
{
public void run()
{
/**** child thread ****
}
public void someMethod()
{
```