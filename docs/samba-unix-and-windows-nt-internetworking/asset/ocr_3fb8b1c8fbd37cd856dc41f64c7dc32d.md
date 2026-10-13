in the `/usr/local/samba/private` directory as a file named `<Domain Name>.<Samba Name>.mac`. The `mac` file name extension stands for *machine account*.

![](bbox=[0.18, 0.23, 0.6, 0.48])

Figure 10.1: Server Manager

# Example 10.1 Creating a Domain Server Password

```
$ smbpasswd -j <Domain Name> -r <PDC Name>.
```

Now it's time to start the `smbd` and `nmbd` daemons on the server. Samba should log-on to the domain during initialization. You can verify active membership using Server Manager (Figure 10.2).

# Domain Control

Although Samba's domain controller functionality is not quite on a par with Windows NT yet, you may still want to consider running Samba as a domain controller for your Windows 9x clients. One reason is that by using Samba as the domain's authentication service, you can collocate UNIX and NetBIOS namespace administration on the same Windows 9x platform. It may also be that your in-house system administration skills and platform support infrastructure favor running a domain controller under UNIX rather than Windows NT. Whatever the reason, you'll find that Samba will perform adequately as a domain controller in the Windows 9x context. Domain control for Windows NT clients entails additional undocumented protocol support and still lies in the realm of the experimental Samba PDC effort.

To enlist Samba as the domain controller for your Windows 9x domain you'll need to verify that WINS service has been configured and is available (see Chapter 8). You can run WINS under Samba by enabling the `wins support` parameter. If WINS services are provided by another machine, identify the remote server's IP address or DNS name using the `wins server` parameter. Remember that `wins support` and `wins server` are mutually exclusive.

```
wins support = yes
```

or