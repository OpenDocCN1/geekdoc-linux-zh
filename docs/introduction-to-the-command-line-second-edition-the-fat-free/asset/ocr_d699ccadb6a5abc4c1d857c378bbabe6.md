# reboot

Purpose: Reboot the system.

Usage syntax: reboot

```
# reboot
BROADCAST MESSAGE FROM ROOT: The system is going down for reboot now!
* Stopping services                   [ OK ]
* Terminating processes                [ OK ]
...
The system will now reboot.
```

Example output of the reboot command

The **reboot** command is used to gracefully reboot the system. It is essentially a shortcut for **shutdown -r now**. Executing **reboot** on the command line will immediately reboot the system as demonstrated in the above example.

> **Warning**
> 
> The reboot command does not offer a grace period and will immediately reboot the system when executed.

Common usage examples:

**reboot** | Gracefully reboot the system