# Chapter 10: Understanding System Administration 451

+   **Advanced Configuration and Power Interface (ACPI)** — Besides monitoring features on your laptop, ACPI can also do thermal control, motherboard configuration, and change power states.

Many older laptops do not include support for ACPI in the BIOS, so you must use APM to monitor and manage your batteries. For some newer laptops, ACPI may be required. In general, ACPI offers a more complete feature set for power management, but APM has more user-level support.

To check whether ACPI or APM are supported on your Linux system, you can use the `dmesg` command after a reboot. For example:

```
# dmesg | less
```

The following procedure was performed on a laptop that used ACPI to manage power events. It describes how to use the GNOME Power Manager applet on the desktop to monitor your battery.

> NOTE: If it seems either ACPI or APM are interfering with the power of your laptop, you can turn off each service when you boot your computer. Add `acpi=off` or `apm=off` to the end of the kernel line (from the GRUB boot screen or `/boot/grub/grub.conf` file) to turn off ACPI or APM, respectively.

# Using the Power Manager applet

If you are using the GNOME desktop, the GNOME Power Manager applet should automatically appear on your panel to keep track of the power levels of your battery (if a battery is present). The following procedure steps you through adding the monitor to your panel (if it is not already there) and configuring it to behave as you

+   1. Move your mouse over the battery icon in the top panel. A tooltip should show you whether or not your laptop is currently running on AC power and your battery's current charge level. Figure 10-7 shows an example of battery information for a laptop that is on AC power and that is in the process of recharging your battery.

![](bbox=[0.29, 0.737, 0.695, 0.837])

**Figure 10-7:** View battery status from the Power Management applet