# Message System Call Interfaces

# sys_msget()

The entire call to `sys_msget()` is protected by the global message queue semaphore (`msg_ids_sem`).

In the case where a new message queue must be created, the `newque()` function is called to create and initialize a new message queue, and the new queue ID is returned to the caller.

If a key value is provided for an existing message queue, then `ipc_findkey()` is called to look up the corresponding index in the global message queue descriptor array (`msg_ids.entries`). The parameters and permissions of the caller are verified before returning the message queue ID. The look up operation and verification are performed while the global message queue spinlock(`msg_ids.ary`) is held.

# sys_msgctl()

The parameters passed to `sys_msgctl()` are: a message queue ID (`msgid`), the operation (`cmd`), and a pointer to a user space buffer of type `msgid_ds` (`buf`). Six operations are provided in this function: `IPC_INFO`, `MSG_INFO`, `IPC_STAT`, `MSG_STAT`, `IPC_SET` and `IPC_RMID`. The message queue ID and the operation parameters are validated; then, the operation(`cmd`) is performed as follows:

# IPC_INFO ( or MSG_INFO)

The global message queue information is copied to user space.

# IPC_STAT ( or MSG_STAT)

A temporary buffer of type `struct msgid64_ds` is initialized and the global message queue spinlock is locked. After verifying the access permissions of the calling process, the message queue information associated with the message queue ID is loaded into the temporary buffer, the global message queue spinlock is unlocked, and the contents of the temporary buffer are copied out to user space by `copy_msgid_to_user()`.

# IPC_SET

The user data is copied in via `copy_msgid_to_user()`. The global message queue semaphore and spinlock are obtained and released at the end. After the the message queue ID and the current process access permissions are validated, the message queue information is updated with the user provided data. Later, `expunge_all()` and `ss_wakeup()` are called to wake up all processes sleeping on the receiver and sender waiting queues of the message queue. This is because some receivers may now be excluded by stricter access permissions and some senders may now be able to send the message due to an increased queue size.

# IPC_RMID

The global message queue semaphore is obtained and the global message queue spinlock is locked. After validating the message queue ID and the current task access permissions, `freemsg()` is called to free the resources related to the message queue ID. The global message queue semaphore and spinlock are released.