```
modprobe i2c-isa
modprobe via686a
```

You can then use the sensors command's `-f` option to view various component temperatures in Fahrenheit, like this:

```
$ sensors -f
via686a-isa-6000
Adapter: ISA adapter
Algorithm: ISA algorithm
2.0V:	+1.36 V (min = +1.79 V, max = +2.18 V)
2.5V:	+2.49 V (min = +2.24 V, max = +2.74 V)
I/O:	+3.28 V (min = +2.95 V, max = +3.62 V)
+5V:	+5.02 V (min = +4.47 V, max = +5.49 V)
+12V:	+11.62 V (min = +10.79 V, max = +13.18 V)
Case Fan: 2700 RPM (min = 48214 RPM, div = 2)
CPU Fan: 3497 RPM (min = 67500 RPM, div = 2)
SYS Temp: +98.8°F (limit = +295°F, hysteresis = -95°F)
CPU Temp: +98.8°F (limit = +295°F, hysteresis = -95°F)
SBr Temp: +79.3°F (limit = -74°F, hysteresis = -95°F)
```

Monitoring your system's hardware can be critically important, especially if you overclock the Central Processing Unit (CPU) in order to gain performance.

# ## Resetting the Date and Time

The Fedora installer will query you during installation for default time zone settings, and whether or not your computer's hardware clock is set to Greenwich Mean Time (GMT)—more properly known as $UTC$, or Coordinated Universal Time.

Linux provides a system date and time; your computer hardware provides a hardware clock-based time. In many cases, it is possible for the two times to drift apart. Linux system time is based on the number of seconds elapsed since Jan. 1, 1970. Your computer's hardware time depends on the type of clock chips installed on your PC's motherboard, and many motherboard chipsets are notoriously subject to drift.

Keeping accurate time is not only important on a single workstation, but also critically important in a network environment. Backups, scheduled downtimes, and other network-wide actions need to be accurately coordinated.

Fedora provides several date and time utilities you can use at the command line or during an X session, including these:

+   - `date`—Used to display, set, or adjust the system date and time from the command line
+   - `hwclock`—A root command to display, set, adjust, and synchronize hardware and system clocks
+   - `system-config-date`—Red Hat's graphical date, time, and network time configuration tool