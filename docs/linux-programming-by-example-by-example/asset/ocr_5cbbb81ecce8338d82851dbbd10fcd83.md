```
```c
void err_quit(char *msg)
{
    perror(msg);
    exit(EXIT_FAILURE);
}
```
```

![](bbox=[0.04, 0.21, 0.16, 0.26])

# **Output**

A test of this program produced the following output. The program ran in one window and was sent signals using the `kill` command from another window (commands sent from the second are shown in brackets).

```
```
$ ./block
[\$ kill -TERM \$(pidof ./block)]
[\$ kill -ALRM \$(pidof ./block)]
[\$ kill -QUIT \$(pidof ./block)]
Quit (core dumped)
```
```

As you can see from the output, sending the process `SIGTERM` and `SIGALRM` had no effect, although both signals' default action is to terminate the process. The command `pidof` `./block` returns the PID associated with `./block`, whereas the `\$( . . . )` construct substitutes the results of the command and passes it to the `kill` command. When the process receives `SIGQUIT`, it quits, as the output shows. Note that because the program blocks `SIGTERM` and `SIGALRM`, `pause` never returns because the process does not receive the signal.

![](bbox=[0.04, 0.58, 0.12, 0.62])

# **Example**

2. This program establishes a handler for `SIGUSR1`. `SIGUSR1`'s default action is to terminate the process. The custom handler just says it was called.

```
```c
/*
 * blkusr.c -Custom handler for SIGUSR1
 */
#include <unistd.h>
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>

void err_quit(char *);  /* err function */
void hndl usr1(int);    /* signal handler */

int main(void)
{
```
```