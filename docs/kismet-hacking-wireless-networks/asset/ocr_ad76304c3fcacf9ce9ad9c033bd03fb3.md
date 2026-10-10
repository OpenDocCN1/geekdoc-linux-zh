```
USB Serial Converter support --->
<> USB Serial Converter support
[*] USB Generic Serial Driver
<> USB Prolific 2303 Single Port Serial Driver
```

The Prolific 2303 driver is a very common USB serial converter driver. You will need to ensure that you have compiled in support for your specific converter.

Next, exit out of the menuconfig, save your kernel configuration, compile your new kernel, move or copy the bzImage to your boot partition, and, if necessary, update your bootloader. After rebooting, insert your USB serial adapter. The system dmesg will show if the kernel correctly recognized your converter (see Figure 1.3).

# NOTE

When you execute **make menuconfig**, it reads from the running kernel or from the kernel configuration file for the current kernel. This configuration has all of the changes that were previously made, therefore, they do not need to be repeated.

# Figure 1.3 The Prolific USB Serial Converter

![](bbox=[0.15, 0.54, 0.83, 0.95])