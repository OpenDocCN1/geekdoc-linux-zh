power-cycling the box, or cutting power to the machine and then powering it back on when not in a halted state, will result in errors the next time the machine boots up.

The actual shutdown process is accomplished by sending a signal to the init daemon requesting a change in run level. With the -h, or halt command, the shutdown process changes the run level to 0, where it becomes safe to power down.

# ## Using Additional Shutdown Options

Another option for shutting down a Linux machine is to have a delay in the shutdown period. This is especially useful when multiple users are logged in. A default message is printed to each user's screen specifying when the machine will be shut down.

Issuing the shutdown command with the -k flag does not actually shut down the system, but will send the warning message to all the users who are logged in. This is useful if you want to shut down the machine for a certain period of time, without exactly being sure when the process will occur. The flag is also useful if you simply want to inform the users that the machine will be shut down shortly and that they need to log off.

If you are sure that time the machine will be shut down, you can issue the shutdown command with the -t option and then the number of seconds later when it will be powered down. Here is an example telling the init process to shut down the machine in five minutes:

```
# shutdown -t 300 -h
```

The shutdown option has a couple other flags that make shutting down the machine easier on both the administrator and clients. Instead of sending the default warning message, you can send a customized message informing all the users at all remote login terminals why the machines will be shut down. Here is an example telling all currently logged-in users that this particular Linux box will be shut down at 11:00 p.m. for a hardware upgrade: No particular flag is needed to send users a specific message.

```
# shutdown -h 23:00 'Performing a hardware upgrade at midnight'
```

Similar to a cron job or at command, the signal sent to init will tell it to wait until 11:00 p.m. before changing the run level to 0.