# Parameters

| `thread` | The thread handle (passed by reference). If successful, the call places the thread handle in this parameter. |
| `attr` | The thread's starting attributes. See `pthread_attr_init` for more information. |
| `start_fn` | The routine in which the thread is to start. This function should return a `void*` value. |
| `arg` | The parameter passed to `start_fn`. You should make this parameter a nonshared (unless you plan on locking it), nonstack memory reference. |

# Possible Errors

| `EAGAIN` | Not enough system resources to create a process for the new thread. |
| `EAGAIN` | More than `PTHREAD_THREADS_MAX` threads are already active. |

# Example

```
```c
void* child(void *arg)
{
    /**** Do something! ****/
    pthread_exit(arg); /* terminate and return arg */
}
int main()
{
    pthread_t tchild;
    if (pthread_create(&tchild, 0, child, 0) < 0 )
        perror("Can't create thread!");
    /**** Do something! ****/
    if (pthread_join(tchild, 0) != 0 )
        perror("Join failed");
}
```
```

# `pthread_join()`

Similar to the `wait()` system call, this call waits for and accepts the return value of the child thread.

# Prototype

```
```c
#include <pthread.h>
int pthread_join(pthread_t tchild, void **retval);
```
```

# Return Value

A positive value if successful. If the thread-create call encountered any errors, the call returns a negative value and sets `errno` to the error.

# Parameters

| `thread` | The thread handle to wait on |
| `retval` | The pointer to the value passed back (passed by reference) |

# Possible Errors