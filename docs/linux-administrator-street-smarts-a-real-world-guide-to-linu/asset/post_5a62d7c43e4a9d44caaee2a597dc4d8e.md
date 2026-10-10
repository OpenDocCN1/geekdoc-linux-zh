
to determine whether your system is using Advanced Power Management (APM) or the newer Advanced Configuration and Power Interface (ACPI) subsystem.

## Scope of Task

This task requires investigating your system with a few commands. You may then want to edit some configuration files or startup scripts. You'll need to use either APM or ACPI, and in either case you should also investigate options for managing your hard disk's power consumption.

## Duration

This task should take half an hour to an hour to complete. If you need to configure power management on many systems, each one will take just a few minutes—more time if the systems are substantially different from each other, but very little time if they're nearly identical to one another.

## Setup

Log into the computer and acquire `root` privileges. No special hardware or software configuration is required, although if you're running a particularly old or bare-bones Linux distribution, you might need to install APM or ACPI software. Although the scenario describes a laptop computer, you can investigate power management features even on a desktop computer.

## Caveats

As always, working as `root` can be dangerous. Power management tools are unlikely to cause catastrophic problems, although you could accidentally set some inconvenient options, such as a too-short hard disk power-down time, which will cause sluggish and erratic performance.

## Procedure

To use power management features, you'll need to activate kernel support and then investigate APM and ACPI options on your system. You'll also want to modify your hard disk options for managing hard disk power consumption.

![](img/f430a19bdf014c43ad7c2d594afd5b21_115_0.png)

> Distributions and GUI environments are increasingly providing point-and-click interfaces to power management tools. These interfaces can be convenient and useful, but they differ from one distribution or environment to another.

## Activating Kernel Support

Both APM and ACPI rely on kernel features to work. General kernel configuration procedures are described earlier, in Task 2.6, “Configure and Compile a Kernel.” The power management features can be compiled into the kernel by activating appropriate options under the Power Management Options menu—both APM and ACPI have their own submenus with options to enable assorted specific features, such as support for fan control, or to enable basic support at system boot time. Generally speaking, enabling an option will do no harm, even if it doesn't apply to your system. You should read the description to see if it applies, though. A few APM options in particular can cause problems. The RTC Stores Time In GMT option can cause your system time to be set strangely after a suspend operation if it’s set incorrectly, and a few other options can cause problems with some hardware, as detailed in their descriptions.

When you configure your kernel, keep in mind that Linux will use APM or ACPI, but not both. In practice, whichever kernel system loads first will control the computer’s power management. The simplest way to deal with this situation is to compile support for one protocol or another, not both. Another approach is to compile both systems as modules and load only the desired modules at boot time. In practice, if you try to use APM or ACPI features, as described in the next couple of sections, and they don’t work, the cause could be the presence of support for the other system in the kernel.

If you’re using your distribution’s stock configuration, chances are it includes a reasonable default APM/ACPI configuration. It may try loading ACPI and then use APM as a fallback, for instance. In any event, you can try using one set of tools and then the other if that doesn’t work. You may need to consult distribution-specific documentation to learn the details of how it’s configured on your system, though.

## Using APM

To use APM features effectively, you need some way to tell the computer when to enter power-conserving states. This task is accomplished with the apmd package, which ships with most Linux distributions and may be installed automatically. The main apmd program is a daemon, which means that it runs in the background waiting for some event to occur. Most daemons, including apmd, should be started when the computer boots. Once running, apmd monitors the system’s battery status, and if the battery’s charge gets too low, apmd kicks the system into a suspend mode in which most functions are shut down and only the system’s RAM is maintained.

The apmd program will also suspend the hard disk if it’s gone unused for a long enough time. (You can also use the hdparm utility to control hard disk power management more directly.) If you want to manually control APM features, you can do so with the apm utility. Typing this command presents basic power management information, such as how much battery power is left. The -s and -S parameters cause the system to go into suspend and standby modes, respectively. Suspend mode shuts off power to most devices, leaving only the CPU and memory operating, and those at minimum power. Standby mode leaves more devices powered up, so the system can recover more quickly, but there’s less power savings in this mode. A fully charged laptop can usually last several hours in standby mode and a day or more in suspend mode. Many laptops include a key sequence that will force the system into suspend or standby mode. In most cases, apmd will detect such a keystroke and honor the request. Consult your laptop’s documentation for details.

## Using ACPI

Linux’s ACPI handling is similar to its APM handling in broad strokes, but of course the details differ. In particular, an ACPI daemon runs instead of an APM daemon. The acpid program is a common ACPI daemon. This daemon is controlled through files in /etc/acpi/events. All the files in this directory whose names do not begin with a dot ( . ) are parsed and interpreted as sets of events and actions to be taken in response to each event. Each event line begins with the string event=, and each action line begins with action=. The actions point to scripts or Linux commands.

One simple ACPI configuration file contains nothing but comments and a very simple action/event pair, as seen here:

```
event=.*
action=/etc/acpi/default.sh %
```

This configuration essentially passes all responsibility over to a shell script, `/etc/acpi/default.sh`. A shell script can be more complex than the simple default ACPI parser, but this approach may be overkill for you.

![](img/f430a19bdf014c43ad7c2d594afd5b21_117_0.png)

**Event names are not fully standardized.** Thus, you may need to monitor your own system to identify important events' names. Check the `/proc/acpi/event` file when you perform an ACPI-related event, such as closing the lid of a laptop computer. This file should change to display the event name, which you can then reference in your Linux ACPI configuration file.

You can use files in the `/proc/acpi` directory to monitor your system and to change defaults. Try using `cat` to view the contents of some of these files, as in **`cat /proc/acpi/event`** to view recent ACPI events. Various tools can link into these files to provide you with useful information, such as your CPU's temperature and battery status. The `acpi` program is one of these tools; type `acpi -V` to have the system display all the information it can.

## Setting Hard Disk Options

You can use the `hdparm` utility to tell hard disks to enter a low-power suspend mode after a specified period of inactivity. To do so, use the `-S` option to `hdparm`, which takes a value from Table 2.4 to specify the idle time before the drive enters suspend mode.

**TABLE 2.4 hdparm -S Options**

| Value | Meaning |
| :--- | :--- |
| 0 | Power-saving mode disabled; disk doesn't power down. |
| 1-240 | Suspend mode entered in multiples of 5 seconds; for instance, 12 means to enter suspend mode after 60 seconds of inactivity. |
| 241-251 | Enter suspend mode after 1 to 11 units of 30 minutes of inactivity. |
| 252 | Enter suspend mode after 21 minutes of inactivity. |
| 253 | Enter suspend mode after a vendor-defined time. |
| 255 | Enter suspend mode after 21 minutes and 15 seconds of inactivity. |
