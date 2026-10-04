The information reported is described in Table 12-7.

# Table 12-7 Port Monitor Information

| Service | Description |
|---|---|
| mbmon | The port monitor name, mbmon. |
| ttymon | The port monitor type, ttymon. |
| a | The service tag value. |
| - | Flags following are set by using the pmadm -f command. |
| root | The ID assigned to the service when it's started. |
| <PMSPECIFIC> Information: |  |
| /dev/term/a | The TTY port pathname. |
| /usr/bin/login | The full pathname of the service to be invoked when a connection is received. |
| contty | The TTY label in the /etc/ttydefs file. |
| ldterm,ttcompat | The streams modules to be pushed. |
| login: Terminal disabled | An inactive message to be displayed when the port is disabled. |
| y | The software carrier value; n indicates software carrier off, y indicates software carrier on. Software carrier is turned on in this example. |
| # | Any comment. There is no comment in this example. |

To disable a port monitor service, type

```
pmadm -d -p mbmon -s a
```

To enable a disabled port monitor service, type

```
pmadm -e -p mbmon -s a
```

# ttyadm

The ttyadm command is an administrative command that formats ttymon information and writes it to standard output. ttyadm provides a means of presenting formatted port monitor-specific (ttymon-specific) data to the sacadm and pmadm commands, which are described next in this chapter. ttyadm is used, for example, to inform users that a port is disabled. Do so by typing

```
ttyadmin -i
```