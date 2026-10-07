# Chapter 7 · Threads

Thus you can pass any object you want into the Thread constructor, provided it implements the Runnable interface (so that it really does a run() method for the thread scheduler to invoke). The object is called the thread's target. Having constructed an instance of Thread, you proceed as before: you invoke the start() method. As before, so registering the thread with the scheduler, and eventually the run() method of the target will be called.

For example, the class Runnable that counts from 10 to 1:

+   1. public class DownCounter implements Runnable {
2.   public void run() {
3.     for (int i = 10; i >= 1; i--) {
4.       System.out.println("Counting Down: " + i);
5.     }
6.   }
7. }

This class does not extend Thread. However, it has a run() method, and it declares that it implements the Runnable interface. Thus instance of the DownCounter class is eligible to be passed into the alternative (nonfinal) constructor for Thread:

+   1. DownCounter dc = new DownCounter();
2. Thread t = new DownCounter(dc);
3. t.start();

This section has two strategies for constructing threads: extending Thread and implementing Runnable. Specifically, the only difference between these strategies is the location of the run() method. The second strategy, where a runnable target is passed into the constructor, is a bit more complicated in the simple examples we have considered. There are good reasons why you might choose to make this extra effort. The run() method, like any other member method, is allowed to access the private data, and call the private methods of the class of which it is member. Putting run() in a subclass of Thread may mean that the member cannot access the features it needs (or cannot access such features in a clean, reasonable manner).

Another reason that might persuade you to implement threads using runnable rather than subclassing Thread is the single-inheritance rule. If you write a subclass of Thread, it cannot be a subclass of anything else; but using Runnable, you can subclass without another parent class.

From an object-oriented point of view, subclass two unrelated functionalities: support for multithreading inherited from the Thread superclass and execution behavior provided by the run() method. These functionalities are not closely related, so good object-oriented discipline suggests that they exist in two separate classes. In the jargon of oriented analysis, if you create a class that extends Thread, you're saying that your class "is a" thread. If you create a class that implements Runnable, you're saying that your class "is associated with" a thread.