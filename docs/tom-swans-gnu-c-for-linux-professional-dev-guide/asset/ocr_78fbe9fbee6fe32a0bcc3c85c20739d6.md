Writing functions that handle errors reliably is always difficult because, for one reason, errors are by nature unpredictable. Worse, as programs become more complex, and therefore invite more intricate error conditions, functions that handle those errors are even more difficult to write and maintain.

Recognizing these problems, C++ designers added the concept of an exception. As you learn in this chapter, an exception is an object that operates with the independence of a satellite in orbit around the earth. It enables a function to report exceptional conditions apart from the function’s normal operation. By incorporating exception handling into C++ programs, it’s easy to manage even the most complex error condition in the most deeply nested chain of function calls.

# A Few Good Terms

Exceptions come with their own terminology and concepts. Following are some overviews that help you to read and understand the information in this chapter:

+   - An exception is just that—it’s an object that describes an exceptional condition requiring special handling. Exceptions are best used for a program’s error handling, but they are not limited to that use.
+   - To create an exception, a function throws an object that describes the nature of the exception. The object can be a string, an object of a class, or any other object. An exception object is not necessarily a class object, but in practice, it usually is.
+   - To handle an exception, a function catches the object thrown as an exception by another function. Statements that catch exceptions are called exception handlers.
+   - Programs prepare to catch exceptions by trying one or more statements that might throw exceptions. In general, to use exceptions, you try one or more statements, and you catch any exceptions those statements throw.

> Note
> Because exceptions are available only in C++, the standard C function library does not report errors using exceptions. However, C++ libraries use exceptions extensively. For more examples of exception handling, see Chapter 25, "Applying Standard Algorithms."

# Introducing Exceptions

Now, let’s see what exceptions look like in C++. Upon detecting an error condition, a function can throw an exception. For example, it might throw a string that describes an error condition:

```
throw "overflow";
```