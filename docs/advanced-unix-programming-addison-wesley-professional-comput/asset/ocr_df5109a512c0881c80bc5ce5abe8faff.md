# **SMI types**—types for SMI

```
```
typedef void *SMIQ;          /* message queue */
typedef enum {
    SMI_SERVER,              /* server */
    SMI_CLIENT               /* client */
} SMIDENTITY;
#define SERVER_NAME_MAX 50  /* max size of server name */
```
```

# **smi_open**—open SMI message queue

```
```
SMIQ *smi_open(
    const char *name,        /* server name */
    SMIDENTITY entity,       /* entity being opened */
    size_t msize             /* fixed message size */
);
/* Returns pointer to message queue or NULL on error (sets errno) */
```
```

# **smi_close**—close SMI message queue

```
```
bool smi_close(
    SMIQ *sqp               /* queue */
);
/* Returns true on success or false on error (sets errno) */
```
```

The message-queue name passed to `smi_open` must be known to the server and all clients. If the implementation needs to create it before opening it, this is done behind the scenes inside `smi_open`. There aren't any permissions in this simple interface, which is one of the many reasons why it's called "simple." Whether the message queue is left around after it's closed isn't specified as part of the interface and is also up to the implementation.

The *entity* argument is either `SMI_SERVER` or `SMI_CLIENT`, depending on which kind of program is doing the opening. There can be only one server process but an undefined number of clients.

The *msgsize* argument is the size of the `smi_data` member of the `smi_msg` structure, for all messages. As I mentioned, there's no provision for messages being of different sizes.

For sending and receiving, we could just pass an address of a buffer to simple send and receive functions, something like `write` and `read`, like this (no size argument because it's a fixed number):

```
```
ec_false( smi_send(sqp, buffer) )
...
ec_false( smi_receive(sqp, buffer) )
```
```