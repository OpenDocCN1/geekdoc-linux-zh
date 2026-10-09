will just stay pending forever. So, the original version, using signal hand- lers, is the one you should use for the detected-error signals.

+   * If one of the hardware-detected signals, SIGBUS, SIGFPE, SIGILL, and SIGSEGV, occurs naturally while blocked, the result is undefined (see Sec- tion 9.1.3). Most likely the process will be immediately terminated, and sigwait will never get a chance to return it. This wasn’t a problem with the signal-handler version because, after the initial setup, those four signals were unblocked.

This is not to say that sigwait isn’t useful. Most signals, including all but the detected-error group in Section 9.1.3, are sent to the process when they are gener- ated naturally (i.e., not by pthread_kill), so a thread waiting in sigwait works perfectly well and is a much better choice than a signal handler.

# 9.2.3 sigsuspend System Call

sigsuspend is an older, nonmultithreading system call that also waits for a sig- nal. Before we get to its details, let’s explore the problem it solves. Back in Chapter 8 when we kept running examples that forked to create processes that connected to the parent’s socket, it was important for the parent to get the socket bound before the child connected, and we used the crude technique of having the children sleep for a few seconds to give the parent a chance to get ahead. Not only is sleeping unreliable, because there’s no guarantee that a few seconds is enough, but it’s also inefficient because a few seconds may be much too long. To recap, here’s the same problem in a simpler example:

```
void try1(void)
{
	if (fork() == 0) {
		printf("child\n");
		exit(EXIT_SUCCESS);
	}
	printf("parent\n");
	return;
}
```

This function displayed

+   child
+   parent