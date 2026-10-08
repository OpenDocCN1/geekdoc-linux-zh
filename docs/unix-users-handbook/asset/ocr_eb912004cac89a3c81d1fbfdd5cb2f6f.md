```
# /opt/asu/lanman/bin/net share

Sharename   Resource                                  Remark
------------------------------------------------------------------------
ADMIN$    C:\OPT\ASU\LANMAN                    Admin Share
IPCS      C:\                                IPC Share
C$
D$        C:\                                Root Share
D$        C:\VAR\OPT\ASU\LANMAN\SHARES       SystemRoot Share
ASTOOLS   C:\VAR\OPT\ASU\LANMAN\SHARES...    Advanced Server Tools
DOSUTIL   C:\VAR\OPT\ASU\LANMAN\SHARES...    DOS Utilities
NETLOGON  C:\VAR\OPT\ASU\LANMAN\SHARES...    Logon Scripts Directory
PATCHES   C:\VAR\OPT\ASU\LANMAN\SHARES...    Client Patches
PRINTLOG  C:\VAR\OPT\ASU\LANMAN\SHARES...    LP printer messages
USERS     C:\HOME\LANMAN                     Users Directory
LASER     laser                               Spooled
The command completed successfully.
#
```

The shares shown include the printer that was added. We could now issue the net share command and add a UNIX file system to be shared. To share the /home directory on the UNIX system *dloaner*, we would issue the following command:

```
# /opt/asu/lanman/bin/net share home=c:\home
home was shared successfully
```

Note that the UNIX notation for the directory was issued with the slash (/) rather than the backslash (\), as you would on a Windows system. We can now view the shares on *dloaner*, including the new *HOME* share, with the net command:

```
# /opt/asu/lanman/bin/net share

Sharename   Resource                                  Remark
------------------------------------------------------------------------
ADMIN$    C:\OPT\ASU\LANMAN                    Admin Share
IPCS      C:\                                IPC Share
C$
D$        C:\                                Root Share
D$        C:\VAR\OPT\ASU\LANMAN\SHARES       SystemRoot Share
ASTOOLS   C:\VAR\OPT\ASU\LANMAN\SHARES...    Advanced Server Tools
DOSUTIL   C:\VAR\OPT\ASU\LANMAN\SHARES...    DOS Utilities
HOME      C:\HOME                              Logon Scripts Directory
NETLOGON  C:\VAR\OPT\ASU\LANMAN\SHARES...    Client Patches
PATCHES   C:\VAR\OPT\ASU\LANMAN\SHARES...    LP printer messages
PRINTLOG  C:\VAR\OPT\ASU\LANMAN\SHARES...    Users Directory
USERS     C:\HOME\LANMAN                     Spooled
LASER     laser
The command completed successfully.
#
```