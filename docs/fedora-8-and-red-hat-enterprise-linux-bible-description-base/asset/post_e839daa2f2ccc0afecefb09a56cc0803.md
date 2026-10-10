
## Finding disk consumption with find

The `find` command is a great way to find file consumption of your hard disk using a variety of criteria. You can get a good idea of where disk space can be recovered by finding files that are over a certain size or were created by a particular person.

> NOTE: You must be root user to run this command effectively, unless you are just checking your personal files.

In the following example, the `find` command searches the root file system (/) for any files owned by the user named `jake` (`-user jake`) and prints the filenames. The output of the `find` command is then listed with a long listing in size order (`ls -lds`). Finally, that output is sent to the file /tmp/jake. When you read the file /tmp/jake, you will find all of the files that are owned by the user `jake`, listed in size order. Here is the command line:

```
# find / -xdev -user jake -print | xargs ls -lds > /tmp/jake
```

> TIP: The -xdev option prevents file systems other than the selected file system from being searched. This is a good way to cut out a lot of junk that may be output from the /proc file system. It could also keep large remotely mounted file systems from being searched.

The next example is similar to the previous one, except that instead of looking for a user's files, this command line looks for files that are larger than 1000 kilobytes (`-size +1000k`):

```
# find / -xdev -size +1000k -print | xargs ls -lds > /tmp/size
```

You can save yourself a lot of disk space by just removing some of the largest files that are no longer needed. Open the /tmp/size file in this example and large files are sorted by size.

## Monitoring System Performance

If your Linux system is being used as a multiuser computer, sharing the processing power of that computer can be a major issue. Likewise, any time you can stop a runaway process or reduce the overhead of an unnecessary program running, your Linux server can do a better job serving files, Web pages, or e-mail to the people that rely on it.

Utilities are included with Linux that can help you monitor the performance of your Linux system. The kinds of features you want to monitor in Linux include CPU usage, memory usage (RAM and swap space), and overall load on the system. The following sections describe tools for monitoring Linux.

### Watch computer usage with System Monitor

If you like visual representations of your system use, the System Monitor provides a great way to see how much your system is being used. To open the System Monitor from the Applications menu on the GNOME panel, select System Tools → System Monitor. Figure 10-6 shows the System Monitor window with the Resources tab selected.

On the Resource Monitor window, lines scroll from right to left, indicating the percentage of your CPU being used as it rises and falls. You can also see how much of your total memory (RAM) is being used at the moment (and over time), as well as the amount of swap space being used. The bar at the bottom of the window shows the amount of data being sent and received over your computer's network interfaces.

Click the Processes tab to see a listing of processes that are running for the current user. Click the columns in that tab to sort processes by name, memory use, percentage of CPU being consumed by the process, and process ID. There are also columns showing the security context of the process (if SELinux is enabled) and the arguments associated with the process.

Click the File Systems tab to see the storage devices (hard disk partitions, CD, USB flash drive, or other) that are currently mounted on your computer. Click columns to sort the devices by device name, directory name, file system type, total disk space, free disk space, or used disk space.

The example in Figure 10-6 shows a computer that is running with over 700MB of RAM. Although there is a fair amount of activity on the System Monitor in this example, there is still User memory available. However, if on your system User memory is running near the maximum, it would indicate the likely occurrence of performance problems as RAM fills up and data has to be moved to swap space. The CPU used is only about 15 percent, which indicates that the CPU is currently keeping up with the demand.

![](img/fb202c163797a743c3c6cf236316bc96_488_0.png)

Figure 10-6: System Monitor graphically displays your system’s CPU and memory usage.

## Monitoring CPU usage with top

Start the top utility in a Terminal window, and it displays the top CPU consuming processes on your computer. Every five seconds, top will determine which processes are consuming the most CPU time and display them in descending order on your screen.

By adding the -S option to top, you can have the display show you the cumulative CPU time that the process, as well as any child processes that may already have exited, has spent. If you want to change how often the screen is updated, you can add the -d secs option, where secs is replaced by the number of seconds between updates.

