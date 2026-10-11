Now, before you start your xntpd daemon, there are a few steps you need to complete. The NTP protocol is a little bit fussy. If the time on your server is more than 17 minutes out of synchronization with the time on the NTP time provider, the NTP protocol considers the time source “in sane” and will refuse to synchronize.

Therefore, you need to set your system time as closely as possible to the time provider’s time before you start the xntpd daemon. This involves three steps:

+   1. Configure your server’s time zone by entering `tzselect` at a shell prompt. Follow the time zone wizard prompts to set your time zone, as shown in Figure 3.38.

![](bbox=[0.04, 0.35, 0.21, 0.41])

![](bbox=[0.32, 0.35, 0.83, 0.6])

+   2. Manually set your server’s system time using the `date` command. The `date` command expects you to provide the current date and time in the format `mmddhhmmyyyy`. For example, if the current date and time is August 30, 2004, 8:30 p.m., you would enter `date 083020302004`. Note that the hour is specified using the 24-hour clock.

+   3. Perform a one-time synchronization with the NTP time provider by entering `ntpd time_provider_IP_address`. For example, if your time provider’s IP address is `10.0.0.1`, you would enter `ntpd 10.0.0.1`. You may have to run this command several times. As a general rule of thumb, you should rerun the command until the offset reported by this command is less than 1 second.

> If the `xntpd` daemon is running, you can’t run the `ntpd` command.