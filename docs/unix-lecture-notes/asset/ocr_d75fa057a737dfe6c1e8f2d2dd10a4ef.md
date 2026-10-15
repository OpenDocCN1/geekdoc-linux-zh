# 5.3.12.2 Example

The following program will demonstrate the use of the sigaction structure for old-style handlers as well as the new-style handlers. The program begins by defining the sigaction structure that will be passed to the sigaction function. The handler function, interrupt_handler, is assigned to the sa_handler field. The sa_flags field is initialized with the bitwise-or of the flags referenced in the command-line. The sa_mask is built step by step. There are a few ways to do this. You can start with an empty set and add to it or start with a full set and remove from it. In this case, I am allowing the user to interactively add signal numbers to the blocked set, so I start with an empty set and add to it. The method of creating these sets is discussed below.

# Listing 5.14: sigaction_demo2.c

```
/*
 * Usage:
 *     sigaction_demo [ reset | noblock | restart ]*
 * i.e., 0 or more of the words reset, noblock, and restart may appear
 * on the command line, and multiple instances of the same word as the same
 * effect as a single instance.
 *
 * reset    turns on SA_RESETHAND
 * noblock  turns on SA_NODEFER
 * restart  turns on SA_RESTART
 *
 * NOTES
 * (1) If you supply the word "reset" on the command line it will set the
 * handling to SIG_DFL for signals that arrive when the process is
 * in the handler. If noblock is also set, the signal will have the
 * default behavior immediately. If it is not set, the default will
 * delay until after the handler exits. If noblock is set but reset is
 * not, it will recursively enter the handler.
 * (2) The interrupt_handler purposely delays for a few seconds in order to
 * give the user time to enter a few interrupts on the keyboard.
 * (3) interrupt_handler is the handler for both SIGINT and SIGQUIT, so if it
 * is not reset, neither Ctrl-C nor Ctrl-\ will kill it.
 * (4) It will ask you to enter the numeric values of signals to block. If
 * you don't give any, no signals are blocked.
 *
 */

#include <stdio.h>
#include <string.h>
#include <signal.h>
#include <time.h>
#include <fcntl.h>

#define INPUTLEN        100

int main(int ac, char* av[])
{
    struct sigaction newhandler;      /* new settings      */
    sigset_t        blocked;          /* set of blocked sigs */
    void            inthandler();     /* the handler       */
```