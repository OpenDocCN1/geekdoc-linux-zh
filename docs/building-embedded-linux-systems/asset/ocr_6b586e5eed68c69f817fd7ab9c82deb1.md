![](bbox=[0.155, 0.075, 0.26, 0.165])

There is development going on that will allow the hrtimer thread to take on a dynamic priority. What this means is that the hrtimer-softirq thread will take on the priority of the timer that it will execute, which in turn is derived from the priority of the task that requested the timer. This feature has been included on various versions of the RT patch, but because of the way Linux is currently designed, it has caused some technical difficulties. A future version of the RT patch will eventually include this feature again, and at that point there will be no need to worry about the priority of the hrtimer-softirq thread because it will automatically change its priority to that of the process that requested the timer.

An RT application must be aware of its use of POSIX timers. If all parts of the application, from low-priority to high-priority processes, use POSIX timers, the lower-priority processes may cause latencies within the higher-priority process when their timers are triggered. These latencies are not particularly critical as long as they are accounted for. A lower-priority process still cannot cause much harm to a higher-priority process by using POSIX timers, even when the higher-priority process is lower in priority than the softirq-hrtimer thread. The only thing that preempts the higher-priority process through the softirq-hrtimer thread is the processing of the timer to send a signal to the lower-priority process.

At the time of this writing, the RT patch's handling of POSIX timers forces each timer interval to be at least one jiffie, promoting it to a jiffie if a shorter time is requested. ${ }^{\dagger}$ This is to keep the hrtimer-softirq thread from starving if the signal process ignores the signal it is supposed to receive from the timer. Ignored signals cause a re-triggering of the softirq-hrtimer thread. This also prevents lower-priority processes from doing more than one timer event per jiffy that would preempt a higher-priority process, and thus would allow the latency caused by lower-priority processes to overrun the system.

![](bbox=[0.155, 0.605, 0.26, 0.695])

The *nanosleep* system call is *not affected* by the softirq-hrtimer. As mentioned earlier, timer interrupts are not handled by threads but are performed at the time the ISR runs. Processes that are sleeping with *nanosleep* will be woken up directly from the interrupt. So, processes that are of higher priority than the softirq-hrtimer interrupt will still work fine using *nanosleep*, and even *sleep* for that matter.

# Priority Inheritance

In Linux kernel version 2.6.18, priority inheritance was, for the first time, part of the mainline Linux kernel. Although this priority inheritance applied only to userland fast mutexes (futex), the infrastructure was in the kernel. This code was developed in the

$^{\dagger}$ jiffies are an arbitrary measurement of time in Linux and are defined as a HZ value in the kernel configuration. Distributions usually default this value to 100, 250, or 1,000.