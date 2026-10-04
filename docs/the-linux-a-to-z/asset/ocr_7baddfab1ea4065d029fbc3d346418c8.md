![](bbox=[0.12, 0.1, 0.9, 0.4])

Figure 17.1 Effect of executing the system call dup(2).

```
#include <unistd.h>
#include <stdio.h>

main()
{
    int fda[2];

    if (pipe(fda)==-1)                /* Create pipe */
        fatal("creating pipe");

    switch (fork())                   /* Create child */
    {
    case -1:
        fatal("forking child");
        break;

    case 0:                           /* Run ls in child */
        close(1);                     /* Close standard output */
        dup(fda[1]);                  /* Duplicate pipe write end */
        close(fda[1]);                /* Close pipe write end */
        close(fda[0]);                /* Close pipe read end */
        execlp("ls", "ls", 0);      /* Execute ls command */
        fatal("trying to exec ls");
        break;

    default:                          /* Run wc in parent */
        close(0);                     /* Close standard input */
        dup(fda[0]);                  /* Duplicate pipe read end */
        close(fda[0]);                /* Close pipe read end */
    }
```