![](bbox=[0.12, 0.096, 0.219, 0.158])

When you need to recover a system that has stopped responding, after the stop+a sequence, be sure to enter the OpenBoot **sync** command to synchronize the system disks and write a crash dump before issuing the appropriate boot command.

| Sequence | System Response |
|---|---|
| stop | Bypasses the POST |
| stop+a | Aborts the operating system or boot process (returns to the OpenBoot **ok** prompt) |
| stop+d | Enters diagnostic mode |
| stop+f | Enters the Forth Monitor on TTYA (instead of the system console) |
| stop+n | Resets the NVRAM contents to default values |

You can use the **kbd(1)** command to enable or disable the stop+a sequence. You can also set the keyboard characteristics by modifying the /etc/default/kbd file and then executing the **kbd -i** command. For example, the following **kbd** command disables the keyboard abort sequence:

```
```sh
# kbd -a disable
```
```

To accomplish the same task, place the _KEYBOARD_ABORT=disable_ entry in /etc/default/kbd and execute the following:

```
```sh
# kbd -i
```
```

# The Boot Process

The boot PROM stores firmware that is responsible for booting the operating system. Because the SPARC boot process is somewhat different from the Intel x86 boot process, they are covered separately here.

# The SPARC Boot Process

The SPARC boot process consists of the following phases:

+   1. **Boot PROM**—This phase displays system information and then runs the POST diagnostics. After the diagnostics are complete, the primary boot program, bootblk, is loaded. Its function is to locate the secondary boot program, ufsboot, on the boot device.