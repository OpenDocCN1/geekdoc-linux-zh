The Python interpreter is not fully thread-safe. In order to support multi-threaded Python programs, there’s a global lock, called the global interpreter lock or GIL, that must be held by the current thread before it can safely access Python objects. Without the lock, even the simplest operations could cause problems in a multi-threaded program: for example, when two threads simultaneously increment the reference count of the same object, the reference count could end up being incremented only once instead of twice.

Therefore, the rule exists that only the thread that has acquired the GIL may operate on Python objects or call Python/C API functions. In order to emulate concurrency of execution, the interpreter regularly tries to switch threads. The lock is also released around potentially blocking I/O operations like reading or writing a file, so that other Python threads can run in the meantime.

The major impact this has in terms of Python performance is that Python threads cannot take advantage of multiprocessor or multicore processor architectures. Thread switching can only occur between the execution of individual bytecodes in the interpreter. The frequency with which the interpreter checks for thread switching is set by the sys.setcheckinterval() function. By default, the interpreter checks for thread switching after every 100 bytecode instructions.

When working with extension modules, the interpreter may invoke functions written in C. Unless specifically written to interact with a threaded Python interpreter, these functions block the execution of all other threads until they complete execution. Thus, a long-running calculation in an extension module may limit the effectiveness of using threads. However, most of the I/O functions in the standard library have been written to work in a threaded environment.

# 16.4.4.1 Python Thread Examples Using the Functional Programming Paradigm

We show both the thread (_thread in Python 3.X) and threading modules, and the examples we present in this section use the thread module.

Unless you need the more powerful OOP tools and capabilities in the threading module, the choice is largely a matter of programmer and programming team preference, and programming design goals/methodologies. We cover some of the functions offered in the threading module in Section 16.4.5.

The basic thread module does not impose OOP, and is very easy to use if you are used to functional programming. As mentioned, the thread module has been renamed to _thread in Python 3.

This module provides low-level primitives for working with multiple threads of control (also called lightweight processes or tasks) that share their global data space. For synchronization, simple locks (also called mutexes) are provided.

# 16.4.4.1.1 thread Functions Reference

The thread module defines the following constants and functions:

```
exception thread.error: Raised on thread-specific errors.
```

```
thread.LockType: This is the type of lock object.
```