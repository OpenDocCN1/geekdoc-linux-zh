# Kernel Support

Kernel port support is built largely into the kernel source files. Parallel ports require that several modules be included. RS-232 serial printing is accomplished with much less fuss and requires no real printer-specific adaptation when the kernel is configured. USB-printing requires the use of a 2.4.x or USB-patched 2.2.x kernel compiled with support for both USB and USB printers, as described in Chapter 12. Remote printing requires no printer-specific kernel options.

# Parallel Port Printers

If you are unsure whether your kernel has parallel port printer support built in, look at /var/log/dmesg to see if a line containing lp0, lp1, or lp2 appears. A 2.2.16 kernel with an HP LaserJet 690C printer might produce the following dmesg lines:

```
parport0: PC-style at 0x378 [SP]
port_probe: succeeded
port0: Printer, HEWETT-PACKARD DESKET 690C
lp0: using parport0 (polling).
```

A kernel earlier than 2.1.33 will not say port, since this method was not introduced until later, but you should still see something like lp0 or lp1 in your output. Depending on the exact kernel options, the exact printer in use, whether or not the printer is powered on when the system boots, you may or not need any reference to the printer model attached to the parallel port. Another way to check is to cat /proc/devices file and grep the output for lp1. If 1p is contained within this file, printing is enabled in the running kernel. Use this command:

```
$ cat /proc/devices | grep lp1
6 lp
```

If your kernel has compiled printer support as a module, these tests may not work, because the printer device won't turn up until you try to print. Therefore, don't be concerned if you don't see any evidence of a printer device. Try printing. If it doesn't work, try checking /proc/devices, as just described. If there's no evidence of a printer device, it's possible that your kernel modules are not loading for some reason.

# The lp/ Device Driver

Under kernels earlier than 2.1.33, the printing device was /dev/lp0, /dev/lp1, or /dev/lp2, depending on which parallel port your printer was connected to. This is a static attachment, so any of these may be correct on your system. If one doesn't work, try the

![](bbox=[0.903, 0.535, 0.978, 0.702])