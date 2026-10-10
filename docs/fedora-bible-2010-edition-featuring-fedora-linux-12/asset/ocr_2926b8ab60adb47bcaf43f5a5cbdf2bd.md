• **Advanced Power Management (APM)** — APM can be used to monitor the battery of your notebook and notify user-level programs to tell you when your battery is low. It can also be used to place your laptop into suspend mode.

• **Advanced Configuration and Power Interface (ACPI)** — Besides monitoring power features on your laptop, ACPI can also do thermal control and motherboard configuration, and change power states.

Many older laptops do not include support for ACPI in the BIOS so you must use APM to monitor and manage your batteries. For some newer laptops, ACPI may be required. In general, ACPI offers a more complete feature set for power management, but APM has more user-level support today.

To check whether ACPI or APM are supported on your Linux system, you can use the dmesg command after a reboot. For example, type:

```
```bash
# dmesg | less
```
```

Page through the output looking for lines beginning with text strings ACPI or apm. On a computer where APM wasn’t working, I saw the message “apm: overriden by ACPI.” When ACPI wasn’t working, I saw the message “ACPI: System description tables not found.”

The procedure in the following section was performed on a laptop that used ACPI to manage power events. It describes how to use the GNOME Power Manager applet on the desktop to monitor your battery.

> **NOTE:** If it seems that either ACPI or APM are interfering with the proper operation of your laptop, you can turn off either service when you boot your computer. Add either acpi=off or apm=off to the end of the kernel line (from the GRUB boot screen or the /boot/grub/grub.conf file) to turn off ACPI or APM, respectively.

# ### Using the Power Manager applet

If you are using the GNOME desktop, the GNOME Power Manager applet should automatically appear on your panel to keep track of the power levels of your battery (if a battery is present). The following procedure steps you through adding the monitor to your panel (if it is not already there) and configuring it to behave as you like.

+   1. Move the mouse pointer over the battery icon in the top panel. A tooltip should tell you whether or not your laptop is currently running on AC power and your battery’s current charge level.
+   
+   2. Right-click the battery icon and select Preferences. The Power Management Preferences window appears.
+   
+   3. Change any of the following values related to your battery monitor:

+   • **On AC Power** — From the On AC Power tab, you can select how many minutes of idle time should elapse before putting the computer or display to sleep. You can also