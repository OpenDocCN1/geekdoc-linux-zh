flows; then call the AI to handle the flow ( thread handle )

+   Attr is a pointer to a structure with flow attributes (you need to pass a null pointer to use the default attributes; some attributes will be reviewed later)

+   thread _ fun is a pointer to a stream function that should be described as
+   g void *mythread_fun ( void * value )
+   {

```
void *mythread_fun ( void * value )
{
    // executing the stream code
}
```

+   arg - the data passed to the stream function (there they will get a parameter value )

An example of creating a POSIX stream:

```
# include < pthread . h >
// flow function
void * thread_fun ( void * num )
{
    printf ( " stream number % d \ n", (int) num );
}
// ..........................
pthread_t th;
// create the second thread
pthread_create (& th, NULL, thread_fun, (void *) ++ thread_num );
// there are two threads running in parallel
```

The new thread begins to run in parallel with the thread that created it. For example, if a thread was created inside the main () function, then two threads would continue to execute: an original program executing the main () code and a new one.

# ## Completion of POSIX Streams

To end a thread, just go to the end of its thread function thread thread _ fun () or call pthread_exit () from it:

```
# include < pthread.h >
```