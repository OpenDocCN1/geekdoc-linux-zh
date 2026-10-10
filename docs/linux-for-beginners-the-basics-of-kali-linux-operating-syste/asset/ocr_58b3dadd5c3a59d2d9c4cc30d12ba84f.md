```
void pthread_exit (void * retval);
```

The retval parameter specifies the return code. Here is an example of ending a stream:

```
void * turead_fun( void * num )
{
printf( " stream number % d \ n", (int) num);
pthread_exit(0);
}
```

There are two different situations for the application startup code:

+   ◆  Executing the return statement or executing all statements by the end of main () completes the whole process with all threads also completing their execution

+   ◆  Executing the pthread_exit () function inside the main () function completes only the initial thread, this action does not affect other threads in the program - they will continue executing until they are completed

Calling the pthread_exit () function is used only to join threads because it does not release the flow resources - this is the responsibility of the threaded joiner.

# ## Waiting For Completion Of Threads

To await completion of threads, use the pthread_join () function. It has the following syntax:

```
int pthread_join (pthread_t the ,, void ** status);
```

This function blocks the thread where it was called until the thread specified by the handle deserves its execution. If the status is not a null pointer, it will point to the data returned by the stream after the call (argument pthread_exit ()). If the thread is already complete by the time the pthread_join () function is called, its information should be read immediately.