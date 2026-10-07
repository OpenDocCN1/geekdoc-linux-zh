# Chapter 7 · Threads

You can mark code as synchronized two ways:

+   * Synchronize an entry by putting the synchronized modifier in the method's declaration. To execute the method, a thread must acquire the lock of the object that owns the method.

+   * Synchronize a method by surrounding the lines of code with curly brackets ({}) and inserting the synchronized(someObject) expression before opening the curly. This technique allows you to synchronize the block on the lock of any object at all, not necessarily the object that owns the code.

The first technique is by far the more common; synchronizing any object other than the object that owns the synchronized code can be extremely dangerous.

![](bbox=[0.17, 0.335, 0.255, 0.385])

The Certification Exam requires you to know how to apply the second technique, but the exam does not make you think through complicated scenarios of synchronizing on external objects. The second technique is discussed at the end of this chapter.

Synchronization makes it easy to clean up some of the problems with the Mailbox class:

```
1. class Mailbox {
2. private boolean request;
3. private String message;
4.
5. public synchronized void
6. sendMessage(String message) {
7. request = true;
8. this.message = message;
9. }
10.
11. public synchronized String retrieveMessage() {
12. request = false;
13. return message;
14. }
15. }
```

Now the request flag and the message string are private, so they can be modified only via the public methods of the class. Because sendMessage() and retrieveMessage() are synchronized, there is no danger of a message-producing thread corrupting the flag and spoiling things for a message-consuming thread, or vice versa.