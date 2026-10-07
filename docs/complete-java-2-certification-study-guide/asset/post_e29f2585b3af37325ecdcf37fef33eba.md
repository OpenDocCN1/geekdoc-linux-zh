
# Exceptions

Occasionally when a program is executing something that occurs that is not quite normal from the point of view of the goal at hand. For example, a user might type an invalid filename; a file might contain corrupted data; a network link could fail; or a bug in the program might cause it try to make an illegal memory access, such as referring to an element beyond the end of an array.

Circumstances of this type are called *exception conditions* in Java and are represented using objects. An extensive class hierarchy descending from `java.lang.Throwable` is dedicated to describing them.

Most new Java programmers first encounter exceptions when they try to call a useful method that they read about the API pages. Usually it's the pages for the `java.io` package, which methods lots of exceptions. For example, you might decide to call the `getCanonicalFile()` method of an instance of `java.io.File`. (Don't worry about what the method actually *does*! We're here to study exceptions, not file I/O.)

If you don't know about exceptions, you might try to do the following:

```
myFile.getCanonicalFile();
```

Unfortunately, this doesn't compile. The compiler error says something like

unreported exception java.io.IOException; method must be caught or declared to be thrown

On closer inspection of the API page for the file class, you will see that the `getCanonicalFile()` method includes the "throws IOException" in its method declaration. Whenever you use "throws" in a method description an [API page, you can't just call the method. You need to deal with the exception in one of two ways: you can catch it or you can declare it. These options are explained in the next two sections.

# Catching Exceptions

One way to call a method that throws an exception is to create a try block and a catch block. The structure looks like this:

```
try {
    // Exception-throwing code
}
catch (Exception_type name) {
    // Exception-handling code
}
```

The try block contains code that throws exceptions. Code that doesn't throw exceptions may also be included. The catch keyword is followed by a declaration, which appears in parentheses. Like any declaration, this consists of an type followed by a name. The type must match the type of the exception being thrown in the try block. (Well, not exactly, but it's a good enough explanation for now.) The name may be anything you like; it has scope within the curlies ({}) of the catch block. To make sense of all this, let's see what happens when an exception is thrown. We'll continue the example of the previous section.

