```
```c
printf("%s", buf);

/* Close and reap the exit status */
p close(fp);
exit(EXIT_SUCCESS);
}

void err_quit(char *msg)
{
    perror(msg);
    exit(EXIT_FAILURE);
}
```
```

As you can see from the listing, `popen` and `pclose` make working with pipes much less code intensive. The price is giving up a certain amount of control. For example, you are forced to use the C's stream library rather than the low-level read and write I/O calls. In addition, `popen` forces your program to perform an exec, which you might not necessarily want or need to do. Finally, the function call `pclose` uses to reap the child's exit status might not fit your program's requirements. This loss of flexibility notwithstanding, `popen` saves 10–15 lines of code itself; while the code to handle reading and writing is significantly simplified from the `piperw` code. The output, part of which follows, is unchanged. The semantics of the mode may seem odd, so just remember that `r` means that you read from `stdout` and `w` means you write to `stdin`.

![](bbox=[0.045, 0.48, 0.16, 0.54])

# ### Output

```
```
$ ./newrw
/*
 * pipopn.c - Open and close a pipe
 */
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>
...
```
```

# ### FIFOs

As stated previously, FIFOs are also called named pipes because they are persistent, that is, they exist in the file system. FIFOs are especially useful because they allow unrelated processes to exchange data.