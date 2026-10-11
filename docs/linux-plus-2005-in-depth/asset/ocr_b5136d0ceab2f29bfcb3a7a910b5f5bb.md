The **facility** is the area of the system to listen to, whereas the **priority** refers to the importance of the information. For example, a facility of kernel and priority of warning indicates that the System Log Daemon should listen for kernel messages of priority warning and more serious. When found, the System Log Daemon places these messages in the `/var/log/logfile` file. The aforementioned entry would read:

```
```
kern.warning    /var/log/logfile
```
```

> **NOTE**
> 
> You can also send information to the syslog daemon on a remote Linux or UNIX server; simply specify the notation @servername in place of /var/log/logfile.

To only log warning messages from the kernel to /var/log/logfile, you can use the following entry instead:

```
```
kern.-warning    /var/log/logfile
```
```

Alternatively, you can log all error messages from the kernel to /var/log/logfile by using the * wildcard, as shown in the following entry:

```
```
kern.*    /var/log/logfile
```
```

In addition, you can specify multiple facilities and priorities; to log all error messages except warnings from the kernel to /var/log/logfile, you can use the following entry:

```
```
kern.*;kern.l-warn    /var/log/logfile
```
```

To log all error messages from the kernel and news daemons, you can use the following entry:

```
```
kern.news.*    /var/log/logfile
```
```

To log all warnings from all facilities except for the kernel, you can use the “none” keyword, as shown in following entry:

```
```
*.warn;kern.none    /var/log/logfile
```
```

Table 11-4 describes the different facilities available and their descriptions.

**Table 11-4 Facilities used by the System Log Daemon**

| **Facility** | **Description** |
| :--- | :--- |
| auth, or, security | Specifies messages from the login system, such as the login program, the getty program, and the su command |
| authpriv | Specifies messages from the login system when authenticating users across the network or to system databases |
| cron | Specifies messages from the cron and at daemons |