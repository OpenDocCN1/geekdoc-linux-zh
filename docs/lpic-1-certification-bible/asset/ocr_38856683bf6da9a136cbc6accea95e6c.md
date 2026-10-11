| Action | Function |
| --- |
| respawn | The process will be restarted whenever it is terminated. You will see this used with the getty login processes, which need to be regenerated each time. |
| wait | The process is started once, and then init will wait until it is terminated. |
| once | The process will be executed only once, when the runlevel is entered. |
| boot | The process will be executed at boot, and any runlevel field entries will be ignored. |
| bootwait | The process is started at boot, and init will wait for it to complete before continuing. |
| initdefault | Specifies the runlevel to enter when the system is booted. |
| sysinit | This entry will be executed at boot, before any other boot or bootwait entries. The runlevel field is ignored. |
| powerwait | This entry will be processed when the power to the system goes down, as reported by a UPS. init will wait for this to complete before continuing. |
| powerfail | The same as powerwait, but init does not wait for this process to complete. |
| powerokwait | This process is executed when the power has been restored to the system. init will wait for its completion. |
| powerfailnow | This process is executed when the UPS signals to the system that the battery is almost exhausted. |
| ctrlaltdel | This entry will be processed when a user presses the Ctrl-Alt-Delete key combination. |
| kbrequest | Execute the specified process when the defined special keyboard combination is pressed. |

The following is an example of the /etc/inittab file with explanations.

```
#
id:3:inittab:


```

Tells the system the default runlevel to start up in. As you can see, this system is probably a Red Hat system booting up in to multiuser text mode.