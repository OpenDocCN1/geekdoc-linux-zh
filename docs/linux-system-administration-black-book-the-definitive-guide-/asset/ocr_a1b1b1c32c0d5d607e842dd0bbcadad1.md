6. In this case, you are not printing to a local device. Therefore, your device assignment line is as follows:

```
:lp=\
```

7. The printer may not be on this machine, but you still need to tell /etc/printcap where to spool files that are waiting for printing. Typically, you would use a location that is available to both this machine and the remote one. Perhaps an NFS share mounted at /shares/print, using a line such as this:

```
:sd=/shares/print/otter:\
```

8. For a printer that is not on this machine, you need to use some additional /etc/printcap setting options. The first of these options defines which machine the printer is connected to. You set this line in the format *rm=host*:\ For example:

```
:rm=otter:\
```

9. Next, you need to specify to which local printer on the remote host the print jobs for this definition go. Here, you use the local name for the remote printer, as follows: *rp=localname*:\ For example, if this printer is lp on otter and this is the last line in the print definition, you would use:

```
:rp=lp
```

10. Any print filtering is done at the remote end. Press the Esc key and then type “ZZ” to save and exit this file.

| Related solution: | Found on page: |
| Mounting Remote File Systems With NFS | 505 |

# Setting Up Popular Print Filters

Two popular print filters available on the Internet are **apsfilter** and **magicfilter**. To utilize these items, do the following:

+   1. Download one or the other of the two scripts from http://metalab.unc.edu/pub/Linux/system/printing/.