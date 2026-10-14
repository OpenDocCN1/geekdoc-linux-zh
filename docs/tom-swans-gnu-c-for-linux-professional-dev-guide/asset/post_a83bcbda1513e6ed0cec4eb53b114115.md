
## EXCEPTIONS AND MEMORY MANAGEMENT

As mentioned in prior chapters, operator new throws an exception if it can't fulfill a memory allocation request. In GNU C++, the exception is an object of the class bad_alloc. Suppose that the program has a function f() that uses new to create a dynamic object of type TAnyClass:

```
T AnyClass * f()
{
    return new TAnyClass();
}
```

To trap the exception that new throws if the memory allocation fails, use try and catch statements such as

```
try {
    TAnyClass * p = f();  // Might throw exception
}
catch (bad_alloc error) {
    cout << error.what() << endl;
    exit(1);
}
```

Although the preceding code works, it is inconvenient to trap bad_alloc exceptions at every use of new. Because an out-of-memory condition usually indicates a serious problem, it's more common to trap the error at a higher level—for instance, in main(), using code such as this:

```
int main()
{
    for (;;) {
        try {
            run();  // Main program loop
        }
        catch (bad_alloc error) {
            cout << "Out of memory" << endl;  // ???
            cout << error.what() << endl;  // ???
            exit(1);
        }
    }
}
```

The basic idea is to use a Do-Forever for loop that repeatedly calls a function—run() in this example—that you might refer to as the main program engine. The catch statement traps all bad_alloc exceptions thrown by run(), or by any other functions that run() calls. However, the output statements are questionable because, if the system is out of memory, there might not be enough free bytes left to execute the output statements themselves. If an exception occurs during the output statements, the program calls terminate() and ends abruptly with a core dump.

A useful trick that can alleviate this kind of trouble is to allocate a pool of memory at the start of the program to be deleted in the event of a memory allocation failure. For example, you might reserve a block of 2,048 bytes:

```
char *reserve = new char[2048];
```

That might also be in a try block, but there’s usually some memory available when the program begins running. In the event of a bad_alloc exception, delete the reserved memory:

```
delete reserve;
reserve = NULL;
```

You can then repeat the operation that led to the error in hopes that the use of new will succeed. If not, another bad_alloc exception is thrown, and you might have to abort the program. One way to do that is to handle and then rethrow the exception:

```
catch (bad_alloc error) {
    if (reserve != NULL)
        throw (error);
}
```

That causes the exception object to remain alive outside the exception handler, and unless there’s another handler higher up in the function-call chain, the program eventually calls the current unexpected exception handler. In that handler, you could perform an orderly shutdown, close files, and do whatever else is necessary before ending the program.

## DEBUGGING EXCEPTIONS

The GNU debugger offers one command for trapping exceptions, but it seems not to work in the release I’m using. However, you might try it with a newer compiler—perhaps it will work for you. First, compile a program such as unexpect.cpp in this chapter (refer to Listing 16.4) and load it into the debugger using these commands:

```
$ g++ -g -o unexpect unexpect.cpp
$ gdb --silent unexpect
(gdb)
```

Set a breakpoint on function main() by specifying its name to the break command (abbreviated simply as b), and then run the program:

```
(gdb) b main
Breakpoint 1 at 0x80489ee: file unexpect.cpp, line 40.
(gdb) run
Starting program: /src/c16/unexpect
Breakpoint 1, main () at unexpect.cpp:40
40 set_unexpected( custom_unexpected );
```

## SUMMARY

As this chapter explained, C++ exceptions are objects that functions can throw to report exceptional conditions. To provide exception handling, programs call functions in try blocks, followed by catch statements for the types of exception objects those functions might throw. Any unhandled exceptions call low-level unexpected() and terminate() functions that you can replace with custom versions to trap all possible errors and prevent programs from shutting down unexpectedly. This chapter also explained related topics such as rethrowing an exception, deriving classes from the standard exception class, and writing exception handlers for out-of-memory errors reported by the C++ new operator.

For more information on subjects introduced in this chapter, turn to the following chapters:

- Chapter 22, “Mastering the Standard string Class”
- Chapter 25, “Applying Standard Algorithms”
