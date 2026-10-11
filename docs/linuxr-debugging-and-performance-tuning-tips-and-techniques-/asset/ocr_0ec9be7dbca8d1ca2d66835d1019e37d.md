write sigemptyset(), sigfillset(), sigaddset(), sigdelset(), and sigismember().

+   5. Practise your bit-bashing skills some more. Repeat the previous exercise, this time assuming that the highest signal is 42.

+   6. Now that you’ve done the previous two exercises, find sigemptyset() et al. in your <signal.h> header file. (You may have to search for them; they could be in files #included by <signal.h>) Are they macros or functions?

+   7. In Section 10.7, “Signals for Interprocess Communication,” page 379, we mentioned that production code should work with the initial process signal mask, adding signals to be blocked and removing them except in the call to sigsuspend(). Rewrite the example, using the appropriate calls to do this.

+   8. Write your own version of the kill command. The interface should be
+   
+   kill [ -s signal-name ] pid ...
+   
+   Without a specific signal, the program should send SIGTERM.

+   9. Why do you think modern shells such as Bash and ksh93 have kill as a built-in command?

+   10. (Hard). Implement sleep(), using alarm(), signal(), and pause(). What if a signal handler for SIGALRM is already in place?

+   11. Experiment with ch10-reap.c, changing the amount of time each child sleeps and arranging to call sigsuspend() enough times to reap all the children.

+   12. See if you can get ch10-reap2.c to corrupt the information in kids, nkids, and kidsleft. Now add blocking/unblocking around the critical section and see if it makes a difference.