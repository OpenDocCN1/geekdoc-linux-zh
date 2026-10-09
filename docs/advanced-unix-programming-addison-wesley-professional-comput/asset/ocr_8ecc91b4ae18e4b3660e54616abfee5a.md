+   * No alarm was set when `sleep` was called.
+   * The remaining alarm time is less than or equal to the requested `sleep` time.
+   * The remaining alarm time is greater than the requested `sleep` time.

This version works:⁸

```
unsigned aup_sleep(unsigned secs)
{
	sigset_t set, oset;
	struct sigaction act, oact;
	unsigned prev_alarm, slept, unslept, effective_secs;

	ec_neg1( sigemptyset(&set) )
	ec_neg1( sigaddset(&set, SIGALRM) )
	ec_neg1( sigprocmask(SIG_BLOCK, &set, &oset) )
	prev_alarm = alarm(0);
	if (prev_alarm != 0 && prev_alarm <= secs)
		effective_secs = prev_alarm;
	else {
		memset(&act, 0, sizeof(act));
		act.sa_handler = slp_handler;
		ec_neg1( sigaction(SIGALRM, &act, &oact) )
		effective_secs = secs;
	}
	alarm(effective_secs);
	set = oset;
	ec_neg1( sigdelset(&set, SIGALRM) )
	if (sigsuspend(&set) == -1 && errno != EINTR)
		EC_FAIL
	unslept = alarm(0);
	slept = effective_secs - unslept;
	ec_neg1( sigaction(SIGALRM, &oact, NULL) )
	if (prev_alarm > slept)
		alarm(prev_alarm - slept);
	ec_neg1( sigprocmask(SIG_SETMASK, &oset, NULL) )
	return unslept;

EC_CLEANUP_BGN
	EC_FLUSH("aup_sleep")
	return 0;
EC_CLEANUP_END
}

static void slp_handler(int signum)
{
}
```

+   ⁸ Geoff Clare contributed to this version by finding bugs in my original attempt.