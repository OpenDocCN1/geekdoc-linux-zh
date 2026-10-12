prevent new logins when the shutdown command is pending, you can create a text file called /etc/nologin with an appropriate message stating that a system shutdown has already been scheduled and that people should try to log in at a later time. Do not forget to rename or delete the /etc/nologin file after you reboot. If you are rebooting a server remotely, be absolutely sure to remove or rename this file prior to the actual shutdown. No user accounts except root are allowed to log in when this file is present. In fact, you may want to add the rm -f /etc/nologin at the end of the /etc/rc.local script and make sure that init runs it at the end of run level 3.

# Shutting down your system with init

You can run init to manually halt your system. For example, the following command halts the system immediately:

```
init 0
```

If you are running in a multiuser mode (run level 3), this command is not the best approach, because it does not inform the users on the system that the system is going to halt. Instead, you can use the shutdown command to halt the server, as described in the “Shutting down with the shutdown command” section earlier in this chapter.

# Canceling a shutdown

The shutdown command enables you to schedule a shutdown event at a later time (as discussed in the “Shutting down with the shutdown command” section earlier in this chapter). However, before the system actually shuts down, a need might arise to cancel the shutdown event; in such a case you issue another shutdown command with a -c option to cancel any scheduled shutdown event as follows:

```
shutdown -c
```

# Automatic shutdown on power failure

If you use a UPS (uninterruptible power supply) to provide backup power for your system and it uses a serial port-based UPS monitoring software