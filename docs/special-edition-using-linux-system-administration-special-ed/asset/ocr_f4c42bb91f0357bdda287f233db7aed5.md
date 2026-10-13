# SAMPLE ftpwho OUTPUT

The following illustrates typical output of the `ftpwho` utility:

```
```text
# ftpwho
Service class all:
    ?       S       0:05
ftpd: localhost: anonymous/user@some.host: IDLE    -   1 users (50 maximum)
```
```

# SAMPLE ftpcount OUTPUT

The following illustrates typical output of the `ftpcount` utility:

```
```text
# ftpcount
Service class all                  -   1 users (50 maximum)
```
```

# USING ftpshut

The `ftpshut` utility allows you to schedule a shutdown of the FTP server. In its most basic form, the `ftpshut` command needs to be provided with a time for the shutdown:

```
```text
# ftpshut time
```
```

The *time* can be specified as a specific time in the form *HHMM* (in other words 1430 for 2:30 p.m.), as an offset of minutes in the form *+minutes* (in other words, to shutdown the server in 30 minutes, use +30), or immediately using now.

Ten minutes prior to the scheduled shutdown, the FTP server will stop accepting new connections. If the scheduled shutdown time is fewer than 10 minutes away then new logins will immediately be prevented. This 10-minute threshold can be altered with the -l argument to the `ftpshut` command. For instance, to shut down WU-FTPD in 30 minutes and start preventing logins 20 minutes prior to the shutdown, use the following command:

```
```text
# ftpshut -l 20 +30
```
```

Five minutes prior to the scheduled shutdown, the FTP server will terminate all existing connections. If the scheduled shutdown time is fewer than 5 minutes away then all connections will immediately be terminated. This 5-minute threshold can be altered with the -d argument to the `ftpshut` command. For instance, to shut down WU-FTPD at 2:30 p.m. and disconnect existing logins 10 minutes prior to the shutdown, use the following command:

```
```text
# ftpshut -d 10 1430
```
```

Optionally, you can warn users of the imminent shutdown of the server by providing a warning message as the last argument to the `ftpshut` command. The message should be a string of text enclosed in double quotation marks. Several special symbols can be used in your message text to force the inclusion of dynamic information. These symbols are outlined in Table 27.3.