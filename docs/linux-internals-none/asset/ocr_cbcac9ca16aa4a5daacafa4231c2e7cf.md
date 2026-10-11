reschedule_idle() because we want to predict the effect of the future schedule() that we’ll send to such a CPU. By predicting the effect of the future schedule() we can choose the best CPU to reschedule at wake-up time. If the CPU to reschedule is not the current one, we send a reschedule event via inter-CPU message passing (SMP-IPI interrupt on x86). goodness() is the core of the Linux scheduler, and it is SMP aware. But reschedule_idle() is the real core of the clever SMP heuristics.

# Kernel Preemption and User Preemption

Linux can do only user preemption. Linus Torvalds doesn’t believe in kernel preemption. That’s not a problem; all is fine for semaphores. Critical sections protected by semaphores can be preempered at any time, as every contention will end in a schedule and there can’t be any deadlock. Here is how it works (Figure 6.1).

![](bbox=[0.03, 0.43, 0.95, 0.79])

Assume that every task, represented by the connected timing machines Ctm1, Ctm2, and Ctm3 in Figure 6.1, has the property that every state, s, has an auxiliary state to which it can be triggered by a suspend signal, and to which it can be restored by a continue signal.