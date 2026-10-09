Here, I build an nsmb.conf allowing Bert access to his files on the corporate CIFS fileserver.

```
[default]
    nbns = 203.0.113.12
    workgroup = BigCorp
[FILESERVER:bert,jw]
    password = $$1624a53302a6d
```

With this configuration, Bert should be able to access whatever CIFS shares those tyrannical Windows admins permit.

# ## CIFS Name Resolution

Before FreeBSD can mount a CIFS share, it needs to identify the host the share is on. While Microsoft has used DNS for decades now, typical Windows environments often support a whole panoply of legacy protocols. Verify that smbutil(1) can find CIFS servers with smbutil lookup.

```
# smbutil lookup fileserver1
Got response from 203.0.113.12
IP address of ntserv1: 203.0.113.4
```

If this works, you have basic CIFS functionality.

# ## Other smbutil(1) Functions

You can view shares on a host at the command line. Start by logging into your host.

```
# smbutil login //unix@fileserver1
Password:
```

So, our configuration is correct. Let's see what resources this server offers with smbutil's view command.

```
# smbutil view //unix@fileserver1
Password:
Share     Type    Comment
--------------
IPC$      pipe    Remote IPC
```