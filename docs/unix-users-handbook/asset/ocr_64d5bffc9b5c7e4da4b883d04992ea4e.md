# NET STATISTICS

**NET STATISTICS** - Use this command to display the statistics log for a service. Issue NET STATISTICS without options to display statistics for all services.

The following is a summary of the **NET STATISTICS** command:

```
C:\ NET STATISTICS /?
NET STATISTICS [WORKSTATION | SERVER]
```

Some commonly used options follow:

SERVER  Displays server service statistics.
WORKSTATION  Displays workstation service statistics.

The following example shows issuing the **NET STATISTICS** command with no options:

```
C:\ NET STATISTICS
Server Statistics for \NISDEV

Statistics since 1/21/98 8:49 AM

Sessions accepted                    3
Sessions timed-out                   32
Sessions errored-out                 32

Kilobytes sent                       165941
Kilobytes received                   33118

Mean response time (msec)            0

System errors                        0
Permission violations                2
Password violations                  0

Files accessed                       12787
Communication devices accessed       0
```