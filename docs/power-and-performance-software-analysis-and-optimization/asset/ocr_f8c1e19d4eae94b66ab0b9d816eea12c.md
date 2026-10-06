# References 41

The coordination of multiple cores occurs in an identical fashion to multiple processors. After a hardware #RESET, one of the logical processors, which can be either a core or separate processor, is selected as the boot processor. The boot processor is responsible for performing the system initialization by executing the early BIOS code. All of the other logical processors halt and wait for the boot processor to begin initialization, it uses Inter-Processor Interrupts (IPIs) to wake the processors.

# 2.3.3 INTEL HYPER-THREADING

Intel Hyper-Threading Technology adds additional parallelism to each processor core by dividing it into multiple hardware threads. Whereas multiple processors duplicate all of the core resources for each core, hardware only require the duplication of a small subset of execution state. Typically, this subset includes the registers and APIC.

Since only the execution state is duplicated, but not the execution pipeline, the core's execution pipeline is shared with each hardware thread. As a result, $\muops$ from both threads are present within the execution pipeline simultaneously. In other words, Hyper-Threading allows the $\muop$ scheduler to fill underutilized execution pipeline resources by interleaving the $\muops$ of two different processes.

Within Linux, each hardware thread appears as a logical processor. For instance, one-core processor with Hyper-Threading will register eight logical processors. Kconfig option enables additional logic within the Linux kernel scheduler that makes it aware of hardware threads. Using this information, it can make better decisions when migrating processes between logical processors.

# REFERENCES

Intel Corporation, 1996, Pentium® Pro Family Developer's Manual, vol. 1: Specifications.
Intel Corporation, 1997, Pentium® Pro Family Developer's Manual.
Intel Corporation, 2013, 10. 64 and IA-32 Architecture Software Developer's Manual,
Computer Hardware Manual.

Israel, J., 1995, Intel pentium used. With permission. http://www.happytrees.org/mainimages/chip-v2/ic-photo-Intel--KB00521EX200-(Pentium-Pro-CPU).png, PNG converted to grayscale and EPS.

Israel, J., 1996, Intel pentium used. With permission. http://www.happytrees.org/main-images/chip-v2/ic-photo-Intel--A80502150-(CPU).JPG, JPEG converted to grayscale and EPS.

Israel, J., 2000, 01. Intel pentium used. With permission. http://www.happytrees.org/mainimages/chip-v2/ic-photo-Intel--1.8GHZ_256_400_1.75V--:(Pentium-4-CPU).png, PNG converted to grayscale and EPS.

Patterson, D.A., Hennessy, L., 2007, Computer Organization and Design: The Hardware/Software Interface, third ed. Mark Kaufman, Burlington, MA.