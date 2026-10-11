# ## CPU Affinity

Many UNIX systems (Solaris, for instance) offer the system administrator the possibility to bind a process to one desired CPU only. This binding to a selected CPU is more commonly known as *CPU affinity*. The rationale behind it is that the CPU primary and secondary cache lines most likely contain the entries particular to the process in question and thus benefit the process's performance overall. This can result in greatly reduced memory access by that CPU, and thus much faster execution. However, faster execution is not necessary when all the process is doing is, for example, spinning on a `spin_lock()` and faster execution is less important than earlier execution when the process has been asleep holding a `wait_lock()` that another process may need.

Thus, great care must be used when playing with affinity, because there is a high chance of seriously disturbing the delicate load balance of the system. CPU affinity probably makes most sense when a process is bound to a certain CPU and no other process can execute on that CPU. This, however, only makes sense if there is a very great number of CPUs available. On a Sun E10000 with 64 CPUs it might make sense to dedicate one CPU to a certain process. On a dual-CPU system, affinity is certainly too expensive.

For the sake of the example here, let's assume there are enough CPUs and let's further assume the workload warrants CPU affinity for a certain process. In that case the following patch might help:

```
```
--- 2.3.38-psret/include/linux/sched.h -1~    Tue Jan 11 14:46:45 2000
+++ 2.3.38-psret/include/linux/sched.h    Tue Jan 11 17:58:52 2000
@@ -363,6 +363,7 @@
	 u32 self_exec_id;
 /* Protection of fields allocation/deallocation */
	 struct semaphore exit_sem;
+	 int bind_cpu;
	};

	/*
@@ -430,6 +431,7 @@
	/* signals */	 SPIN_LOCK_UNLOCKED, &init_signals, ({}), ({}), NULL,
		&init_task.sigqueue, 0, 0, \
	/* exec cts */ 0,0, \
	/* exit_sem */ __MUTEX_INITIALIZER(name.exit_sem),	\
+NO_PROC_ID,
	}

#ifndef INIT_TASK_SIZE
--- 2.3.38-psret/kernel/sched.c -1~    Sun Jan 9 20:45:31 2000
```
```