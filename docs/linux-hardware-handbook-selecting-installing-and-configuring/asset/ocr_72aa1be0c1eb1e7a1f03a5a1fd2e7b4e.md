Table 16.1. Sharing interrupts in this way works acceptably in DOS, but requires special configuration in Linux. Therefore, if you purchase an internal modem or secondary serial port card, you should do one of three things:

+   Disable an unused serial port on the motherboard and configure the internal modem to use its port number. For instance, you could disable `/dev/ttyS0` (identified as **COM1**: in the BIOS) using your BIOS’s setup routines, and configure the modem to take on this identity.
+   *   Enable the Support for sharing serial interrupts option under Character devices in the Linux kernel configuration. Doing so enables you to use a shared interrupt for serial ports.
+   *   Assign the new port an interrupt other than the standard one. For instance, you might give it IRQ 9. The add-on device will then become `/dev/ttyS2` (and `/dev/ttyS3`, if it’s a two-port serial card and you give the second card its own interrupt, as well).

If you need more than two or three serial ports, I recommend you use a multiport serial board. These products support running several serial ports on just one interrupt, but they require special drivers in Linux. Fortunately, the Linux kernel includes the necessary drivers to support several multiport serial boards, so you should check the kernel configuration options to find which boards are supported.

By default, most Linux distributions are configured to not use interrupts for printing on the parallel ports. Instead, the hardware is operated in *polling mode*, which consumes more CPU time but leaves the parallel port’s interrupt available for use by other devices. If you want to switch to using an interrupt for a printer port, you can do so by copying the interrupt number to the `/proc/parport/n/irq` file, where *n* is the parallel port number. For instance, to change `/dev/lp0` to use interrupt 7, issue the following command:

```
echo 7 > /proc/parport/0/irq
```

You can confirm that this action has had the desired effect by typing `cat /proc/interrupts` and checking that interrupt 7 is used by the parallel port driver. You should then check to be sure you can print. If this change causes problems, you can reverse it by echoing the value 0 to the `/proc/parport/n/irq` file.

# Note

Linux kernels prior to 2.1.131 used a different method of configuring interrupt-driven printing. These kernels used a program called *tunelp* to do the job. I describe this program later in this chapter.