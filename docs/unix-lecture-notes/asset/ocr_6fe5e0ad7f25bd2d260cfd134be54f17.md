# Examples

The following program, signal_demo1.c, shows how signal handlers for Ctrl-C (SIGINT) and Ctrl-\ (SIGQUIT) are installed.

# Listing 5.12: signal_demo1.c

```
#include <stdio.h>
#include <signal.h>

void catch1(int signum)
{
    printf("You can do better than that!\n");
}

void catch2(int signum)
{
    printf("I'm no quitter!\n");
}

int main()
{
    int i;

    signal( SIGINT, catch1 );
    signal( SIGQUIT, catch2 );
    for(i = 20; i > 0; i-- ) {
        printf("Try to kill me with ^C or ^\\.\n");
        sleep(1);
    }
    return 0;
}
```

The call signal(signum, f) installs f() as the signal handler for the signal signum. When signal() is executed, f() is installed. Until that point, f() is not installed. When you run signal_demo1 and enter a Ctrl-C, the SIGINT signal is sent to the process executing signal_demo1; as a result, the handler f() runs, and when it terminates, the program resumes execution. In signal_demo1.c, the only action taken by either handler is to print a message on the screen, simply to show that the function was executed.

The next program, signal_demo2.c, is almost the same as signal_demo1.c with one exception: SIGINT and SIGQUIT are ignored by calling signal() with SIG_IGN as the second argument.

```
#include <stdio.h>
#include <signal.h>
int main()
{
```