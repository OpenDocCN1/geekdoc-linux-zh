```
multicast: add net ff00::/8: gateway fe80::a0 0:20ff:fea2:6382
starting rpc services: rpcbind done.
Setting default IPv4 interface for multicast: add net 224.0/4: gateway unknown
syslog service starting.
syslogd: line 24: WARNING:loghost could not be resolved
Print services started.
volume management starting.
Mar 23 13:19:33 unknown snmpdx:
The system is ready.
ultra console login:
```

The startup process is controlled by a number of configuration variables. The ones that affect the startup process are described in Table 2.17.

# TABLE 2.17

# Boot Configuration Variables

| Variable | Description |
|---|---|
| auto-boot? | Controls whether the system automatically starts up after a system reset or when the power is turned on. The default for this variable is true. When the system is powered on, the system automatically starts up to the default run level. |
| boot-command | Specifies the command to be executed when auto-boot? is true. The default value of boot-command is boot with no command-line arguments. |
| diag-switch? | If the value is true, runs in the diagnostic mode. This variable is false by default. |
| boot-device | Contains the name of the default startup device that is used when OpenBoot is not in diagnostic mode. |
| boot-file | Contains the default startup arguments that are used when OpenBoot is not in diagnostic mode. The default is no arguments. (See Table 2.18 for details of when this variable is used.) |
| diag-device | Contains the name of the default diagnostic mode startup device. The default is net. (See Table 2.18 for details of when this variable is used.) |

continues