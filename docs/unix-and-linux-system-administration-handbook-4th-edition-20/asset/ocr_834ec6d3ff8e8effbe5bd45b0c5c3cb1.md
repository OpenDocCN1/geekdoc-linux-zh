# AIX logging and error handling

Another issue in kernel logging is the appropriate management of the system console. As the system is booting, it's important for all the output to come to the console. However, once the system is up and running, console messages may be more an annoyance than a help, particularly if the console is used for logins.

Both **dmesg** and **klog** let you set the kernel's console logging with a command-line flag. For example:

```
sudo dmesg -n 2
```

Level 7 is the most verbose and includes debugging information. Level 1 includes only panic messages (the lower-numbered levels are the most severe). All kernel messages continue to go to the central buffer (as syslog) regardless of whether they are forwarded to the console.

The kernel provides some control files underneath the **/proc/sys** directory to allow floods of repeated messages to be choked off at the source. See the section **Tuning Linux kernel parameters** starting on page 421 for more information about the general mechanism through which kernel parameters are set. The specific control files are **/proc/sys/kernel/printk_ratelimit**, which specifies the minimum number of seconds that must elapse between kernel messages once the choke has been activated (default 5), and **/proc/sys/kernel/printk_ratelimit_burst**, which specifies how many messages to let through before activating the choke (default 10). These parameters are advisory, so do not absolutely guarantee that a heavy flow of messages will be statched. They also apply only to messages created in the kernel by the `printk()` function.

Logging for the startup scripts is unfortunately not well managed as kernel logging.

Red Hat Enterprise Linux uses an **initlog** command to capture the output of startup commands and shut off it to syslog. Unfortunately, **initlog** must be mentioned explicitly whenever a command is run, so the information comes at the cost of some complexity. Events make their way to **/var/log/boot.log**.

Our example systems make no coherent effort to capture a history of the startup scripts' output. Some information is logged by individual commands and daemons, which might go unrecorded.

# 11.3 AIX LOGGING AND ERROR HANDLING

![](bbox=[0.181, 0.796, 0.236, 0.836])

AIX manages its logs differently from other UNIX systems. Although syslog is present in the default installation, it is not configured. AIX relies on a proprietary daemon called **errdemon** for system error reporting. **errdemon** is intended to handle system diagnostic messages (as notifications of hardware failures or full filesystems) but not to handle logging for individual daemons. Thus, the prudent system administrator will rely on the wisdom of **errdemon** for