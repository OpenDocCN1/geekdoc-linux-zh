These abbreviations may not mean much if you don't know what they stand for, so I've broken each of them down here:

+   **us: user CPU time**
+   This is the percentage of CPU time spent running users' processes that aren't niced. (**Nicing** is a process that allows you to change its priority in relation to other processes.)

+   **sy: system CPU time**
+   This is the percentage of CPU time spent running the kernel and kernel processes.

+   **ni: nice CPU time**
+   If you have user processes that have been niced, this metric will tell you the percentage of CPU time spent running them.

+   **id: CPU idle time**
+   This is one of the metrics that you want to be high. It represents the percentage of CPU time that is spent idle. If you have a sluggish system but this number is high, you know the cause isn't high CPU load.

+   **wa: I/O wait**
+   This number represents the percentage of CPU time that is spent waiting for I/O. It is a particularly valuable metric when you are tracking down the cause of a sluggish system, because if this value is low, you can pretty safely rule out disk or network I/O as the cause.

+   **hi: hardware interrupts**
+   This is the percentage of CPU time spent servicing hardware interrupts.

+   **si: software interrupts**
+   This is the percentage of CPU time spent servicing software interrupts.

+   **st: steal time**
+   If you are running virtual machines, this metric will tell you the percentage of CPU time that was stolen from you for other tasks.

In the previous example, you can see that the system is over 50% idle, which matches a load of 1.70 on a four-CPU system. When you diagnose a slow system, one of the first values you should look at is I/O wait so