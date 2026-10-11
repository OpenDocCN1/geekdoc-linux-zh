```
exit(EXIT_FAILURE);
    }

    /* These are the flags we'll set on the file */
    flags = EXT2_SYNC_FL | EXT2_NODUMP_FL;
    /* Set the flags, bail out gracefully if it fails */
    if(ioctl(fd, EXT2_IOC_SETFLAGS, &flags)) {
        perror("ioctl");
        close(fd);
        exit(EXIT_FAILURE);
    }

    if(flags & EXT2_SYNC_FL)
        puts(stdout, "SYNC flag set");

    if(flags & EXT2_NODUMP_FL)
        puts("NODUMP flag set");

    close(fd);
    exit(EXIT_SUCCESS);
}
```

Output from a sample run of setext2 follows:

![](bbox=[0.0, 0.501, 0.091, 0.543])

# **Output**

```
$ touch foo
$ lsattr foo
------- foo
$ ./setext2 foo
SYNC flag set
NODUMP flag set
$ lsattr foo
--S--d- foo
```

The semantics of the ioctl routine require that the file being modified be open hence the open call. After assigning the attributes EXT2_SYNC_FL and EXT2_NODUMP_FL to the flags variable, the ioctl call attempts to set them, being sure to close the open file if the call fails. The last code block confirms that the requested attributes (sync and no-dump) were, in fact, set. The lsattr command used in the sample run further confirms this fact.