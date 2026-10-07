
## Chapter 5 · Flow Control, Assertions, and Exception Handling

then the block will handle any IOException instance and also (because that's how instanceof works) any instance of any subclass of IOException.

If the exception is not compatible with any catch block, or if it wasn't thrown from a try block, the JVM checks the exception types declared to be thrown by the current method. If a compatible type is found (again using `instanceof`), the JVM's attention turns to the method that called the current method, and this entire process repeats...possibly many times, if the exception is to be handled by the calling chain.

If [there] simply isn't a compatible catch block for the exception, the JVM prints the exception's stack trace and terminates itself. The compiler makes every possible effort to prevent you from writing code in which this happens.

Notice that if a try throws 15 different exception types, and all the types are subclasses of, for example, `IOException`, then you don't need 15 catch blocks. You can have a single catch (`IOException x`) block, because every exception that can possibly be thrown will be an instance of `IOException`. You would do this if every different exception required the same processing.

## Two Kinds of Exception checked and runtime.

Java has two kinds of exceptions: checked and runtime. A good way to understand the difference is to look at some exception class names. All of Java's exception classes have names that are somewhat long and quite descriptive.(It's a worthwhile trade-off.) For example, `ArrayIndexOutOfBoundsException`. It's obvious what condition one indicates. There's `FileNotFoundException`, which is equally obvious.

There's an important difference between an array index that's too large and a file that can't be found. The array index problem is completely avoidable; there is no reason why anyone should ship code that ties to nonexistent array elements. On the other hand, the existence or nonfiction of files on a disk is not something over the program or the programmer has any control. At the time you write your code, you can't possibly know what files will exist on disks attached to all computers that you run your program in the infinite future.

To put it bluntly, an out-of-bounds array index is your fault. An absent fault in Java terminology, the avoidable exceptions that you are known as runtime exceptions. The term isn't very descriptive; you might think of it as an abbreviation for "should-never-happen-at-runtime". Other runtime exceptions include `ArithmeticException`, which you've seen division by zero, and `NegativeArraySizeException`, which is when you construct an array with it gotten—negative length.

The right time to deal with runtime exceptions is when you're designing, developing, and debugging your code. Since runtime exceptions should never be thrown in finished code, it's not appropriate to deal with them in catch blocks. In fact, runtime exceptions are exempt from the rules you've discussed so far. You are free to call methods that throw runtime exceptions, without enclosing the classes in try blocks or adding throws to the declaration of your enclosing methods. If it weren't for this exemption, Java source would be all but impossible to read.

Every expression that uses division, every array construction, and every other would require an exception-handling mechanism.

The compiler and JVM define runtime exceptions to be the java.lang.RuntimeException class, as well as all its subclasses. Figure 5.1 shows the big picture of the exception hierarchy.
Any exception that does not descend from RuntimeException is known as a checked exception, or it is the checked exception that is handled by the try-catch mechanism. The compiler ensures that every checked exception has a handler somewhere.

Errors, which appear on the right side of the figure, behave just like other checked exceptions. However, programmers should never throw or catch errors, which are mostly troubling in JVM. The only errors that programmers are likely to see are assertion errors, which are discussed later in chapter.

## FIGURE 5.1 The Exception Inheritance Hierarchy

![](img/09f8389b7ae2705d1ab14be2d5e857e3_179_0.png)

## The finally Block

The last catch associated with a try block may be followed by a finally block. This is a block of code, enclosed in curly (()) and preceded by the keyword finally. Here's an example:

1. File myfile = getmyfile();
2. String s = getStringAndHopeForAllAllDigits();
3.
4. try {
5. System.out.println("About to call.");
6. int x = Integer.parseInt(s);
7. myFile.getCanonicalFile();
8. System.out.println("Call succeeded.");
9. }
10.
11. catch (FormatException xceptn) {
12. System.out.println("Bad text!" + xceptn.getMessage());
13. xceptn.printStackTrace();
14. }
15.
16. catch (IOException xceptn) {
17. System.out.println("File stress!" + xceptn.getMessage());
18. xceptn.printStackTrace();
19. }
20.
21. finally {
22. System.out.println("In the finally block.");
23. }
24.
25. System.out.println("Life goes on.");

**The finally block's code is guaranteed to execute in nearly all circumstances.** If the block throws its exception, execution jumps to the corresponding exception handler, and so the finally block doesn't run to completion. Aside from that it takes a catastrophe to prevent a finally block from running. Here's what it takes:

- The death of the thread
- System.exit()

