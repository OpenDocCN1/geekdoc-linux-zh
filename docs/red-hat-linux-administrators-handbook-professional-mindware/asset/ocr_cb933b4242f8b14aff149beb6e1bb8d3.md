If you want the printer list to appear in the browser list, set the `browseable` parameter to `yes` in the preceding configuration. Similarly, if you want to allow the `guest` account to use the printer, set `guest ok` to `yes` in the `[printers]` configuration.

That’s all that is required to set up all of your printers. However, if you prefer to make one or more printers privately available to one or more users, you can specify a separate section for each of these users. For example, if I want to create private printer (fancyjet) access for a user called bigboss, I can create a configuration such as the following:

```
[fancyjet]  
comment = Big Boss Only Printer  
valid users = bigboss  
path = /home/bigboss/fancyjet  
guest ok = no  
browseable = no  
writable = no  
printable = yes
```

The `valid users` parameter enables you to specify a space-separated list of users who have access to the printer.

After you modify and test the `/etc/samba/smb.conf` file, restart the Samba service, and you should be able to access the Linux printers from your Windows computers.

# Using an interactive Samba client

smbclient also enables you to access a Samba resource interactively. For example, if you want to access a disk share on a Windows system from your Linux system, use smbclient as follows:

```
smbclient //WINDOWS-SERVER/resource -U username -P password
```

In the following example, `smbclient` is used to access the C:\ drive on PLUTO as user kabir:

```
smbclient //PLUTO/c -U kabir -P foobar
```