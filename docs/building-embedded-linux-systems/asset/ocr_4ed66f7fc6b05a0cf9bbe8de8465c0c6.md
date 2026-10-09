Otherwise, the worker thread will not be preempted by the packet being received, and the work done by the worker thread will continue to run and prevent anything of lower priority from running on that CPU. The end result would appear to be a system hang. If all other threads are of lower priority than the worker thread, no other threads will be able to capture control of the CPU.

# ### Interrupts and CPU Affinities

An operating system scheduler on a multiprocessor system tries to keep each thread on the CPU where it started in order to prevent expensive cache flushes. This tendency is called CPU affinity. It is very important to note that the CPU affinity of an IRQ thread is determined by the CPU affinity of the interrupt itself. Every time the interrupt handler executes, it compares the thread CPU affinity to that of the interrupt affinity. If they are different, the interrupt service thread affinity is updated to that of the interrupt affinity. So, if you want to set the affinity of the interrupt service thread, simply set the affinity of the interrupt. We'll show the impact of this rule with an example that plays with the affinity of the interrupt service thread, as well as the interrupt itself:

```
```
# cat /proc/interrupts | grep 1de0
    14:   13602   1720   IO-APIC-edge      1de0
# ps ax | grep IRQ-14
  790 ?     5c     0:00 [IRQ-14]
```
```

The system used two CPUs, as can be seen in the first output. The 1de0 controller with interrupt 14 went off 13,602 times on CPU 0 and 1,720 times on CPU 1. The ps command helped the pid (790) of the interrupt service thread for IRQ 14.

In the commands that follow, a simple check of the /proc filesystem reveals the affinity of the interrupt: it's bound to CPU 0 (which is represented by the affinity mask of 1). We then try to manipulate the affinity:

```
```
# cat /proc/irq/14/smp_affinity
      1
# taskset -p 790
pid 790's current affinity mask: 1
# taskset -p 2 790
pid 790's current affinity mask: 1
pid 790's new affinity mask: 2
# taskset -p 790
pid 790's current affinity mask: 2
# cat /proc/irq/14/smp_affinity
      1
```
```

The first taskset command just shows the affinity of the IRQ 14 interrupt service thread (pid 790). It also has the affinity of CPU 0. Next, we try an incorrect way of changing the interrupt service thread's CPU affinity mask by using taskset to set the thread's affinity to CPU 1 (the CPU affinity bitmask of 2 corresponds to CPU 1). A recheck of the /proc/irq/14/smp_affinity file shows that changing the CPU affinity of the interrupt service thread had no effect on the affinity of the IRQ. Furthermore, the scheduler will