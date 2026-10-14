Fortunately, Ubuntu provides good support for suspend and hibernate. Suspend means that your computer writes its current state to memory and goes into a low power mode, while Hibernate writes the current state of the system to disk and powers off the computer. Either way, your computer will start much faster the next time you go to use it.

# Resetting the Date and Time

The Ubuntu installer queries during installation for default time zone settings, and whether your computer's hardware clock is set to Greenwich mean time (GMT)—more properly known as UTC or coordinated universal time.

Linux provides a system date and time; your computer hardware provides a hardware clock-based time. In many cases, it is possible for the two times to drift apart. Linux system time is based on the number of seconds elapsed since January 1, 1970. Your computer's hardware time depends on the type of clock chips installed on your PC's motherboard, and many motherboard chipsets are notoriously subject to drift.

Keeping accurate time is not only important on a single workstation, but also critically important in a network environment. Backups, scheduled downtimes, and other network-wide actions need to be accurately coordinated.

Ubuntu provides several date and time utilities you can use at the command line or during an X session, including these:

+   date—Used to display, set, or adjust the system date and time from the command line
+   hwclock—A root command to display, set, adjust, and synchronize hardware and system clocks
+   time-admin—Ubuntu's graphical date, time, and network time configuration tool

# Using the date Command

Use the date command to display or set your Linux system time. This command requires you to use a specific sequence of numbers to represent the desired date and time. To see your Linux system's idea of the current date and time, use the date command like this:

```
$ sudo date
Wed Jan 10 14:17:01 EDT 2005
```

To adjust your system's time (say, to January 27, 2006 at 8 a.m.), use a command line with the month, day, hour, minute, and year, like so:

```
$ sudo date 012600002003
Fri Jan 27 08:00:00 EDT 2006
```