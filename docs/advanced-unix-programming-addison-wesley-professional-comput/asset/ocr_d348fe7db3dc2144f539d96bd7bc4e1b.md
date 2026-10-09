```
```c
static void cleanup_handler(void *arg)
{
    free(arg);
    (void)pthread_mutex_unlock(&mtx);
}

static void *thread_func(void *arg)
{
    struct node *p = NULL;

    pthread_cleanup_push(cleanup_handler, p);
    while (true) {
        ec_cv( pthread_mutex_lock(&mtx) )
        while (head == NULL)
            ec_cv( pthread_cond_wait(&cond, &mtx) )
        p = head;
        head = head->next;
        printf("Got %d from front of queue\n", p->n_number);
        free(p);
        ec_cv( pthread_mutex_unlock(&mtx) )
    }
    pthread_cleanup_pop(false);
    return (void *)true;
}

EC_CLEANUP_BGN
    (void)pthread_mutex_unlock(&mtx);
EC_FLUSH("thread_func")
return (void *)false;
EC_CLEANUP_END
```
```

Now we should be OK. Note that the whole complication of dealing with cancellation could have been avoided if I chose some other way to terminate the thread once the initial thread had stopped putting nodes on the queue. That’s something to consider in your own applications—don’t use cancellation when a less ruthless action will do the job. On the other hand, if the thread to be terminated is blocked (in read, say) and you can’t very easily get it unblocked, thread cancellation may be the best choice. It’s certainly a better choice than a signal, which also can unblock a system call; as we shall see in Chapter 9, signals have much worse side effects.

# **5.17.6 Threads vs. Processes**

You’re probably wondering when you should use threads vs. processes. Generally, you use threads when you want concurrent processing on the same complex data structures. Three common situations are: