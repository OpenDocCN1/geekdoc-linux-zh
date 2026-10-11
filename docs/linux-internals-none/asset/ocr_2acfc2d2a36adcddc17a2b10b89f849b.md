up/sleep signal probably is better than using a spinlock that tries to reacquire the lock inside a loop. Implementing the hint can be done easily via the prctl system call. It would be possible to call:

```
```
prctl(PR_RESET_TIMESLICE);
```
```

Andrea Arcangeli wrote an implementation (that doesn't care about the scheduler fairness) against kernel 2.2.13:

```
```
--- 2.2.13/kernel/sys.c Sun Oct 31 23:31:39 1999
+++ /tmp/sys.c Sun Nov 28 18:00:13 1999
@@ -995,6 +995,9 @@
 }
			current->pdeath_signal = sig;
			break;
+		case PR_RESET_TIMESLICE:
+			current->counter += current->priority >> 1;
+			break;
		default:
			error = -EINVAL;
			break;
--- 2.2.13/include/linux/prctl.h	Sun Oct 31 23:31:38 1999
+++ /tmp/prctl.h	Sun Nov 28 18:01:01 1999
@@ -4,6 +4,7 @@
/*  Values to pass as first argument to prctl()  */

#define PR_SET_PDEATHSIG	1  /*  Second arg is a signal  */
+#define PR_RESET_TIMESLICE	2  /*  Second arg is a signal  */

#endif /* __LINUX_PRCTL_H */
```
```

In his patch, Andrea Arcangeli gives a new half-timeslice to the process calling the prctl(PR_RESET_TIMESLICE) syscall. The patch is obviously not secure, because everybody could run his task all the time by calling prctl all the time, but a real implementation should take care of all the security details. My implementation should work just fine if used in a trusted environment, and you can take it as an example.

# ## Data Structures—linux/sched.h

```
```
1 ifdef __LINUX_SCHED_H
2 #define __LINUX_SCHED_H
3
4 #include <asm/param.h>	/* for HZ */
5
6 extern unsigned long event;
7
```
```