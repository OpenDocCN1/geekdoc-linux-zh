# **PERFORMANCE MONITORING**



Table 13-1 **Common keywords used with the setserial utility**

| Option | Description |
| :--- | :--- |
| port n | Sets the I/O address to n for a serial device |
| irq n | Sets the IRQ to n for a serial device |
| auto_irq | Attempts to automatically detect the IRQ setting for a serial device |
| spd_hi | Sets the speed of a serial port to 56KB/s |
| spd_vhi | Sets the speed of a serial port to 115KB/s |
| spd_normal | Sets the speed of a serial port to 38.4KB/s |

# ## **Performance Monitoring**

Some problems that you will encounter on a Linux system are not as noticeable as those discussed in the previous section; such problems affect the overall performance of the Linux system. Like the problems discussed earlier, performance problems can be caused by software or hardware or a combination of the two.

Hardware that is improperly configured might still work, but at a slower speed. In addition, when hardware ages, it might start to malfunction and send large amounts of information to the CPU when not in use; this process is known as **jabbering** and can slow down a CPU and, hence, the rest of the Linux system. To avoid this hardware malfunction, most companies retire computer equipment after two to three years of use.

Software can also affect the overall performance of a system; software that requires too many system resources monopolizes the CPU, memory, and peripheral devices. Poor performance can also be the result of too many processes running on a computer, processes that make a great deal of read/write requests to the hard disk (such as databases), or rogue processes. To remedy most software performance issues, you can remove software from the system to free up system resources; if this software is needed for business activity, you can instead choose to move the software to another Linux system that has more free system resources.

Software performance problems can also sometimes be remedied by altering the hardware. Upgrading or adding another CPU allows the Linux system to execute processes faster and reduce the number of processes running concurrently on the CPU. Alternatively, some peripheral devices can perform a great deal of processing that is normally performed by the CPU; this is known as **bus mastering**. Using bus mastering peripheral components reduces the amount of processing the CPU must perform and, hence, increases system speed.

Adding RAM to the computer also increases system speed as processes will have more working space in memory and the system will swap much less information to and from the hard disk. Because the operating system, peripheral components, and all processes use RAM constantly, adding RAM to any system often has a profound impact on system performance.