```
exit(EXIT_FAILURE);
}

exit(EXIT_SUCCESS);
}
```

The output from one run of this program follows. As before, it uses the queue ID created by `mkq` and also reads the message posted by the `qsnd` example.

![](bbox=[0.04, 0.22, 0.14, 0.29])

# **Output**

```
$ ./mkq
created queue id = 640
opened queue id = 640
$ ./qsnd 640
Enter message to post:
this is test message number one
message posted

$ ./grd 640
reading queue id: 00640
message type: 14308
    message text: this is test message number one
```

You can see from the code listing that reading from a message queue is easier than writing to one and requires less code. Of particular interest in the sample program is that it fetches the first message off the top of the queue because it passed a `type` of 0. In this case, because the PID of the message writing process is known or can be easily discovered (`14308`), `grd` could have passed a `type` of 14308 and fetched the same message from the queue.

# *Removing Message Queues*

The `msgctl` function provides a certain degree of control over message queues. Its prototype is as follows:

```
int msgctl(int msqid, int cmd, struct msqid_ds *buf);
```

As usual, `msqid` is the queue ID of an existing queue. `cmd` can be one of the following:

+   - `IPC_RMID` —Removes the queue `msqid`.
+   - `IPC_STAT` —Fills `buf` with the queue’s `msqid_ds` structure. `IPC_STAT` enables you to peek into a queue’s contents without removing any messages. Because it is a non-destructive read, you could consider it similar to `msgrcv`.