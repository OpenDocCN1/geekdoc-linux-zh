# Chapter 6 • Configuring the X Window System, Localization, and Printing

same time zone as you. For instance, the New_York time file works if you're in Boston, Philadelphia, Cincinnati, or any other city in the same (Eastern) time zone as New York.

+   4. If a localtime file exists in /etc, delete it or rename it. (For instance, type `localtime`).

+   5. Create a symbolic link from your chosen time zone to the /etc/localtime file. For instance, you can use `ln -s /usr/share/zoneinfo/US/Eastern localtime` to set up a computer in the U.S. Eastern time zone. Alternatively, you can copy a file (cp) rather than a symbolic link (ln -s). If /etc and your target file are on the same filesystem, you can create a hard link rather than a symbolic link if you.

At this point, your system should be configured to use the time zone you've selected. If you changed times, you should be able to see the difference by typing date, described earlier. The time zone on your system should change by issuing this command before you change the /etc/localtime file or link. The time should also change by the number of hours between the time zones you've selected (give a bit for the time it takes to change the time zone).

In addition to /etc/localtime, some distributions use a secondary file with text-mode time zone data. This file is called /etc/timezone on Debian and its derivatives. On Fedora and related distributions, it's /etc/sysconfig/clock. This file contains one or two with the name of the time zone, sometimes in the form of a variable assignment. For instance, the /etc/timezone file on Ubuntu system looks like this:

America/New_York

This file provides a quick way to change your time zone. It should also be updated when you change your time zone, less-level configuration tools could be confused. For a program called tzsetup, tzselect, tzconf, or something similar. Typically, these programs ask you for your location in several steps (starting with your continent, then name, and perhaps you for your state or city) and create an appropriate symbolic link.

# Setting an Individual Login's Time Zone

One wrinkle on time zone issues is the TZ variable. (Chapter 9 covers environment variables in more detail.) This environment variable holds time information in three of formats:

+   * The most common format on Linux is `:filename`, as in :`/usr/share/zoneinfo/Europe/London`. This tells the system that the time zone is the one described in the specified file.

+   * A second format, common on non-Linux systems, is `std offset`, where `std` is a three-character or longer time zone name (such as EST) and `offset` is a time relative to UTC, with positive values representing offsets of the Prime Meridian and negative values being east of it. For instance, EST+5 specifies U.S. Eastern Time. This format is used when daylight saving time is not in effect.