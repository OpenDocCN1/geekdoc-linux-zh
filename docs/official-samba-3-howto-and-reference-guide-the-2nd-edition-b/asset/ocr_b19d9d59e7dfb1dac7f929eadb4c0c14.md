# 4.7.2 Joining Domain Fails Because of Existing Machine Account

“I get told, ‘You already have a connection to the Domain...’ or ‘Cannot join domain, the credentials supplied conflict with an existing set...’ when creating a Machine Trust Account.”

This happens if you try to create a Machine Trust Account from the machine itself and already have a connection (e.g., mapped drive) to a share (or IPChS) on the Samba PDC. The following command will remove all network drive connections:

```
C:\> net use * /d
```

This will break all network connections.

Further, if the machine is already a “member of a workgroup” that is the same name as the domain you are joining (bad idea), you will get this message. Change the workgroup name to something else — it does not matter what — reboot, and try again.

# 4.7.3 The System Cannot Log You On (C00019B)

“I joined the domain successfully but after upgrading to a newer version of the Samba code I get the message, ‘The system cannot log you on (C00019B). Please try again or consult your system administrator when attempting to logon.’”

This occurs when the domain SID stored in the secrets.tdb database is changed. The most common cause of a change in domain SID is when the domain name and/or the server name (NetBIOS name) is changed. The only way to correct the problem is to restore the original domain SID or remove the domain client from the domain and rejoin. The domain SID may be reset using either the net or rpcclient utilities.

To reset or change the domain SID you can use the net command as follows:

```
root# net getlocalsid 'OLDNAME'
root# net setlocalsid 'SID'
```

Workstation Machine Trust Accounts work only with the domain (or network) SID. If this SID changes, domain members (workstations) will not be able to log onto the domain. The original domain SID can be recovered from the secrets.tdb file. The alternative is to visit each workstation to rejoin it to the domain.

# 4.7.4 The Machine Trust Account Is Not Accessible

“When I try to join the domain I get the message, ‘The machine account for this computer either does not exist or is not accessible.’ What’s wrong?”