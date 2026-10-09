# 7.3.1  SMI Types and Functions

I'm just going to explain the interface in this section; the specific implementations come later. First, here's the generalized message structure:

```
```
struct smi_msg—structure for SMI

struct smi_msg {
long smi_mtype; /* must be first */
struct client_id {
long c_id1;
long c_id2;
} smi_client;
char smi_data[1];
};
```
```

The first two members, `smi_mtype` and `smi_client`, are required by some of the implementations, as we shall see. We've already seen, in the example in Section 7.2.2, that a client has to pass its process ID to the server; in an SMI message, this goes into the `client.c1_id1` member. We'll see `smi_mtype` and `smi_client.c_c_id2` used later on.

The message data (`smi_data`) can be anything at all, with these restrictions:

+   - Server and client may be on different machines, so no pointers or other data that isn't meaningful across a network should be passed.
+   - As different machines have different byte ordering, binary numbers need to be expressed in a network-standard format. This topic is explored in Section 8.1.4.

In this simple interface, server and client have to agree on the fixed message size, and the actual size of the `smi_data` array depends on that size. Once you've mastered the principles in this and the next chapter, you can investigate relaxing that limitation in your own version of the SMI that you use in your own applications.

Before sending or receiving, a server or client has to open a message queue, which should be closed upon termination. Conceptually, sent messages are put on the queue, and received messages are taken from the queue. What a queue actually is is implementation dependent and is hidden inside the SMI implementation, much as the internals of a FILE type are hidden by the Standard C I/O functions.

The opening and closing interfaces are: