# Using the hwclock Command

Use the hwclock command to display or set your Linux system time, display or set your PC's hardware clock, or to synchronize the system and hardware times. To see your hardware date and time, use hwclock with its --show option like so:

```
$ sudo hwclock --show
Fri 27 Jan 2006 02:17:53 PM GMT -0.193809 seconds
```

Use hwclock with its --set and --date options to manually set the hardware clock like so:

```
$ sudo hwclock --set --date "01/27/06 08:00:00"
```

```
$ sudo hwclock --show
Tue 27 Jan 2006 08:00:08 AM GMT -0.151718 seconds
```

In these examples, the hardware clock has been set using hwclock, which is then used again to verify the new hardware date and time. You can also hwclock to set the Linux system date and time date using your hardware clock's values with the Linux system date and time.

For example, to set the system time from your PC's hardware clock, use the --hctosys option like so:

```
$ sudo hwclock --hctosys
```

To set your hardware clock using the system time, use the --systohc option like so:

```
$ sudo hwclock --systohc
```

# Changing the Time and Date

Ubuntu's graphical X tool named time-admin can be used to set your system date and time. The client is found in System, Administration, Time & Date.

After you press Enter, you are asked to enter your password. Type in your password and click the OK button. You will then see a window, as shown in Figure 2.16.

Set the date and time by using the Calendar and Time fields. You can also have your workstation obtain updated date and time information via the Internet by choosing Remote Time Servers under the Select Servers button. To do this, you need to have ntpd time daemon support installed. If it is not present, Ubuntu asks whether you want to retrieve it, and then installs it so that you can proceed. After it has been installed, restart the time-admin client and you will now be able to select specific Internet time servers for you to synchronize with.