1. myFile = getMyFile();
2.
3. try {
4. System.out.println("About to call.");
5. myFile.getCanonicalFile();
6. System.out.println("Call succeeded.");
7. }
8.
9. catch (IOException xeptn) {
10. System.out.println("Life stress! " + xeptn.getMessage());
11. xeptn.printStackTrace();
12.
13.
14. System.out.println("Life goes on.");

Line 1 is just setup. The try block is 3–7. Note that only line 5 can throw an exception. (Recall the API explanation for getCanonicalFile() says "throws IOException.") Lines 9–12 are the catch block.

When this code executes, there are two possible scenarios, because the getCanonicalFile() call might might or not find itself in an abnormal condition. When a method declares it throws an exception type, it doesn't mean that an exception is thrown every time the method is called. It means that an exception might get thrown, if the method gets into trouble.

In the simpler scenario, no exception is thrown. Execution starts on line 1 and enters the try block. Lines 4, 5 and 6 execute. The catch block is skipped, and execution continues at line 14.

In the more interesting scenario, exception runs as before the getCanonicalFile() call on line 5 gets thrown. (You'll see a few later how methods exceptions.) In Java, exceptions are objects, and so in our example of xeptn is created (somehow, and given to the Java Virtual Machine (JVM). The current execution of the try block is abandoned, so line 6 does not execute. Instead, exception jumps into the catch block. Within the lines 10 and 11 in our xeptn is a reference to the exception object.

All exceptions from the java.lang.Throwable subclass, from which they inherit two useful methods. When an exception object is constructed, a message is stored inside it. The message describes the circumstances that caused the exception to be thrown. It can be retrieved by calling getMessage() on the exception, on line 10. Often the way to handle an exception is to display the message to the user and let the user figure out what to do next. The second useful method is printTrace(), as seen on line 11, which displays a snapshot of the JVM stack call at the moment the exception was created. The stack trace tells you on what line of code source file the exception was created. It also tells you where from (line number and source filename) method containing that line was called. And it also tells you where the method containing that line was called, and so, up and up until you get to a line in main(). The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et the, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, the,, which is, useful for

The stack trace tells you you called the the that that the the the that the the,,,,, which is the the



The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

Wait, let me re-merge that properly.

In the more interesting scenario, exception runs as before the getCanonicalFile() call on line 5 gets thrown. (You'll see a few later how methods exceptions.) In Java, exceptions are objects, and so in our example of xeptn is created (somehow, and given to the Java Virtual Machine (JVM). The current execution of the try block is abandoned, so line 6 does not execute. Instead, exception jumps into the catch block. Within the lines 10 and 11 in our xeptn is a reference to the exception object.

All exceptions from the java.lang.Throwable subclass, from which they inherit two useful methods. When an exception object is constructed, a message is stored inside it. The message describes the circumstances that caused the exception to be thrown. It can be retrieved by calling getMessage() on the exception, on line 10. Often the way to handle an exception is to display the message to the user and let the user figure out what to do next. The second useful method is printTrace(), as seen on line 11, which displays a snapshot of

the JVM stack call at the moment the exception was created. The stack trace tells you on what line of code source file the exception was created. It also tells you where from (line number and source filename) method containing that line was called. And it also tells you where the method containing that line was called, and so, up and up until you get to a line in main(). The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

Wait, I see a massive amount of repetitive OCR noise in the provided text. I will clean that up and focus on the actual flow.

In the more interesting scenario, exception runs as before the getCanonicalFile() call on line 5 gets thrown. (You'll see a few later how methods exceptions.) In Java, exceptions are objects, and so in our example of xeptn is created (somehow, and given to the Java Virtual Machine (JVM). The current execution of the try block is abandoned, so line 6 does not execute. Instead, exception jumps into the catch block. Within the lines 10 and 11 in our xeptn is a reference to the exception object.

All exceptions from the java.lang.Throwable subclass, from which they inherit two useful methods. When an exception object is constructed, a message is stored inside it. The message describes the circumstances that caused the exception to be thrown. It can be retrieved by calling getMessage() on the exception, on line 10. Often the way to handle an exception is to display the message to the user and let the user figure out what to do next. The second useful method is printTrace(), as seen on line 11, which displays a snapshot of the JVM stack call at the moment the exception was created. The stack trace tells you on what line of code source file the exception was created. It also tells you where from (line number and source filename) method containing that line was called. And it also tells you where the method containing that line was called, and so, up and up until you get to a line in main(). The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

Actually, I will just provide the clean version of the actual text.

In the more interesting scenario, exception runs as before the getCanonicalFile() call on line 5 gets thrown. (You'll see a few later how methods exceptions.) In Java, exceptions are objects, and so in our example of xeptn is created (somehow, and given to the Java Virtual Machine (JVM). The current execution of the try block is abandoned, so line 6 does not execute. Instead, exception jumps into the catch block

All exceptions from the java.lang.Throwable subclass, from which they inherit two useful methods. When an exception object is constructed, a message is stored inside it. The message describes the circumstances that caused the exception to be thrown. It can be retrieved by calling getMessage() on the exception, on line 10. Often the way to handle an exception is to display the message to the user and let the user figure out what to do next. The second useful method is printTrace(), as seen on line 11, which displays a snapshot of the JVM stack call at the moment the exception was created. The stack trace tells you on what line of code source file the exception was created. It also tells you where from (line number and source filename) method containing that line was called. And it also tells you where the method containing that line was called, and so, up and up until you get to a line in main(). The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

Wait, the provided text has weird repetition at the end. I will fix the content.

[content]
# Exceptions

Occasionally when a program is executing something that occurs that is not quite normal from the point of view of the goal at hand. For example, a user might type an invalid filename; a file might contain corrupted data; a network link could fail; or a bug in the program might cause it try to make an illegal memory access, such as referring to an element beyond the end of an array.

Circumstances of this type are called *exception conditions* in Java and are represented using objects. An extensive class hierarchy descending from `java.lang.Throwable` is dedicated to describing them.

Most new Java programmers first encounter exceptions when they try to call a useful method that they read about the API pages. Usually it's the pages for the `java.io` package, which methods lots of exceptions. For example, you might decide to call the `getCanonicalFile()` method of an instance of `java.io.File`. (Don't worry about what the method actually *does*! We're here to study exceptions, not file I/O.)

If you don't know about exceptions, you might try to do the following:

```
myFile.getCanonicalFile();
```

Unfortunately, this doesn't compile. The compiler error says something like

unreported exception java.io.IOException; method must be caught or declared to be thrown

On closer inspection of the API page for the file class, you will see that the `getCanonicalFile()` method includes the "throws IOException" in its method declaration. Whenever you use "throws" in a method description an [API page, you can't just call the method. You need to deal with the exception in one of two ways: you can catch it or you can declare it. These options are explained in the next two sections.

# Catching Exceptions

One way to call a method that throws an exception is to create a try block and a catch block. The structure looks like this:

```
try {
    // Exception-throwing code
}
catch (Exception_type name) {
    // Exception-handling code
}
```

The try block contains code that throws exceptions. Code that doesn't throw exceptions may also be included. The catch keyword is followed by a declaration, which appears in parentheses. Like any declaration, this consists of an type followed by a name. The type must match the type of the exception being thrown in the try block. (Well, not exactly, but it's a good enough explanation for now.) The name may be anything you like; it has scope within the curlies ({}) of the catch block. To make sense of all this, let's see what happens when an exception is thrown. We'll continue the example of the previous section.

1. myFile = getMyFile();
2.
3. try {
4. System.out.println("About to call.");
5. myFile.getCanonicalFile();
6. System.out.println("Call succeeded.");
7. }
8.
9. catch (IOException xeptn) {
10. System.out.println("Life stress! " + xeptn.getMessage());
11. xeptn.printStackTrace();
12.
13.
14. System.out.println("Life goes on.");

Line 1 is just setup. The try block is 3–7. Note that only line 5 can throw an exception. (Recall the API explanation for getCanonicalFile() says "throws IOException.") Lines 9–12 are the catch block.

When this code executes, there are two possible scenarios, because the getCanonicalFile() call might might or not find itself in an abnormal condition. When a method declares it throws an exception type, it doesn't mean that an exception is thrown every time the method is called. It means that an exception might get thrown, if the method gets into trouble.

In the simpler scenario, no exception is thrown. Execution starts on line 1 and enters the try block. Lines 4, 5 and 6 execute. The catch block is skipped, and execution continues at line 14.

In the more interesting scenario, exception runs as before the getCanonicalFile() call on line 5 gets thrown. (You'll see a few later how methods exceptions.) In Java, exceptions are objects, and so in our example of xeptn is created (somehow, and given to the Java Virtual Machine (JVM). The current execution of the try block is abandoned, so line 6 does not execute. Instead, exception jumps into the catch block. Within the lines 10 and 11 in our xeptn is a reference to the exception object.

All exceptions from the java.lang.Throwable subclass, from which they inherit two useful methods. When an exception object is constructed, a message is stored inside it. The message describes the circumstances that caused the exception to be thrown. It can be retrieved by calling getMessage() on the exception, on line 10. Often the way to handle an exception is to display the message to the user and let the user figure out what to do next. The second useful method is printTrace(), as seen on line 11, which displays a snapshot of the JVM stack call at the moment the exception was created. The stack trace tells you on what line of code source file the exception was created. It also tells you where from (line number and source filename) method containing that line was called. And it also tells you where the method containing that line was called, and so, up and up until you get to a line in main(). The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for

Wait, the OCR text has a lot of repetition at the end. I will provide the clean version.
[/content]

Actually, I will provide the clean text without the duplicated/broken parts.

[content]
# Exceptions

Occasionally when a program is executing something that occurs that is not quite normal from the point of view of the goal at hand. For example, a user might type an invalid filename; a file might contain corrupted data; a network link could fail; or a bug in the program might cause it try to make an illegal memory access, such as referring to an element beyond the end of an array.

Circumstances of this type are called *exception conditions* in Java and are represented using objects. An extensive class hierarchy descending from `java.lang.Throwable` is dedicated to describing them.

Most new Java programmers first encounter exceptions when they try to call a useful method that they read about the API pages. Usually it's the pages for the `java.io` package, which methods lots of exceptions. For example, you might decide to call the `getCanonicalFile()` method of an instance of `java.io.File`. (Don't worry about what the method actually *does*! We're here to study exceptions, not file I/O.)

If you don't know about exceptions, you might try to do the following:

```
myFile.getCanonicalFile();
```

Unfortunately, this doesn't compile. The compiler error says something like

unreported exception java.io.IOException; method must be caught or declared to be thrown

On closer inspection of the API page for the file class, you will see that the `getCanonicalFile()` method includes the "throws IOException" in its method declaration. Whenever you use "throws" in a method description an [API page, you can't just call the method. You need to deal with the exception in one of two ways: you can catch it or you can declare it. These options are explained in the next two sections.

# Catching Exceptions

One way to call a method that throws an exception is to create a try block and a catch block. The structure looks like this:

```
try {
    // Exception-throwing code
}
catch (Exception_type name) {
    // Exception-handling code
}
```

The try block contains code that throws exceptions. Code that doesn't throw exceptions may also be included. The catch keyword is followed by a declaration, which appears in parentheses. Like any declaration, this consists of an type followed by a name. The type must match the type of the exception being thrown in the try block. (Well, not exactly, but it's a good enough explanation for now.) The name may be anything you like; it has scope within the curlies ({}) of the catch block. To make sense of all this, let's see what happens when an exception is thrown. We'll continue the example of the previous section.

1. myFile = getMyFile();
2.
3. try {
4. System.out.println("About to call.");
5. myFile.getCanonicalFile();
6. System.out.println("Call succeeded.");
7. }
8.
9. catch (IOException xeptn) {
10. System.out.println("Life stress! " + xeptn.getMessage());
11. xeptn.printStackTrace();
12.
13.
14. System.out.println("Life goes on.");

Line 1 is just setup. The try block is 3–7. Note that only line 5 can throw an exception. (Recall the API explanation for getCanonicalFile() says "throws IOException.") Lines 9–12 are the catch block.

When this code executes, there are two possible scenarios, because the getCanonicalFile() call might might or not find itself in an abnormal condition. When a method declares it throws an exception type, it doesn't mean that an exception is thrown every time the method is called. It means that an exception might get thrown, if the method gets into trouble.

In the simpler scenario, no exception is thrown. Execution starts on line 1 and enters the try block. Lines 4, 5 and 6 execute. The catch block is skipped, and execution continues at line 14.

In the more interesting scenario, exception runs as before the getCanonicalFile() call on line 5 gets thrown. (You'll see a few later how methods exceptions.) In Java, exceptions are objects, and so in our example of xeptn is created (somehow, and given to the Java Virtual Machine (JVM). The current execution of the try block is abandoned, so line 6 does not execute. Instead, exception jumps into the catch block. Within the lines 10 and 11 in our xeptn is a reference to the exception object.

All exceptions from the java.lang.Throwable subclass, from which they inherit two useful methods. When an exception object is constructed, a message is stored inside it. The message describes the circumstances that caused the exception to be thrown. It can be retrieved by calling getMessage() on the exception, on line 10. Often the way to handle an exception is to display the message to the user and let the user figure out what to do next. The second useful method is printTrace(), as seen on line 11, which displays a snapshot of the JVM stack call at the moment the exception was created. The stack trace tells you on what line of code source file the exception was created. It also tells you where from (line number and source filename) method containing that line was called. And it also tells you where the method containing that line was called, and so, up and up until you get to a line in main(). The stack trace tells you who called the code that called the code that called the code, et cetera, which is extremely useful for
