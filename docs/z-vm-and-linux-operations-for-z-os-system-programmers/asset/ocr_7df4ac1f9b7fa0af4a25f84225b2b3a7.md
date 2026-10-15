# CP QUERY MAXUSERS

Use this command to display the maximum number of logged-on users allowed. If users cannot log on, this might be a good command to execute.

> z/OS analogy: To display the number of maximum users in a z/OS environment, browse the member IEASYSSxx of your SYS1.PARMLIB concatenation.

# CP QUERY MDC

Use this command from a class B user to query minidisk cache (MDC) settings for the entire system, for a real device, an active minidisk, or a minidisk defined in the directory. See Example 7-11. This command is useful for investigating I/O problems.

# Example 7-11 Query MDC command

```
q mdc
Minidisk cache ON for system
Storage MDC min=0M max=128M, usage=3%, bias=1.00
Xstore MDC min=0M max=0M, usage=0%, bias=1.00
Ready; T=0.01/0.01 10:23:24
```

# CP QUERY NAMES

Use this command to display:
• A list of all logged-on users
• The real or logical device number of the display that each user is connected
See Example 7-12.

# Example 7-12 Query Names command

```
q n
LNXCER - DSC , LNXGUI - DSC , LNXXEN - DSC , COSTA -L0004
FTPSERVE - DSC , TCPIP - DSC , DTCVSM2 - DSC , DTCVSW1 - DSC
VMSERVR - DSC , VMSERVU - DSC , VMSERVS - DSC , OPERSYMP - DSC
DISKACNT - DSC , EREP - DSC , OPERATOR - DSC , MAINT -L0003
VSM - DSC , TCPIP
Ready; T=0.01/0.01 10:26:04
```

> z/OS analogy: On z/OS systems, you can display similar information by running the SDSF Display Active command.