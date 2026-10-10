```
{
 atexit (stop_clock);
 first_time = FALSE;
}

old_tick = getvect (BIOS_TIMER);
setvect (BIOS_TIMER, tick);
installed = TRUE;
}
```

# Signal

Interrupts raised by the host computer can be trapped and diverted in several ways. A simple method is to use signal(). Signal() takes two parameters in the form:

```
void (*signal (int sig, void (*func) (int))) (int);
```

The first parameter, sig, is the signal to be caught. This is often predefined by the header file signal.h. The second parameter is a pointer to a function to be called when the signal is raised. This can be either a user function or a macro defined in the header file signal.h, to do some arbitrary task, such as ignore the signal.

On a PC platform, it is often useful to disable the Ctrl-Break key combination that is used to terminate a running program by the user. The following PC signal() call replaces the predefined signal SIGINT, which equates to the Ctrl-Break interrupt request with the predefined macro SIG- IGN, and ignores the request:

```
signal (SIGINT,SIG_IGN);
```

This example catches floating-point errors on a PC, and zero divisions:

```
#include <stdio.h>
#include <signal.h>

void (*old_sig) ();

void catch(int sig)
{
printf ("Catch was called with: %d\n",sig);
}

void main()
{
int a;
int b;

old_sig = signal (SIGFPE,catch);

a = 0;
b = 10 / a;

/* Restore original handler before exiting! */
```