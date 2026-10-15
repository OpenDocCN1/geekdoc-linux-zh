```
/* Join all threads and print sum */
for ( t = 0 ; t < num_threads; t++) {
    pthread_join(threads[t], (void**) NULL);
}

printf("The array total is %8.2f\n", total);

/* Free all memory allocated to program */
free ( threads );
free ( thread_data );
free ( a_vector );
free ( b_vector );

return 0;
}
```

# 10.6.7 Other Types of Mutexes

The type of a mutex is determined by the mutex attribute structure used to initialize it. There are four possible mutex types:

PTHREAD_MUTEX_NORMAL

PTHREAD_MUTEX_ERRORCHECK

PTHREAD_MUTEX_RECURSIVE

PTHREAD_MUTEX_DEFAULT

The default type is always PTHREAD_MUTEX_DEFAULT, which is usually equal to PTHREAD_MUTEX_NORMAL. To set the type of a mutex, use

```
int pthread_mutexattr_settype(pthread_mutexattr_t *attr, int type);
```

passing a pointer to the mutexattr structure and the type to which it should be set. Then you can use this mutexattr structure to initialize the mutex.

There is no function that, given a mutex, can determine the type of that mutex. The best one can do is to call

```
int pthread_mutexattr_gettype(const pthread_mutexattr_t *restrict attr,
    int *restrict type);
```

which retrieves the mutex type from a mutexattr structure. But, since there is no function that retrieves the mutexattr structure of a mutex, if you need to retrieve the type of the mutex, you must access the mutexattr structure that was used to initialize the mutex to know the mutex type.

When a normal mutex is accessed incorrectly, undefined behavior or deadlock result, depending on how the erroneous access took place. A thread will deadlock if it attempts to re-lock a mutex that it already holds. But if the mutex type is PTHREAD_MUTEX_ERRORCHECK, then error checking takes place instead of deadlock or undefined behavior. Specifically, if a thread attempts to re lock a