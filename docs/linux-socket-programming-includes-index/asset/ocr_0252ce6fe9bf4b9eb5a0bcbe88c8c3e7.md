The only parameter that changes is the xdr_<return-type> (xdr_proc_res, in this case). You always call this function before doing anything else. It is smart enough not to do anything if called the first time. (For a complete listing of the algorithm and files for this program, please refer to the Sams Publishing Web site.)

# Adding Records and Pointers to the Fray

The last type should be very familiar. The struct is identical to C's record declaration and fills the same purpose. But, the struct serves an additional purpose. Using the rpcgen toolset has a significant (but not intractuable) limitation: You cannot pass more than one parameter through a service call. All multiple parameter calls must use records to pass in and out the data.

A structure definition is as follows:

```
/****...*****/
/*** RPC RPCList X File snippet ***
/****...*****/
typedef struct NodeStruct *TNode;
struct NodeStruct
{
string Name<>;
TNode Next;
};
```

You may notice that the structure has a pointer type (*TNode*) in the body. If you recall, the earlier part of the chapter stated that you cannot send pointers over the network—the memory spaces are not the same, so a pointer reference is meaningless. The rpcgen XDR is very smart: it copies and translates all pointer references in a complex structure so that the client or server can understand the results. You can send trees, linked lists, and any non-looping dynamic memory storage.

The only strangeness is the syntax in the X file. A pointer type must be declared as a *typedef*:

```
/****...*****/
/*** RPC syntax example ***
/****...*****/
typedef struct NodeStruct Tnode;
struct NodeStruct
{
string Name<>;
TNode *Next; /*--- This is not legal ---*/
};
```

The Sams Web site has several examples, including an RPC *ps* command that ships the information back in a dynamically allocated table with rows and fields.