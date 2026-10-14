# EXCEPTIONS AND MEMORY MANAGEMENT

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