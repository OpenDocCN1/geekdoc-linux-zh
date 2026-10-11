This displays your network connections through a network port. You'll probably want to display it. If your host is a prime victim, the other machines that connect to it could be likely springboards to get to your host.

```
NFS Cache [Low Risk]: 0
Sysstat [Low Risk]: 1
```

This displays your host information remotely. Disable the port.

```
Bootparam [Low Risk]: 0
BootparamDom [Low Risk]: 0
Finger [Low Risk]: 0
Rusers Output [Low Risk]: 0
Finger Output [Low Risk]: 0
SNMP Public Information [Low Risk]: 0
Old Sendmail Version [Low Risk]: 0
Verify Account Information About Users with Sendmail [Low Risk]: 1
Expand Account Information About Users with Sendmail [Low Risk]: 1
```

User accounts can be verified and information obtained through sendmail. You may want to disable the VRFY command in sendmail.

```
NNT Daemon [Low Risk]: 0
Trace Routing of Packets [Low Risk]: 1
```

You can see how packets go from the origin, being your host, to the destination host. This provides a hacker with routing and hop information about your host.

```
Open/Close Connection Flood [Low Risk]: 0
Old INND Version [Low Risk]: 0
Kerberos User List Vulnerable [Low Risk]: 0
Kerberos Brute Force Vulnerable [Low Risk]: 0
RWH0 Daemon Overflow [Low Risk]: 0
SMTP Timer Abort: 0
Netbios Tests Disabled: 0
Unable to Bind to Ident: 0
Unable to Listen on Ident: 0
Additional Module Output: 0

--------- End of Report ---------
```