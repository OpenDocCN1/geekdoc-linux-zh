item was created using two calls to $malloc( )$ , one for the list item itself, represented by struct _blist_ just shown, and one for the variable data item. We then generated 10,000 records on the list containing variable string data, resulting in 20,000 calls to $malloc( )$ .

To use *mtrace*, three conditions must be satisfied:

+   * A header file, *mcheck.h*, must be included in the source file.
+   * The application must call *mtrace( )* to install the handlers.
+   * The environment variable MALLOC_TRACE must specify the name of a writable file to which the trace data is written.

When these conditions are satisfied, each call to one of the traced functions generates a line in the raw trace file defined by MALLOC_TRACE. The trace data looks like this:

```
0 ./mt_ex: {0x80486ec} + 0x804a5f8 0x10
```

The @ sign signals that the trace line contains an address or function name. In the previous example, the program was executing at the address in square brackets, 0x80486ec. Using binary utilities or a debugger, we could easily associate this address with a function. The plus sign (+) indicates that this is a call to allocate memory. A call to $free( )$ would be indicated by a minus sign. The next field indicates the virtual address of the memory location being allocated or freed. The last field is the size, which is included in every call to allocate memory.

This data format is not very user friendly. For this reason, the *mtrace* package includes a utility* that analyzes the raw trace data and reports on any inconsistencies. In the simplest case, the Perl script simply prints a single line with the message “No memory leaks”. Listing 13-12 contains the output when memory leaks are detected.