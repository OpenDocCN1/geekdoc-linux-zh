# Example 3.6: Using waitpid(3)

```
```
#include <assert.h>
#include <errno.h>
#include <stdio.h>
#include <stdlib.h>

int main (void)
{
  int rc, status;
  pid_t pid;

  pid = fork();

  if (pid < 0) {
    perror ("fork");
    exit (1);
  }

  if (0 == pid) {
    printf ("\tChild process (pid=$d) running\n", getpid());
    sleep (10);
    printf ("\tChild process (pid=$d) terminating\n", getpid());
    exit (0);
  }

  printf ("Parent process (pid=$d) waiting for child (pid=$d)\n",
         getpid(), pid);

  rc = waitpid (pid, &status, 0);

  printf ("Parent process (pid=$d) continuing ", getpid());
  printf ("after the termination of child (pid=$d).\n", pid);
  printf ("Status = 00%x  Return Code=$d\n", status, rc);

  if (rc < 0) {
    perror ("waitpid");
    exit (2);
  }

  exit (0);
}
```
```