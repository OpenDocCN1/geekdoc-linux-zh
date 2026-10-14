> > **Tip**
> >
> > For simple administration tasks with the Samba server, there is also the program swat. It provides a simple web interface with which you can conveniently configure the Samba server. In a web browser, call up `http://localhost:901` and log in as user root. swat is also activated in the files `/etc/inetd.conf` and `/etc/services`. More information about swat can be found in its man page.

# Samba as Login Server

In networks where predominantly Windows clients are found, it is often preferable that users may only register with a valid account and password. This can be brought about with the help of a Samba server. In a pure Windows network, a Windows NT server takes on this task. This is configured as a Primary Domain Controller (PDC). The following entries must be made in the [global] section of the smb.conf.

```
```text
global]
workgroup = TUI-NET
domain logons = yes
domain master = yes
```
```

*File 61: []*

If encrypted passwords are used for verification purposes, the Samba server must be able to handle these. The entry encrypt passwords = yes in the [global] section enable this functionality. In addition, it is necessary to prepare user accounts and passwords in an encryption format that conforms with Windows. This is done with the command smbpasswd -a name. Since, in accordance with the Windows NT domain concept, the computers themselves need a domain account, this is created with the following commands:

```
```text
useradd -m machinename
smbpasswd -a -m machinename
```
```

*File 62: Adding a Machine Account*

With the useradd command, a masked dollar sign, masked by a backslash, is added. The command smbpasswd includes this automatically when the -m parameter is used.