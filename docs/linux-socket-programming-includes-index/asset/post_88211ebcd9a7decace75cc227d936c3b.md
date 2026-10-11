
## struct proc_res

```c
struct proc_res
{
int Err;
union
{
char *Data;
} proc_res_u;
};
```

The union is very useful if you want to send back a specific error code without tripping up the XDR routines. The server-side code always returns a pointer to the result, not the result itself. If the server fails, it returns a NULL. First, a NULL is not very descriptive, and second, the lower-level calls may intercept a NULL return.

The next example uses the union structure to either return the information from a file in /proc or an error code. The full X file is as follows:

```text
/*** RPC_PROC X File declaration ***

union proc_res switch (int Err)
{
case 0: /****no error, return string ****/
string Data<>; /****no limit****/
default: /*--if error, return nothing--*/
void;
};

program RPCPROC
{
version RPCPROCVESION
{
proc_res READPROC(string) = 1; /****/proc filename ****/
} = 2000025;
}
```

The server accepts the filename that points in the /proc virtual file system and opens the file. If no error occurs, the server reads the contents, closes the file, and returns the result. You can run into a little problem here. First, the server returns the reference to the result, so the data must not be on the stack. All return values are made static to ensure that the data is still around. However, strings are always converted into char*.

When you fill your return record, you must allocate memory to insert strings. This means that you must somehow free up the memory; otherwise, your program develops memory leaks. The XDR routines offer a way to clean up from the previous call:

```c
xdr_free((xdrproc_t)xdr_proc_res, (void*)&result);
```

The only parameter that changes is the xdr_<return-type> (xdr_proc_res, in this case). You always call this function before doing anything else. It is smart enough not to do anything if called the first time. (For a complete listing of the algorithm and files for this program, please refer to the Sams Publishing Web site.)

## Adding Records and Pointers to the Fray

The last type should be very familiar. The struct is identical to C's record declaration and fills the same purpose. But, the struct serves an additional purpose. Using the rpcgen toolset has a significant (but not intractable) limitation: You cannot pass more than one parameter through a service call. All multiple parameter calls must use records to pass in and out the data.

A structure definition is as follows:

```c
/*** RPC RPCList X File snippet ***

typedef struct NodeStruct *TNode;
struct NodeStruct
{
string Name<>;
TNode Next;
};
```

You may notice that the structure has a pointer type (*TNode*) in the body. If you recall, the earlier part of the chapter stated that you cannot send pointers over the network—the memory spaces are not the same, so a pointer reference is meaningless. The rpcgen XDR is very smart: it copies and translates all pointer references in a complex structure so that the client or server can understand the results. You can send trees, linked lists, and any non-looping dynamic memory storage.

The only strangeness is the syntax in the X file. A pointer type must be declared as a *typedef*:

```c
/*** RPC syntax example ***

typedef struct NodeStruct Tnode;
struct NodeStruct
{
string Name<>;
TNode *Next; /*--- This is not legal ---*/
};
```

The Sams Web site has several examples, including an RPC *ps* command that ships the information back in a dynamically allocated table with rows and fields.

## Creating Non-Stateless Calls with Open Connections

Passing information back and forth from the client to the server involves much more than the data. Each program often has to keep track of the machine state in order to respond correctly to a request. The previous sections focused on programs that assume nothing about other calls; they also refer to another type of call. Each call is typically independent from every other (a stateless connection). This is not very useful if you have to maintain some kind of information from call to call.

For lack of a better term, a *stateful* (or non-stateless) connection must retain some kind of information so that proper communications can occur. A couple examples of this are logins (the person must be logged in before he gets any data) and database transactions (the server may not transmit the entire table all at once).

The first course of action is to answer these questions: “Why are stateless connections common?” and “Why are stateful connections a burden?”

### Diagnosing the State Problem

The stateless connection is simple. The client sends information, and the server replies with the answer. If the question is lost, the client simply asks again. That approach falls very short of the needs of a stateful connection.

The stateful connection has to maintain a relationship. As noted in earlier sections and chapters, a server and client make sure that the handshake is deterministic and recoverable. The problems with stateful connection include the following:

- **Current State**—The session must keep track of the actions already performed. No one likes to answer questions or jump through the same hoops over and over.
- **State Path or Route**—The session must clearly have a particular path or route. The steps forward and back must be deterministic and clear. If not, state recovery or next steps become uncertain or confused.
- **State Recovery**—If a state is lost the system may need to roll back to a previously known state. Even if connections drop, the client and server must pick up where they left off. As a last resort, both systems must be able to completely undo the transactions up to the point of disconnection.

The state problem must address each of these issues. In some cases, recovery is moot. But, overall, the client and server must uniquely identify each other’s current session.

## Remembering Where You Are

The simplest stateful connection is one that keeps track of the current state. You can do this with a session ID. This ID must be encoded so that only the client and server understand the significance of it. As a simple example, the client requests the first row of a database query result. To get the next row, the server must be able to associate the next call with the initial query.

A simple way to address this problem is to divide up the calls into at least three phases: initialize, transact, and terminate. The sole purpose of the initialization state should be to establish the session and begin the processing. The transaction-based calls manipulate the state that the initialization started. And, the termination state flushes any pending transactions, closes the connection, and secures the data.

After the session is closed, the session ID is no longer valid.

## Following a Specific Route

The three primary states—initialize, transact, and terminate—are the beginnings of providing a state route map. The state route map shows all the states and how to get between them. Given the current information about the session, the server and client know exactly what they can do and how to get to the next state.

Determinism in a state map means that you must have unique states and unique transitions. Specifically:

- No single transition leads to disparate states—Example: If the server changes directory, the client must reflect the change.
- No two states can have the same transition—Example: A transaction cannot result in both the client and the server waiting for a message.

Without the predictability that determinism provides, you cannot recover from any state failure.

## Recovering from a State Failure

Of the three different problems that stateful connections face, recovering from state failure is the most difficult. The network particularly introduces many different ways to lose state. Some state loss causes include hardware, routing, connectivity, program defects, and so on. The first problem is recognition.

State loss can be a nasty problem if you do not plan for it. First, both programs must check each other’s session ID. The session ID must also include some level of security, expiration, and state identification. You can even include the last state and potential next states. If any of these keys gets out of sync, your program can determine that state has been lost.
