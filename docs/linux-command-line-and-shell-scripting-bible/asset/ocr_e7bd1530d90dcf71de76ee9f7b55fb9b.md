# Script Control

The anacron program uses timestamps to determine if a scheduled job has been run at the proper interval. If it determines that a job missed a scheduled running, it automatically runs the job as soon as possible. This means that if your Linux system is turned off for a few days, it starts back up any jobs to schedule during the time it was off automatically running.

This is a feature that's often used for scripts that perform routine log maintenance. If the system is always off when the script should run, the logs would never get trimmed and could grow to undesirable sizes. With anacron, you are guaranteed that the logs will be trimmed at least each time the system is started.

The anacron program has its own table (usually located at /etc/anacontab) to specify jobs. Almost all Linux distributions, this table is only accessible by the root user. The format of the anacron table is slightly different from that cron table:

```
period delay identifier command
```

The period entry defines how the job should be run, specified in days. The delay entry specifies how many minutes after the anacron program determines that a command should be run it actually run. This allows you to set different delay values for different commands so that you don't have them all running as soon as you turn on the Linux system.

The identifier entry is a unique non-blank character string to uniquely identify the job in log messages and return e-mails.

# Start At the Beginning

The last method of starting scripts is to have your script run automatically either as soon as the Linux system boots or whenever a user starts a new bash shell session. Starting scripts at boot is usually reserved for special scripts that perform system functions, such as configuring a network interface or starting a server process. However, it's possible that you'll need to perform a function every time the Linux system boots, such as resetting a custom log file or starting a custom application.

The ability to run a script every time a user starts a new shell (even just when a specific user starts a bash shell) also come in handy. There are times when you want to set filters for a shell session or ensure that a specific file has been set.

This section describes how to configure your Linux system to run your scripts either at boot or each time a new bash shell starts.

# Starting your scripts at boot

Before you can get your script to start at boot time, you'll need to know a little bit about how the Linux boot process works. There's a specific order that Linux uses to start scripts at boot time, and knowing that process can help you in getting your script to perform the way you want it.

355