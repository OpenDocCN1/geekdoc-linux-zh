This is a powerful feature. Some hardware architectures do not enforce interrupt priorities. Those that do might not enforce the priorities consistent with your specified real-time design goals. Using CONFIG_PREEMPT_HARDIRQ, you are free to define the priorities at which each IRQ will run.

Conversion of ISRs to threads can be disabled at runtime through the /proc file system or at boot time by entering a parameter on the kernel command line. When enabled in the configuration, unless you specify otherwise, ISR threading is enabled by default.

To disable ISR threading at runtime, issue the following command as root:

```
# echo '0' > /proc/sys/kernel/hardirq_preemption
```

To verify the setting, display it as follows:

```
# cat /proc/sys/kernel/hardirq_preemption
1
```

To disable ISR threading at boot time, add the following parameter to the kernel command line:

```
hardirq-preempt=0
```

# 17.3.1.3 Preemptable Softirqs

CONFIG_PREEMPT_SOFTIRQ reduces latency by running softirqs within the context of the kernel’s softirq daemon (ksoftirqd). ksoftirqd is a proper Linux task (process). As such, it can be prioritized and scheduled along with other tasks. If your kernel is configured for real time, and CONFIG_PREEMPT_SOFTIRQ is enabled, the ksoftirqd kernel task is elevated to real-time priority to handle the softirq processing.⁵ Listing 17-3 shows the code responsible for this from a recent Linux kernel, found in .../kernel/softirq.c.

> ⁵ See Linux Kernel Development, referenced at the end of this chapter, to learn more about softirqs.