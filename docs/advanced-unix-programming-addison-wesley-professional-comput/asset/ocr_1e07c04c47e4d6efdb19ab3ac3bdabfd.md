A solution for the second problem is to store the number to be printed in a local variable, free the node, and then call printf.

But the first problem has no obvious solution. We have to install a *cancellation cleanup handler*, which is a function that's called just before cancellation to clean thing up. We'll fix the second problem in the cancellation cleanup handler as well.

A cancellation cleanup handler always has this prototype (the name doesn't matter):

```
```c
void cleanup_handler(void *arg);
```
```

A thread installs a cleanup handler with `pthread_cleanup_push` and unstalls it with `pthread_cleanup_pop`:

```
```c
pthread_cleanup_push——install cleanup handler

#include <pthread.h>

void pthread_cleanup_push(
    void (*handler)(void*), /* pointer to cleanup-handler function */
    void *arg               /* data to pass to function */
);```
```

```
```c
pthread_cleanup_pop——uninstall cleanup handler

#include <pthread.h>

void pthread_cleanup_pop(
    int execute /* execute handler? */
);```
```

When cancellation occurs, the cleanup handler is called. If there's more than one, they're all called, in the reverse order of how they were pushed. Each function is popped after it's called, which is fine, since the thread will be gone.

These functions must be paired, and they must be at the same C or C++ block level. If you don't do this, you'll probably get very strange *compile-time errors*, as the functions are usually implemented as macros with embedded braces (like `EC_CLEANUP_BGN` and `EC_CLEANUP_END`; see Section 1.4.2).

Depending on how you've done things, it may make sense to call the cleanup handler even when the thread exits normally. To make that convenient, you can make the `execute` argument to `pthread_cleanup_pop` true.

Here's the improved version of thread_func. Note that I explicitly initialized p to NULL to make sure its value is always valid for free.