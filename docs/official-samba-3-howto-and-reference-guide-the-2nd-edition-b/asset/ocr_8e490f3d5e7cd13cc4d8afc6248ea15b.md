The following **/etc/nsswitch.conf** file contents are required:

```
...` `passwd: files ldap ` `shadow: files ldap ` `group: files ldap ` `...` `hosts: files wins ` `...`
```

The **/etc/ldap.conf** file must be configured also. Refer to the PADL documentation and source code for nss-ldap to specific instructions. ` `The next step involves preparation of the ADS schema. This is briefly discussed in the remaining part of this chapter.

# ### 13.2.4.1 IDMAP, Active Directory, and MS Services for UNIX 3.5

The Microsoft Windows Service for UNIX (SFU) version 3.5 is available for free download^[3] from the Microsoft Web site. You will need to download this tool and install it following Microsoft instructions.

# ### 13.2.4.2 IDMAP, Active Directory and AD4UNIX

Instructions for obtaining and installing the AD4UNIX tool set can be found from the Geekcomix^[4] Web site.

> [^3]: <http://www.microsoft.com/windows/sfu/> ` `[^4]: <http://www.geekcomix.com/cgi-bin/classnotes/wiki.pl?LDAP01/An_Alternative_Approach>