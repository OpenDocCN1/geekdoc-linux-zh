```
if (done)
break;
ec_rv( pthread_mutex_lock(&mtx) )
printf("Thread 2 says %ld\\n", ++x);
ec_rv( pthread_mutex_unlock(&mtx) )
sleep(1);
}
return (void *)x;

EC_CLEANUP_BGN
EC_FLUSH("thread_func")
return NULL;
EC_CLEANUP_END
}

int main(void)
{
pthread_t tid;
void *status;
bool done;

assert(sizeof(long) <= sizeof(void *));
ec_rv( pthread_create(&tid, NULL, thread_func, (void *)6) )
while (true) {
ec_rv( pthread_mutex_lock(&mtx) )
done = x >= 10;
ec_rv( pthread_mutex_unlock(&mtx) )
if (done)
break;
ec_rv( pthread_mutex_lock(&mtx) )
printf("Thread 1 says %ld\\n", ++x);
ec_rv( pthread_mutex_unlock(&mtx) )
sleep(2);
}
ec_rv( pthread_join(tid, &status) )
printf("Thread 2's exit status is %ld\\n", (long)status);
return EXIT_SUCCESS;

EC_CLEANUP_BGN
return EXIT_FAILURE;
EC_CLEANUP_END
}
```

Note that we had to pull the conditionals out of the while expressions so that we could surround them with the locking and unlocking calls. We certainly don't want to protect the whole loop, for that would destroy the concurrency. It requires some care to protect enough to be safe but not so much to hurt performance. Unfortunately, while you may be able to detect a performance problem with the