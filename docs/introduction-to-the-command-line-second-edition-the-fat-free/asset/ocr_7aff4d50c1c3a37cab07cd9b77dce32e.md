# # poweroff

Purpose: Power off the system.

Usage syntax: poweroff

```
# poweroff

BROADCAST MESSAGE FROM ROOT:
The system is going down for power off now!

* Stopping services [ OK ]

* Terminating processes [ OK ]

...

The system will now power off.
```

The poweroff command will immediately shutdown and power off the system. It is essentially a shortcut for shutdown -P now. The poweroff command is found on all Linux distributions and some BSD and Unix systems.

> **Note** To see if the poweroff command is supported on your system, type whereis poweroff.

> **Warning** The poweroff command does not offer a grace period and will immediately bring down the system when executed.

Common usage examples:

```
poweroff | Shutdown and poweroff the system
```