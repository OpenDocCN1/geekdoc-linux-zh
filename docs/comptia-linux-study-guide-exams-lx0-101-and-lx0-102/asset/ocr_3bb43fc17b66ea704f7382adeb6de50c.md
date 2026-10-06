hwclock [options]

You can specify options to accomplish several goals:

**Show the Hardware Clock** View the hardware clock, pass the -r or --show option. The time is displayed in local time, even if the hardware clock is set to UTC.

**Set the Hardware Clock Manually** To set the hardware clock to a date you specify, you need two options:--set and --date=newdate. The newdate is in the format that the date program accepts.

**Set the Hardware Based on the Software Clock** If you set the software clock, you can synchronize the hardware clock to the same value with the --systoch option.

**Set the Hardware Clock Based on the Hardware Clock** If your hardware clock is accurate but your software clock isn't, you can use the --hwclock option to set the software clock to the hardware clock's value. This option is often used in SysV startup script to set the system clock when you compute the first boots.

**Specify UTC or Local Time** You can tell Linux to treat the hardware clock as storing UTC by using the --utc option or to treat it as holding local time by using the --localtime option. The default is whichever was last used when the hardware clock was set.

Ordinarily, you won't use hwclock directly often. You may need to use a daylight shift if you maintain your hardware clock in local time, but most distributions scripts manage this task automatically. You may also want to use it once in a while to keep the hardware clock from drifting too far from an accurate time; but again, many distributions do this automatically as part of the system procedure.

![](bbox=[0.137, 0.574, 0.235, 0.633])

> You can also set the hardware clock via your computer's firmware utility. Consult your motherboard or hardware manual for details. You must reboot the system to do this, typically pressing the Delete or other key at a critical time early in the boot process (before your boot loader takes over). You must then find the time option and set it appropriately. If Linux is using UTC, remember to set the clock to UTC rather than local time.

# Using NTP

Typically, a clock on an isolated computer needn't be set with any great precision. It doesn't really matter if the time is off by a few seconds, or a few minutes, so long as the time is reasonably consistent on that computer for the purpose of cron, other scheduling tools, and time stamps. Sometimes, though, maintaining a truly accurate system time is important. This is true for a few scientific, business, and industrial applications (such as astronomical measurements or determining the start and stop times for broadcasts). In a networked environment, maintaining the correct time can be more important. Time stamps on files may become confused if a server and its clients have different times, for instance. Worse a few protocols, such as the Kerberos security suite, embed time