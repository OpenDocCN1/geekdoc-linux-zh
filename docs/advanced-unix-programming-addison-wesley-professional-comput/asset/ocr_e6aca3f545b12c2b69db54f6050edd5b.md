```
pthread_create—create thread

```
#include <pthread.h>

int pthread_create(
    pthread_t *thread_id,      /* new thread’s ID */
    const pthread_attr_t *attr, /* attributes (or NULL) */
    void *(*start_fcn)(void *), /* starting function */
    void *arg                 /* arg to starting function */
);
/* Returns 0 on success, error number on error */
```
```

The new thread starts with a call to the start function specified in the `pthread_create` call, which must have this prototype:

```
pthread starting function

```
void *start_fcn(
    void *arg
);
/* Returns exit status */
```
```

Whatever you pass as the fourth argument to `pthread_create` is passed directly to the starting function. It’s a `void` pointer for generality, and often it will indeed be a pointer to some data. Since the threads share the same address space, the pointer is valid for both threads. You want, you can also pass in integer data, but you have to cast it to a `void` pointer. And, to be safe, you should check (with an `assert`, say) that the integer type you’re using fits in a `void` pointer, with a line like this that you’ll see in some of the examples that follow:

```
```
assert(sizeof(long) <= sizeof(void *));
```
```

The attributes that affect the new thread are not just some flags but rather an object of type `pthread_attr_t` that you have to set with calls like `pthread_attr_setscope` and `pthread_attr_setstacksize`, which I won’t go into here. (But perhaps you’re beginning to appreciate why there are a hundred thread-related calls.) In our examples we’ll use just default attributes, so our second argument to `pthread_create` will be NULL.

The “pthread” functions uniformly return 0 on success and an error code on failure, rather than setting errno. We have a special “ec” macro for this, `ec_rv`, which takes the error code, if any, and treats it as if it were an `errno` value, which it is.19

> 19. The various functions in the error-checking package were modified to be thread-safe, but the code for that isn’t shown in this book. You’ll see it on the Web site, however.