| Command | Description |
|---|---|
| lpq command | Query print queue.
User %p (printer). |
| lpq cache time | How long lpq info is cached; limits server load from repeated query requests from Windows clients. Default is 10 seconds. The Windows spool manager on each client will query a remote print queue every 15 seconds. The cache files are stored in /tmp/lpq.xxxx where xxxx is a hash of the lpq command in use. |
| lprm command | Remove a print job from a queue.
Use %p (printer) and %j (job #). |
| lppause command | Pause a specific print job.
Use %p (printer) and %j (job #). |
| lpresume command | Resume a specific print job.
Use %p (printer) and %j (job #). |
| postscript | Force printing in postscript mode; fixes leading ctl-d problem by adding a %! sequence to the beginning of the file before sending it to the printer. |
| queuepause command | Pause a specific print queue.
Use %p (printer). |
| queueresume command | Resume a specific print queue.
Use %p (printer) |

# Print Command

In particular, you'll want to verify the options specified by the print command parameter. The value of print command is a text string that will be invoked via a system() call to process a print file after the file has been written to the spool directory. In general, this will result in the file's being handed off to the printing subsystem. The print command must remove the print file from the spool directory when processing has been completed. Example 12.2 displays print command defaults for the supported operating system types.

# Example 12.2 Default Print Command Values

```
print command = lpr -r -P%p %s    AIX, BSD, LPRNG, PLP, QNX
print command = lp -c -d%p %s; rm %s    HPUX, SYSV
print command = lp -d%p -s %s; rm %s    SOFTQ
```

Note that the specified command must indicate the spool file name and, optionally, the printer name (Table 12.2). In addition, if guest ok is specified for the printer, some systems experience print failures if the guest account value is nobody. In this event, use an alternate UNIX account in the guest account parameter.

# Command Parameter Scripts

The print command parameters listed in Table 12.1 designate a text string that