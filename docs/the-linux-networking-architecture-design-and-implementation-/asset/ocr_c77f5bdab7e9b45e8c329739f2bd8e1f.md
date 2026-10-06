# 2.7 Timing in the Linux Kernel

There are two basic usages for high-resolution timers:

Periodic shot: A timer with a specific interval is initialized and then periodically triggers an interrupt when this interval expires. This corresponds to the behavior of the timer interrupt in the Linux kernel, which always triggers an interrupt after 10 ms.

This type of timer is suitable for all scenarios where actions have to run frequently and normally after fixed intervals. If the accuracy of these intervals is within the range of milliseconds, the standard timers described in the previous sections can be used.

One shot: Exactly one action needs to run at a specific time, regardless of other events. Such an action is, for example, when you send a packet at a pre-calculated time or represent an image from a video.

Until recently, one-shot and periodic-shot timers had been available only on the basis of timer interrupts, offering an accuracy of not more than 1/7 seconds. The timer functionality introduced next is based on the APIC component (in short APIC timer) to avoid the problems outlined above. The UKA-APIC timer was developed at the Institute for Telematics at the University of Karlsruhe, Germany, and can be downloaded from [ObWe01].

Technical Basis of the APIC Timer Intel x86 processor family originally used the PIC 8259A Programmable Interrupt Controller to manage triggered interrupts. It was used since the first personal computer at the beginning of the eighties and met its tasks without problem. However, multiprocessor capability needs to distribute triggered interrupts among several processors of an SMP computer. For this reason, Intel introduced the so-called APIC Programmable Interrupt Controller. More specifically, there are the following two chips, as shown in Figure 2–9:

![](bbox=[0.058, 0.673, 0.942, 0.913])

FIGURE 2-9 Use of an Advanced Programmable Interrupt Controller (APIC) in multiprocessor systems.