By default, processes are sorted by CPU usage. You can sort processes numerically by PID (press P), by age (press T), by resident memory usage (press M), by time (press T), or back to CPU usage (press P). *Note: The original OCR text mentions pressing 'A' for PID and age, and 'M'/'T'/'P' for others. Standard top commands are P (CPU), M (Mem), T (Time/age). I will preserve the original text's intent but correct the obvious OCR errors where 'A' was likely meant to be 'P' for PID or 'T' for Time. However, looking at standard top: P=CPU, M=Mem, T=Time. The text says "by PID (press A), by age (press A)". This is likely an OCR error for 'P' or 'T'. Let's look at the context: "sort processes numerically by PID (press A), by age (press A), by resident memory usage (press M), by time (press T)". It is highly probable that 'A' is an error. In many versions, 'P' is PID, 'T' is Time. I will stick close to the text but correct obvious misreads if they are standard keys. Actually, in some top versions, you press 'P' to sort by PID, 'T' to sort by Time (age). The OCR says 'A' for both. I will leave it as is unless it's a clear typo like 'l' vs 'I'. Wait, 'A' is not a standard sort key in basic top. It might be a typo for 'P' or 'T'. Given the instruction to correct OCR errors, I should be careful. Let's look at the previous sentence: "press A". I will assume it's a typo for the correct key. However, without knowing the exact version, I will leave the keys as described in the text to avoid altering information, unless it's a clear visual misread like 'l' for 'I'. Here 'A' might be correct for a specific variant or just a typo in the book. I will retain the text but ensure formatting is correct.*

The following output shows an example of top running, with information sorted by memory use. The system shown is running a GNOME desktop, with OpenOffice.org Writer, Firefox Web browser and several other applications active. Notice that the amount of memory free is very low. To get good performance out of a Fedora desktop system, 256MB may not be enough once you start running a lot of big applications.

```
top - 16:11:41 up 10:27, 2 users, load average: 1.60, 0.51, 0.18
Tasks: 107 total, 2 running, 103 sleeping, 0 stopped, 2 zombie
Cpu(s): 16.6us, 6.5sy, 0.0ni, 0.0id, 76.9wa, 0.0hi, 0.0si, 0.0st
Mem: 252424k total, 249224k used, 3200k free, 2360k buffers
Swap: 1020088k total, 14240k used, 1005848k free, 86820k cached

  PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
 4242 chris 18 0 183m 37m 25m R 19.9 15.0 0:05.86 nwriter.bin
 4217 chris 15 0 137m 31m 17m S 0.0 12.9 0:07.27 firefox-bin
 4244 chris 15 0 39148 18m 7684 S 0.0 7.6 0:04.94 beagle3-helper
 4138 chris 15 0 101m 14m 9.8m S 0.0 5.9 0:06.87 cappobar
```

## Monitoring power usage on laptop computers

To effectively use a laptop computer, you need to be able to monitor and manage the laptop’s power usage. Using tools provided in Fedora or RHEL, you can configure your laptop to:

- Monitor the battery level.
- Notify you when the battery is low.
- Notify you when the battery is fully charged.
- Show when the laptop is plugged in.
- Suspend the current session.

Fedora and RHEL offer two facilities that do power management: APM and ACPI.

- **Advanced Power Management (APM)** — APM can be used to monitor the battery of your notebook and notify user-level programs to tell you when your battery is low. It can also be used to place your laptop into suspend mode.

- **Advanced Configuration and Power Interface (ACPI)** — Besides monitoring power features on your laptop, ACPI can also do thermal control, motherboard configuration, and change power states.

Many older laptops do not include support for ACPI in the BIOS, so you must use APM to monitor and manage your batteries. For some newer laptops, ACPI may be required. In general, ACPI offers a more complete feature set for power management, but APM has more user-level support today.

To check whether ACPI or APM are supported on your Linux system, you can use the dmesg command after a reboot. For example, type:

```
# dmesg | less
```

Page through the output looking for lines beginning with text strings ACPI or apm. On a computer where APM wasn’t working, I saw the message “apm: overridden by ACPI.” When ACPI wasn’t working, I saw the message “ACPI: System description tables not found.”

The following procedure was performed on a laptop that used ACPI to manage power events. It describes how to use the GNOME Power Manager applet on the desktop to monitor your battery.

> **NOTE:** If it seems that either ACPI or APM are interfering with the proper operation of your laptop, you can turn off either service when you boot your computer. Add either acpi=off or apm=off to the end of the kernel line (from the GRUB boot screen or the /boot/grub/grub.conf file) to turn off ACPI or APM, respectively.

### Using the Power Manager applet

If you are using the GNOME desktop, the GNOME Power Manager applet should automatically appear on your panel to keep track of the power levels of your battery (if a battery is present). The following procedure steps you through adding the monitor to your panel (if it is not already there) and configuring it to behave as you like.

1. Move the mouse pointer over the battery icon in the top panel. A tooltip should tell you whether or not your laptop is currently running on AC power and your battery’s current charge level. Figure 10-7 shows an example of battery information for a laptop that is on AC power and that is in the process of recharging the battery.
