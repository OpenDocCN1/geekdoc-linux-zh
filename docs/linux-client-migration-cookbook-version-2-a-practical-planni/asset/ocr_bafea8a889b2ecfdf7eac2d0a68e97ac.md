**Important:** Make sure to use the right version of Kerberos (either MIT or Heimdal). For AD on Windows Server® 2003, Heimdal should be at least Version 0.6 and MIT at least Version 1.3.1. Also check to see if the kinit and klist commands actually come from the correct implementation and not from Java. The Java kinit is known not to work.

When using Novell Linux Desktop, the heimdal and heimdal-linux-tools packages might not be installed by default. These are needed to connect to AD on Windows 2003 Server.

**Important:** Make sure clients and the Active Directory (or Kerberos) server have the same time within a defined allowed skew.

Microsoft Windows servers use Simple Network Time Protocol (SNTP), which is a simplified version of the (UNIX/Linux) Network Time Protocol (NTP). The packets and formats are identical and thus can be used together. This means that the Linux clients can be synchronized with the AD servers using ntp.

You can test the Kerberos configuration by doing a `kinit USERNAME@REALM` to make sure the password is accepted by the Windows 200x KDC.

**Important:** Only newly created accounts in ADS or accounts that have had their passwords changed once since migration work. If an account stems from before the migration (or installation in the case of Administrator), the **kinit** command returns a message about a wrong encryption. Changing the password of the account resolves this problem.

To actually join the AD domain, you execute the following:

```
net ads join -U administrator
```

This prompts for the administrator password, for example, joining client1 to the domain AD6380 using administrative user idsadmin (see Example 9-4).

*Example 9-4* Example of joining client1 to domain AD6380

```
[root@client1]# net ads join -U idsadmin
idsadmin password:*******
Using short domain name -- AD6380
Joined 'CLIENT1' to realm 'AD6380.LOCAL'
```