At first glance, finally blocks don't seem very useful. After all, isn't the first line? The finally block's code is guaranteed to execute in nearly all circumstances. If the block throws its exception, execution jumps to the corresponding exception handler, and so the finally block doesn't run to completion. Aside from that it takes a catastrophe to prevent a finally block from running. Here's what it takes:

- The death of the thread
- System.exit()

At first glance, finally blocks don't seem very useful. After all, isn't the first line? The finally block's code is guaranteed to execute in nearly all circumstances. If the block throws its exception, execution jumps to the corresponding exception handler, and so the finally block doesn't run to completion. Aside from that it takes a catastrophe to prevent a finally block from running. Here's what it takes:

- The death of the thread
- System.exit()

At first glance, finally blocks don't seem very useful. After all, isn't the first line? The finally block's code is guaranteed to execute in nearly all circumstances. If the block throws its exception, execution jumps to the corresponding exception handler, and so the finally block doesn't run to completion. Aside from that it takes a catastrophe to prevent a finally block from running. Here's what it takes:

- The death of the thread
- System.exit()

At first glance, finally blocks don't seem very useful. After all, isn't the first line? The finally block's code is guaranteed to execute in nearly all circumstances. If the block throws its exception, execution jumps to the corresponding exception handler, and so the finally block doesn't run to completion. Aside from that it takes a catastrophe to prevent a finally block from running. Here's what it takes:

- The death of the thread
- System.exit()

At first glance, finally blocks don't seem very useful. After all, isn't the first line? The finally block's code is guaranteed to execute in nearly all circumstances. If the block throws its exception, execution jumps to the corresponding exception handler, and so the finally block doesn't run to completion. Aside from that it takes a catastrophe to prevent a finally block from block from running. Here's what it takes:

- The death of the thread
- System.exit()

At first glance, finally blocks don't seem very useful. After all, isn't the first line? The finally block's code is guaranteed to execute in nearly all circumstances. If the block throws its exception, execution jumps to the corresponding exception handler, and so the finally block doesn't run to completion. Aside from that it takes a catastrophe to prevent a finally block from running. Here's what it takes:

- The death of the thread
- System.exit()

## Throwing Exceptions

Every expression that uses division, every array construction, and every other would require an exception-handling mechanism.

The code is guaranteed to execute in nearly all circumstances. If the block throws its exception, execution jumps to the corresponding exception handler, and so the finally block doesn't run to completion. Aside from that it takes a catastrophe to prevent a finally block from running. Here's what it takes:

- The death of the thread
- System.exit()

At first glance, finally blocks don't seem very useful. After all, isn't the first line? The finally block's code is guaranteed to execute in nearly all circumstances. If the block throws its exception, execution jumps to the corresponding exception handler, and so the finally block doesn't run to completion. Aside from that it takes a catastrophe to prevent a finally block from running. Here's what it takes:

- The death of the thread
- System.exit()

At the point where you want to throw, construct an instance of your exception type. Then use the throw keyword as shown in the example:

```
IOException x = new IOException('Phaser bank lock.');
throw x;
```

All the exceptions in the core have two constructors. One is a args-construct. It's bad to use it. It's much more helpful to pass a descriptive string into the constructor. This string is returned when someone catches your exception and calls getMessage().

The moment an exception is constructed, the current thread's stack is recorded in the exception object, where it can be retrieved. It's good practice to throw an exception as soon as possible after construction, so that the stack will reflect the thread's status at the moment the exception was thrown.

> All checked types thrown from a method must be represented in the throws list. To properly represent them, an exception type must either appear on the list or descend from a type that appears on the list.

## Creating Your Exception Classes

Creating your own exception is easy. First, decide whether you want a checked or a runtime exception. Checked exceptions should extend lang.Exception or one of its subclasses. Runtime exceptions should extend lang.RuntimeException or one of its subclasses. Choose a descriptive name for your class that will end with exception.

The class doesn't need methods, unless you have a special need for them. It should have two constructors. The argument list of these should include

- A message
- A cause
- A message and a cause that is retrieved by the getMessage() call.

> A message is a string that is retrieved by the getMessage() call. A cause is another exception. Causes come into play when a method handles an exception by throwing a different exception type, one that will have more information about the method's callers. The code that catches the exception might need more information embedded in the original exception: the cause or the stack trace might be especially useful.

To retrieve an exception's cause, call getCause(). The return type is actually Throwable, which allows throwables and errors to have causes. A cause might have its own cause, and so on; this structure is known as exception chaining.

All you need to deal with the message and cause is pass to the superclass constructor. Here's an example:

```java
public class PhaserBankException extends Exception {
  public PhaserBankException(String message) {
    super(message);
  }
}
```
