```
puts("Unknown error");
    else
        puts("Lock established");}
    close(fd);
    unlink(argv[1]);
    exit(EXIT_SUCCESS);
}
```

A sample run of lockit produces the following output:

```
$ ./lockit lockit.c.lck
lock established
file already locked
```

Unless something unexpected occurs, lockit successfully locks the file (whose name is passed as the only command-line argument) in the first open statement. Then, in the second open statement, lockit tries to lock the file a second time by creating the same lockfile. Specifying O_CREAT in the open call, along with O_EXCL, means that the open call will fail if the file already exists. To express it another way, creating or opening a lock file using the syntax shown is synonymous with locking a file; deleting a lock file is synonymous with unlocking a file. Because this test fails, the program reports that the file is already locked. Back in the outer block, the program closes the file descriptor and unlinks (deletes) the file, thus removing the lock.

# Record Locking

Although lock files are easy to use, they have significant drawbacks:

+   - When a file is locked, it is not available to other processes that merely want to read it.
+   
+   - The O_EXCL flag is reliable only on local filesystems, not on networked filesystems such as NFS.
+   
+   - The locks are only advisory; processes can ignore them.
+   
+   - If a process terminates before it removes a lock file, the lock file remains in place and other processes have no reliable way to determine whether it is stale, that is, left over from a process that died prematurely.

These shortcomings led to the development of record locking, which gives programmers the ability to lock specific regions of files, called records. Record locks, sometimes referred to as POSIX locks, allow multiple