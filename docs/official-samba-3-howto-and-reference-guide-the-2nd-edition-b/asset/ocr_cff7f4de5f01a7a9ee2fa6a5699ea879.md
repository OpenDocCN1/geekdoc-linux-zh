KDC (i.e., the hostname with no domain attached) or it can be the NetBIOS name followed by the realm.

The easiest way to ensure you get this right is to add a /etc/hosts entry mapping the IP address of your KDC to its NetBIOS name. If you do not get this correct, then you will get a local error when you try to join the realm.

If all you want is Kerberos support in smbclient, then you can skip directly to Section 6.4.5 now. Section 6.4.3 and Section 6.4.4 are needed only if you want Kerberos support for smbd and winbindd.

# ## 6.4.3 Create the Computer Account

As a user who has write permission on the Samba private directory (usually root), run:

```
`root# net ads join -U Administrator%password`
```

The Administrator account can be any account that has been designated in the ADS domain security settings with permission to add machines to the ADS domain. It is, of course, a good idea to use an account other than Administrator. On the UNIX/Linux system, this command must be executed by an account that has UID=0 (root).

When making a Windows client a member of an ADS domain within a complex organization, you may want to create the machine trust account within a particular organizational unit. Samba-3 permits this to be done using the following syntax:

```
`root# kinit Administrator@your.kerberos.REALM`
`root# net ads join "organizational_unit"`
```

Your ADS manager will be able to advise what should be specified for the “organizational_unit” parameter.

For example, you may want to create the machine trust account in a container called “Servers” under the organizational directory “Computers\BusinessUnit\Department.” like this:

```
`root# net ads join "Computers\BusinessUnit\Department\Servers"`
```

This command will place the Samba server machine trust account in the container Computers\BusinessUnit\Department\Servers. The container should exist in the ADS directory before executing this command.