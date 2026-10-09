```
          } = 2000025;
```

The server accepts the filename that points in the /proc virtual file system and opens the file. If no error occurs, the server reads the contents, closes the file, and returns the result. You can run into a little problem here. First, the server returns the reference to the result, so the data must not be on the stack. All return values are made static to ensure that the data is still around. However, strings are always converted into `char*` .

When you fill your return record, you must allocate memory to insert strings. This means that you must somehow free up the memory; otherwise, your program develops memory leaks. The XDR routines offer a way to clean up from the previous call:

```
xdr_free((xdrproc_t)xdr_proc_res, (void*)&result);
```

The only parameter that changes is the xdr_&lt;return-type&gt; (xdr_proc_res, in this case). You always call this function before doing anything else. It is smart enough not to do anything if called the first time. (For a complete listing of the algorithm and files for this program, please refer to the Sams Publishing Web site.)

# ## Adding Records and Pointers to the Fray

The last type should be very familiar. The `struct` is identical to C’s record declaration and fills the same purpose. But, the `struct` serves an additional purpose. Using the rpcgen toolset has a significant (but not intractable) limitation: You cannot pass more than one parameter through a service call. All multiple parameter calls must use records to pass in and out the data.

A structure definition is as follows:

```
/***********************************/
/**  RPC RgCList X File snipet    ***/
/***********************************/
typedef struct NodeStruct *TNode;
struct NodeStruct
{
    string Name<>;
    TNode Next;
} ;
```

You may notice that the structure has a pointer type (TNode) in the body. If you recall, the earlier part of the chapter stated that you cannot send pointers over the network—the memory spaces are not the same, so a pointer reference is meaningless. The `rpcgen` XDR is very smart; it copies and translates all pointer references in a complex structure so that the client or server can understand the results. You can send trees, linked lists, and any non-looping dynamic memory storage.

The only strangeness is the syntax in the X file. A pointer type must be declared as a typedef:

```
/***********************************/
```