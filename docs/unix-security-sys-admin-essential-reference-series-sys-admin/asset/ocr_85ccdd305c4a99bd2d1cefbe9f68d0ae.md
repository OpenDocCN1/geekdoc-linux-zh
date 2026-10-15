There is one extra risk to SUID root programs. Because they usually start out running from the user's account, they need to be very careful about setting their $PATH, their shared library search path, and so on. In our case, we always run out of an account under control of the systems administrator, so we merely need to make the environment the same as root's. For that reason, passwd is the account's shell, with a very minimal environment.

```
/*
 * error reporters -- for open, existence and write errors.
 */
sayExists(outFile) char *outFile; {
    (void) fprintf(stderr, "%s: Error - file %s already exists,\n"
                   "    try again later.\n", ProgName,outFile);
    return;
}

sayOpenError(name,readWriteOrStat,errno) char *name;
    int readWriteOrStat, errno;
    char *operation;
{
    switch (readWriteOrStat) {
    case R_OK:
        operation = "stat input";
        break;
    case O_RDONLY:
        operation = "read input";
        break;
    case O_WRONLY:
        operation = "create output";
        break;
    }
    (void) fprintf(stderr, "%s: can't %s file \"%s\", %s (errno %d).\n"
                   "    halting.\n", ProgName, operation, name,
                   (errno < sys_nerr) ? sys_errlist[errno] :
                   "Unknown error", errno);
    return;
}
```