# 6.12.2 The bouncestr.c Program Using O_ASYNC: Flawed Version

Sometimes it is worth writing a bad program in order to understand how to write a good program. This is such an exercise. The program (excluding the #includes and parts that are identical to the bouncestr.c program's ) is shown below. The program is terminated within the on_input() handler when it receives the quit input character. This is because, once the program has started, it cannot be terminated by turning off the timer or by setting the control variable of the loop to 1. This will be explained later.

The tasks of the main program are:

+   1. Establish the signal handlers.
+   2. Initialize NCurses (in cbreak mode with no echo).
+   3. Initialize the data state of the program (speed, direction, rows, columns, etc)
+   4. Set up keyboard signals.
+   5. Start the interval timer.
+   6. Display the messages on the last line and loop until it is time to quit.

The program:

# Listing 6.16: A flawed bouncestr_async.c

```
/* <——— snip ———> */
int dir; /* Global variable to store direction of movement */
int speed; /* Current speed in chars/second */
volatile sig_atomic_t finished;

void move_msg(int); /* handler for alarm */
void on_input(int); /* handler for keybd */
void enable_kbd_signals(); /* setup for SIGIO */

int main(int argc, char * argv[])
{
    struct sigaction newhandler; /* for installing handlers */
    sigset_t blocked; /* to set mask for handler */
    char msgge[40];

    /* Set up signal handling */
    newhandler.sa_handler = on_input; /* name of handler */
    newhandler.sa_flags = SA_RESTART; /* flag is just RESTART */
    sigemptyset(&blocked); /* clear all bits of blocked set */
    newhandler.sa_mask = blocked; /* set this empty set to be the mask */
    if ( sigaction(SIGIO, &newhandler, NULL) === -1 ) {
        perror("sigaction");
        return (1);
    }

    sigemptyset(&blocked); /* clear all bits of blocked set */
```