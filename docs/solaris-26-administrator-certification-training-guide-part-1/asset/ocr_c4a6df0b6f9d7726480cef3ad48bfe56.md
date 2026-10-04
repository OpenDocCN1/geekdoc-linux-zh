In particular, SAF enables you to

+   - Set up ttymon and listen port monitors (using the sacadm command)
- Set up ttymon port monitor services (using the pmadm and ttyadm commands)
- Set up listen port monitor services (using the pmadm and nisadmin commands)
- Troubleshoot tty devices
- Troubleshoot incoming network requests for printing service
- Troubleshoot the Service Access Controller (using the sacadm command)

The configuration files associated with SAF are described in Table 12-4.

# Table 12-4 Files Associated with SAF

| File | Description |
|---|---|
| /etc/saf/_sysconfig | Per system configuration script |
| /etc/saf/_sactab | SAC's administrative file; contains configuration data for the port monitors that the SAC controls |
| /etc/saf/pmtag | Home directory for port monitor pmtag |
| /etc/saf/pmtag/_config | Per-port monitor configuration script for port monitor pmtag if it exists |
| /etc/saf/pmtag/_pmtab | Port monitor pmtag's administrative file; contains port monitor-specific configuration data for the services pmtag provides |
| /etc/saf/pmtag/svctag | Per-service configuration script for service svctag |
| /var/saf/log | SAC's log file |
| /var/saf/pmtag | Directory for files created by pmtag, such as log files |

# sacadm

Use the sacadm command to add, list, remove, kill, start, enable, or disable a ttymon or listen port monitor. You must be logged in as superuser to use this command. For example, the command syntax used to add a ttymon port monitor is

```
sacadm -a -p mbmon -t ttymon -c /usr/lib/saf/ttymon -v 'ttyadm -V' -y "TTY Ports a & b"
```

Notice the use of the ttyadm command.

To view the newly added port monitor, type:

```
sacadm -l -p mbmon
```