So we have to look for “”end-of-file.””

To make things easier, we’ll code functions to handle interaction with the editor. At the start of processing we call `edinvoke` to invoke the editor and set up the pipes. Instead of using the file descriptors directly, which would require us to do I/O with `read` and `write`, we create Standard C `FILE` pointers instead, using `fdopen`. We can then write to the editor on `sndfp` and read from the editor on `rcvfp`. Here is `edinvoke`, which is a lot like the first part of `fsort`:

```
```
static FILE *sndfp, *rcvfp;
static bool edinvoke(void)
{
    int pfdout[2], pfdin[2];
    pid_t pid;

    ec_negl( pipe(pfdout) )
    ec_negl( pipe(pfdin) )
    switch (pid = fork()) {
    case -1:
        EC_FAIL
    case 0:
        ec_negl( dup2(pfdout[0], STDIN_FILENO) )
        ec_negl( dup2(pfdin[1], STDOUT_FILENO) )
        ec_negl( close(pfdout[0]) )
        ec_negl( close(pfdin[1]) )
        ec_negl( close(pfdout[1]) )
        ec_negl( close(pfdin[0]) )
        execlp("ed", "ed", "-", (char *) NULL);
        EC_FAIL
    }
    ec_negl( close(pfdout[0]) )
    ec_negl( close(pfdin[1]) )
    ec_null( sndfp = fdopen(pfdout[1], "w") )
    ec_null( rcvfp = fdopen(pfdin[0], "r") )
    return true;

EC_CLEANUP_BGN
    if (pid == 0) {
        EC_FLUSH("edinvoke");
        _exit(EXIT_FAILURE);
    }
    return false;
EC_CLEANUP_END
}
```
```