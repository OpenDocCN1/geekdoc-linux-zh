
![](img/8f9e74e2b343ff525bebfb720a3d8441_72_0.png)

FIGURE 2.14 Ubuntu's network-admin will help you set up an appropriate modem.

only on Windows. Despite the release of binary-only drivers to enable use of some of these modems, these devices remain the bane of Linux notebook and some desktop users.

You might find some support for Lucent (but not Lucent AMR), Motorola SM56-type, the IBM Mwave, and Conexant HSF (not HCF) controllers. At the time of this writing, there was no support for any 3Com or U.S. Robotics controllerless modems. For links to drivers and more information, browse to the Linux WinModem web page at http://www.linmodems.org.

## Configuring Power Management in Ubuntu

Advanced Configuration and Power Interface (ACPI) enables workstations and servers to automatically turn off when instructed to shut down. Most often used by Linux mobile users, ACPI can help extend battery sessions through the use of intelligent storage-cell circuitry, CPU throttling (similar to, but not the same as safety thermal throttling incorporated by Intel in Pentium III and IV CPUs), and control of displays and hard drives.

Most PCs support ACPI via the BIOS and hardware. ACPI support is configured, enabled, and incorporated in the Linux kernel.

ACPI information is constantly available through the acpi command, which looks like this:

```
$ acpi -V

Battery 1: charged, 100%
Thermal 1: ok, 47.0 degrees C
AC Adapter 1: on-line
```

This example provides information such as battery charge status, percentage of charge, as well as current system temperature and status of the AC adapter.

Alternatively, you can use the GUI tool that Ubuntu provides, which can be found under the System, Preferences menu as the Power Management option (shown in Figure 2.15).

![](img/8f9e74e2b343ff525bebfb720a3d8441_73_0.png)

FIGURE 2.15 Gnome Power Management allows you to monitor battery status and configure specific power-related actions, such as closing the lid of your laptop or pressing the power button.

Fortunately, Ubuntu provides good support for suspend and hibernate. Suspend means that your computer writes its current state to memory and goes into a low power mode, while Hibernate writes the current state of the system to disk and powers off the computer. Either way, your computer will start much faster the next time you go to use it.

## Setting the Date and Time

The Ubuntu installer queries during installation for default time zone settings, and whether your computer's hardware clock is set to Greenwich mean time (GMT)—more properly known as UTC or coordinated universal time.

Linux provides a system date and time; your computer hardware provides a hardware clock-based time. In many cases, it is possible for the two times to drift apart. Linux system time is based on the number of seconds elapsed since January 1, 1970. Your computer's hardware time depends on the type of clock chips installed on your PC's motherboard, and many motherboard chipsets are notoriously subject to drift.

- hwclock—A root command to display, set, adjust, and synchronize hardware and system clocks
- time-admin—Ubuntu's graphical date, time, and network time configuration tool

### Using the date Command

Use the date command to display or set your Linux system time. This command requires you to use a specific sequence of numbers to represent the desired date and time. To see your Linux system's idea of the current date and time, use the date command like this:

```
$ date
Tue Mar 18 20:01:43 GMT 2008
```

To adjust your system's time (say, to March 19 2008 at 8 a.m.), use a command line with the month, day, hour, minute, and year, like so:

```
$ sudo date 031900002008
Wed Mar 19 08:00:00 GMT 2008
```

### Using the hwclock Command

Use the hwclock command to display or set your Linux system time, display or set your PC's hardware clock, or to synchronize the system and hardware times. To see your hardware date and time, use hwclock with its --show option like so:

```
$ hwclock --show
Tue 18 Mar 2008 20:04:27 GMT -0.034401 seconds
```

Use hwclock with its --set and --date options to manually set the hardware clock like so:

```
$ sudo hwclock --set --date '03/19/08 08:00:00'
$ hwclock --show
Wed 19 Mar 2008 08:00:08 AM GMT -0.151718 seconds
```

In these examples, the hardware clock has been set using hwclock, which is then used again to verify the new hardware date and time. You can also use hwclock to set the Linux system date and time using your hardware clock's values with the Linux system date and time.

For example, to set the system time from your PC's hardware clock, use the --hctosys option like so:

```
$ sudo hwclock --hctosys
```

To set your hardware clock using the system time, use the --systohc option like so:

```
$ sudo hwclock --systohc
```
