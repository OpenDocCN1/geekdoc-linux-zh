right kind of testing, it’s much harder to test whether you’ve prevented all race conditions.

We still have a defect: Suppose in pthread_func the call to pthread_mutex_unlock fails, causing the thread to exit. This might leave the mutex locked, causing the initial thread to block forever in one of its calls to pthread_mutex_lock. A potential solution is to make sure the mutex is unlocked in pthread_func’s cleanup code, with another call to pthread_mutex_unlock, like this:

```
```
EC_CLEANUP_BGN
    (void)pthread_mutex_unlock(&mtx);
    EC_FLUSH("thread_func")
    return NULL;
EC_CLEANUP_END
```
```

We’re assuming that if the first call to pthread_mutex_unlock failed, the second one might succeed, which seems like a stretch. Since there is really no way either pthread_mutex_lock or pthread_mutex_unlock can fail as long as the mutex has a valid value, probably the easiest, safest, and clearest way to proceed is to check the error return from these functions during debugging, but not in the production program. Or, you might decide that for your application it’s better to leave the error checks in, as long as you get a report of the error, so you don’t waste time trying to find out why the application stalled. This is another example of why threads can be very tricky to use correctly. You may find that you spend 5% of your time implementing the threads and 95% of your time ensuring that you’ve done it right.

The proper way to proceed is to encapsulate the access to shared data with a collection of functions (or with a class, if you’re using an object-oriented language like C++ ) with the mutexes in the access functions. Don’t spread the locking and unlocking calls willy-nilly throughout your program, as I did.

So I’ll show the example rewritten yet again, this time with all access to x going through a single function, get_and_incr_x, which does all the locking and unlocking. Both x and the mutex have been moved inside the function. Notice how much more readable this version is than the previous one. More readable almost always implies more reliable!

```
```
static long get_and_incr_x(long incr)
{
    static long x = 0;
    static pthread_mutex_t mtx = PTHREAD_MUTEX_INITIALIZER;
    long stn;
```
```