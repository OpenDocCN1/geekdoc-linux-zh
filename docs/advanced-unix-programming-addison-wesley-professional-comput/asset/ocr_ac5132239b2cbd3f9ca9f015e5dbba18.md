is the same as what we did in Section 7.5.3. It creates the name if it doesn't already exist, and any problems with the name are reported as problems with `ftok`, not with `open` or `close`. (If you don't like that, you can check the `open` for an error other than `ENOENT` separately, instead of embedding it in an immediate call to `close`.)

Then we do a `semget` with the `IPC_CREAT` and `IPC_EXCL` flags so that it will fail if the semaphore already exists. All processes and threads for which it failed for that reason need to wait for it to be initialized. The process or thread that got a successful return from `semget` uses `semctl` to initialize it, and then it does a `semop` (which I'll explain shortly) that doesn't do anything to the value, but as a side-effect sets the `sem_otime`.

Processes and threads that need to wait will loop until a `semget` succeeds, sleeping each time, and then looping again until the time becomes nonzero, also sleeping each time.

For System V semaphores, `SimpleSemClose` doesn't do much:

```
```
bool SimpleSemClose(struct SimpleSem *sem)
{
    free(sem);
    return true;
}
```
```

To remove a simple semaphore, you call `SimpleSemRemove`:

> **SimpleSemRemove**—remove simple semaphore
> 
> ```c
> #include "SimpleSem.h"
> 
> bool SimpleSemRemove(
>       struct SimpleSem *sem       /* semaphore */
> );
> /* Returns true on success or false on error (sets errno) */
> ```

It's OK to call `SimpleSemRemove` on a semaphore that doesn't exist—that's not considered an error. In fact, that's exactly what you should do when an application starts up and you want to start with a fresh semaphore.

Here's the code for `SimpleSemRemove`:

```
```
bool SimpleSemRemove(const char *name)
{
    key_t key;
    int semid;
```
```