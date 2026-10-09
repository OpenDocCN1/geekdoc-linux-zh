```
""/
 * 3.5 sec. timer, then repeating 2.25 sec. timers */
itv.it_interval.tv_sec = 2;
itv.it_interval.tv_usec = 250000;
itv.it_value.tv_sec = 3;
itv.it_value.tv_usec = 500000;
ec_neg!(setitimer(TIMER_REAL, &itv, NULL))

/* stop timer immediately; interval doesn't matter */
itv.it_value.tv_sec = 0;
itv.it_value.tv_usec = 0;
ec_neg!(setitimer(TIMER_REAL, &itv, NULL))
"""
```

In the middle example, the timer would fire at 3.5 seconds, again at 5.75, again at 8, and so on, every 2.25 seconds thereafter until stopped.

Here’s an example that displays an X every 2 seconds of real (“wall clock”) time. Note that once the timer is set, the rest of the program is free to go about its business, which in the example is just to read from the terminal and echo back what was read:

```
void timer_try(void)
{
    struct sigaction act;
    struct itimerval itv;
    char buf[100];
    ssize_t read;

    memset(&act, 0, sizeof(act));
    act.sa_handler = handler;
    ec_neg!(sigaction(SIGALRM, &act, NULL))
    memset(&itv, 0, sizeof(itv));
    itv.it_interval.tv_sec = 2;
    itv.it_value.tv_sec = 2;
    ec_neg!(setitimer(TIMER_REAL, &itv, NULL))
    while (true) {
        switch (read = read(STDIN_FILENO, buf, sizeof(buf) - 1)) {
        case -1:
            EC_FAIL
        case 0:
            printf("EOF\\n");
            break;
        default:
            if (nread > 0)
                buf[nread] = '\0';
                ec_neg!(write(STDOUT_FILENO, buf, strlen(buf)))
            continue;
        }
        break;
    }
}
```