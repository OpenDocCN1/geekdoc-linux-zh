# Changing Runlevels with telinit

No matter what runlevel you start in, you can change from one runlevel to another with the telinit command. If your default runlevel is 3, you power up in runlevel 3, but you can change to, say, runlevel 5 with telinit 5. The command telinit 0 shuts down your system. In the next example, the telinit command changes to runlevel 1, the administrative state:

```
# telinit 1
```

telinit is really a symbolic link (another name for a command) to the init command. The init command performs that actual startup operations and is automatically invoked when your system starts up. Though you could use init to change runlevels, it is best to use telinit. When invoked as telinit, init merely changes runlevels.

# runlevel Command

Use the runlevel command to see what state you are currently running in. It lists the previous state followed by the current one. If you have not changed states, the previous state will be listed as N, indicating no previous state. This is the case for the state you boot up in. In the next example, the system is running in state 3, with no previous state change.

```
# runlevel
N 3
```

# Shutdown

Although you can power down the system with the telinit command and the 0 state, you can also use the shutdown command. The shutdown command has a time argument that gives users on the system a warning before you power down. You can specify an exact time to shut down, or a period of minutes from the current time. The exact time is specified by hh:mm for the hour and minutes. The period of time is indicated by a + and the number of minutes. The shutdown command takes several options with which you can specify how you want your system shut down. The -h option, which stands for halt, simply shuts down the system, whereas the -r option shuts down the system and then reboots it. In the next example, the system is shut down after ten minutes.

```
# shutdown -h +10
```

To shut down the system immediately, you can use +0 or the word now. The following example shuts down the system immediately, and then reboots.

```
# shutdown -r now
```

With the shutdown command, you can include a warning message to be sent to all users currently logged in, giving them time to finish what they are doing before you shut them down.

```
# shutdown -h +5 "System needs a rest"
```

If you do not specify either the -h or the -r options, the shutdown command shuts down the multiuser mode and shifts you to an administrative single-user mode. In effect, your system state changes from 3 (multiuser state) to 1 (administrative single-user state). Only the root user is active, allowing the root user to perform any necessary system administrative operations with which other users might interfere.