MCA Micro Channel Architecture. Although Linux is compatible with MCA, Red Hat Linux does not support it.

USB Universal Serial Bus.

Linux kernel support for Firewire, MCA, and USB is not yet complete. The Linux 2.4 kernel will include additional support for USB, USB device drivers may not be immediately available. Red Hat support for Firewire, MCA, and USB is planned.

# System Resources

Most devices require system resources in order to operate. Although some devices can share system resources, many cannot. An important part of configuring devices is assigning resources in such a way that no conflicts occur. The most important system resources are IRQs, I/O ports, and DMAs, which are explained in the following sections.

# IRQs

An IRQ, or hardware interrupt, is a signal that notifies the CPU of an important event, such as completion of an input/output (I/O) operation. Most devices require a dedicated IRQ, which must be assigned manually or by the system BIOS. A PC has a limited number of IRQs, most of which have standard assignments, as shown in Table 2.2.

# TABLE 2.2 Standard IRQ Assignments

| IRQ | Assignment |
| 0 | Reserved for nonmaskable interrupt (NMI), which flags parity errors |
| 1 | Reserved for system timer |
| 2 | Reserved for cascade to second interrupt controller (IRQ 8-15) |
| 3 | Serial ports ttyS1 and ttyS3 if enabled; otherwise, available |
| 4 | Serial ports ttyS0 and ttyS2 if enabled; otherwise, available |
| 5 | Parallel lp1 if enabled; otherwise, available; often used for sound card or modem |
| 6 | Floppy disk drive controller |