# 9.1 Process Creation and Management

```
519 static void
520 strip (const char *path)
521 {
522 int status;
523 pid_t pid = fork ();
524
525 switch (pid)
526 {
527 case -1:
528 error (EXIT_FAILURE, errno, "fork system call failed");
529 break;
530 case 0: /* Child. */
531 exec1p ("strip", "strip", path, NULL);
532 error (EXIT_FAILURE, errno, "cannot run strip");
533 break;
534 default: /* Parent. */
535 /* Parent process. */
536 while (pid != wait (&status)) /* Wait for kid to finish. */
537 /* Do nothing. */ ;
538 if (status)
539 error (EXIT_FAILURE, 0, "strip failed");
540 break;
541 }
542 }
```

Line 523 calls fork(). The switch statement then takes the correct action for error return (lines 527–529), child process (lines 530–533), and parent process (lines 534–539).

The idiom on lines 536–537 is common; it waits until the specific child of interest exits. wait()’s return value is the PID of the reaped child. This is compared with that of the forked child. status is unused other than to see if it’s nonzero (line 538), in which case the child exited unsuccessfully. (The test, while correct, is coarse but simple. A test like `if (WIFEXITED(status) && WEXITSTATUS(status) != 0)` would be more pedantically correct.)

From the description and code presented so far, it may appear that parent programs must choose a specific point to wait for any child processes to die, possibly polling in a loop (as install.c does), waiting for all children. In Section 10.8.3, “Parental Supervision: Three Different Strategies,” page 385, we’ll see that this is not necessarily the case. Rather, signals provide a range of mechanisms to use for managing parent notification when a child process dies.