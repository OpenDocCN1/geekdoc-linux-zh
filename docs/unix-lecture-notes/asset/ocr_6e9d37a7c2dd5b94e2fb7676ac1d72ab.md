There are three flags that can be passed to waitpid():

+   - **WNOHANG** return immediately if no child has exited.
+   - **WUNTRACED** also return if a child has stopped (but not traced via ptrace(2)). Status for traced children which have stopped is provided even if this option is not specified.
+   - **WCONTINUED** (Since Linux 2.6.10) also return if a stopped child has been resumed by delivery of SIGCONT.

The program in Listing 7.12 below combines some of the preceding ideas and demonstrates the use of waitpid() with the WNOHANG flag.

# Listing 7.12: waitpiddemo.c

```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/wait.h>
#include <signal.h>

void child()
{
    int exit_code;

    printf("I am the child and my process id is %d.\n",getpid());
    sleep(2);
    printf("Enter a value for the child exit code followed by <ENTER>.\n");
    scanf("%d",&exit_code);
    exit(exit_code);
}

int main(int argc, char* argv[])
{
    pid_t pid;
    int status;
    int signum;

    printf("Starting up...\n");
    if ( -1 === (pid = fork())) {
        perror("fork");
        exit(1);
    }
    else if ( 0 === pid ) {
        child();
    }
    else {
        /* wait for specific child process with waitpid()
           If no child has terminated, do not block in waitpid()
           Instead just sleep. (Would do something useful instead.)
        */
        while (0 === waitpid(pid, &status, WNOHANG) ) {
            printf("still waiting for child\n");
            sleep(1);
        }
    }
```