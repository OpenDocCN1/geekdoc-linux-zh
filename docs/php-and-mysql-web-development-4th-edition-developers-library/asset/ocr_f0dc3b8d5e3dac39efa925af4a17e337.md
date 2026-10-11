perform operations related to the name. For example, you can construct a lock name based on a unique key value for a row in a table to enable cooperative locking of that row.

To release a lock explicitly, call `RELEASE_LOCK( )` with the lock name:

```
RELEASE_LOCK('Mel1ie')
```

+   RELEASE_LOCK( ) returns 1 if the lock was released successfully, 0 if the lock was held by another connection (you can release only your own locks), or NULL if no such lock exists.

Any lock held by a client is automatically released if the same client issues another GET_LOCK( ) call, because only one string at a time can be locked per client connection. In this case, the lock being held is released before the new lock is obtained, even if the lock name is the same. A lock also is released when the client's connection to the server terminates. Note that if you have a very long-running client and its connection times out due to inactivity, any lock held by the client is released.

To test the status of a lock name, you have two options:

+   Invoke `IS_FREE_LOCK(str)`, which returns 1 if the name is available (not currently being used as a lock), 0 if the name is in use, or NULL if an error occurred.

+   Invoke `IS_USED_LOCK(str)`, which returns NULL if there is no lock or the connection ID of the client that holds it if there is one.

You can also use `GETLOCK(str, 0)` as a simple poll to determine without waiting whether a lock on `str` is in force. However, this has the side effect of locking the string if it is not currently locked, so you must remember to call `RELEASE_LOCK( )` as appropriate. All advisory locking functions return NULL if the lock name argument is NULL.

+   `GET_LOCK(str, timeout)`
+   
+   Attempt to acquire an advisory lock with the name indicated by the string `str` within a timeout value of `timeout` seconds. `GET_LOCK( )` returns 1 if the lock was obtained successfully within the timeout period, 0 if the lock attempt failed due to timing out, or `NULL` if an error occurred.

+   `IS_FREE_LOCK(str)`
+   
+   Checks the status of the advisory lock named by `str`. Returns 1 if the name is available (not currently being used as a lock), 0 if the name is in use, or `NULL` if an error occurred.

+   `IS_USED_LOCK(str)`
+   
+   If there is a lock with the name given by `str`, `IS_USED_LOCK( )` returns the connection ID of the client that created the lock. Returns `NULL` if there is no such lock.

+   `RELEASE_LOCK(str)`
+   
+   Releases the advisory lock named by `str`. Returns 1 if the lock was released successfully, 0 if the lock was held by another connection, or `NULL` if no such lock exists.