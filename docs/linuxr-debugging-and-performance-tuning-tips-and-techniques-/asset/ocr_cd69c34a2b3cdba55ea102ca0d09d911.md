Otherwise the delivery will be offset by a small time dependent on the system loading.

Of the three timers, **ITIMER_REAL** seems most useful. The following program, ch14--timers.c, shows how to read data from a terminal, but with a *timeout* so that the program won't hang forever waiting for input:

```
/* ch14--timers.c ---- demonstrate interval timers */
#include <stdio.h>
#include <assert.h>
#include <signal.h>
#include <sys/time.h>

/* handler --- handle SIGALRM */
void handler(int signo)
{
   static const char msg[] = "\n** Timer expired, you lose **\n";
   assert(signo == SIGALRM);

   write(2, msg, sizeof(msg) - 1);
   exit(1);
}
/* main --- set up timer, read data with timeout */
int main(void)
{
   struct itimerval tval;
   char string[BUFSIZ];

   timerclr(& tval.it_interval); /* zero interval means no reset of timer */
   timerclr(& tval.it_value);

   tval.it_value.tv_sec = 10;  /* 10 second timeout */

   (void) signal(SIGALRM, handler);

   printf("You have ten seconds to enter/your name, rank, and serial number: ");

   (void) setitimer(ITIMER_REAL, & tval, NULL);
```