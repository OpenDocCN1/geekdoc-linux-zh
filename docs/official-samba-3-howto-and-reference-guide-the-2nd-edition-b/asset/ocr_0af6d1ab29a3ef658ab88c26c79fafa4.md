```
root# smbpasswd -a jackb
New SMB password: m0r3p4in
Retype new SMB password: m0r3p4in
Added user jackb.

root# smbpasswd -a maryo
New SMB password: secret
Reenter smb password: secret
Added user maryo.

root# smbpasswd -a ameds
New SMB password: mysecret
Reenter smb password: mysecret
Added user ameds.
```

+   4. Install printer using the CUPS Web interface. Make certain that all printers that will be shared with Microsoft Windows clients are installed as raw printing devices.

+   5. Start Samba using the operating system administrative interface. Alternately, this can be done manually by executing:

```
root#  nmbd; smbd;
```

Both applications automatically execute as daemons. Those who are paranoid about maintaining control can add the -D flag to coerce them to start up in daemon mode.

+   6. Configure the /export directory:

```
root#  mkdir /export
root#  chown maryo.users /export
root#  chmod u=rwx,g=rwx,o=rwx /export
```

+   7. Check that Samba is running correctly:

```
root#  smbclient -L localhost -U%
Domain=[MIDEARTH]  OS=[UNIX]  Server=[Samba-3.0.20]
```

| Sharename | Type | Comment |
| :---------- | :---- | :------ |
| public | Disk | Data |
| IPC$ | IPC | IPC Service (Samba-3.0.20) |
| ADMIN$ | IPC | IPC Service (Samba-3.0.20) |
| hplj4 | Printer | hplj4 |

Server | Comment