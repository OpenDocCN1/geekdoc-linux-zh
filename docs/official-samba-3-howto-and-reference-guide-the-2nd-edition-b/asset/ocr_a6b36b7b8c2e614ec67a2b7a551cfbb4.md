# Example 2.3.6 Member Server smb.conf (Shares and Services)

```
[homes]
comment = Home Directories
valid users = %S
read only = No
browseable = No

[spyfull]
comment = Accounting Application Only
path = /export/spyfull
valid users = @Accounts
admin users = maryo
read only = Yes

[public]
comment = Data
path = /export/public
read only = No

[printers]
comment = All Printers
path = /var/spool/samba
printer admin = root, maryo
create mask = 0600
guest ok = Yes
printable = Yes
use client driver = Yes
browseable = No
```

+   3. Join the domain. Note: Do not start Samba until this step has been completed!

```
root# net rpc join -Uroot%'bigsecret'
Joined domain MIDEARTH.
```

+   4. Make absolutely certain that you disable (shut down) the `nscd` daemon on any system on which `winbind` is configured to run.

+   5. Start Samba following the normal method for your operating system platform. If you wish to do this manually, execute as root:

```
root# nmbd; smbd; winbind;
```

+   6. Configure the name service switch (NSS) control file on your system to resolve user and group names via winbind. Edit the following lines in `/etc/nsswitch.conf`:

```
passwd: files winbind
group: files winbind
```