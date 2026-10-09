The default behavior for these signals is to suspend the process, which makes a lot of sense: Background processes that need access to the controlling terminal stop, and you move them to the foreground when you're ready to interact with them.

The exceptions to the basic rule are:

+   *   A background process attempting to read with `SIGTTIN` signals ignored or blocked instead gets an `EIO` error from `read`.
+   *   An orphaned background process (process-group leader has terminated) also gets an `EIO` from `read`.
+   *   If the `TOSTOP` terminal attribute (see Section 4.5.6) is clear, the process is allowed to write.
+   *   If `TOSTOP` is set but `SIGTTOU` signals are ignored or blocked, the process is allowed to write.
+   *   If `TOSTOP` is set, an orphaned background process gets an `EIO` error from `write`.

So, to summarize the rules: A background process can't read the controlling terminal no matter what; it gets an error or is stopped. An orphaned background process gets an error if it tries to write the terminal. Nonorphaned background processes can write it if `TOSTOP` is clear or if `SIGTTOU` are ignored or blocked; otherwise they are stopped.

The asymmetry between reading and writing is because it never makes sense for two processes to both read characters—it's much too dangerous. (Imagine typing `rm *.o` and having the shell only get `rm *.`.) Two processes writing is only confusing, and if that's what the user really wants, then so be it.

# ### 4.3.2 System Calls for Sessions

**setsid**--create session and process group

```c
#include <unistd.h>

pid_t setsid(void);
/* Returns process-group ID or -1 on error (sets errno) */
```

**getsid**--get session ID

```c
#include <unistd.h>

pid_t getsid(
    pid_t pid               /* process ID or 0 for calling process */
);
/* Returns session ID or -1 on error (sets errno) */
```