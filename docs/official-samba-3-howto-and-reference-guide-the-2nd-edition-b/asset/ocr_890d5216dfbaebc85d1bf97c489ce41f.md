“NT.STATUS-LOGON_FAILURE.” There is no current workaround to re-establish the Samba-2.2 behavior.

+   2. When adding machines to a Samba-2.2 controlled domain, the “add user script” was used to create the UNIX identity of the machine trust account. Samba-3 introduces a new “add machine script” that must be specified for this purpose. Samba-3 will not fall back to using the “add user script” in the absence of an “add machine script”.

# ### 34.4.3 Passdb Backends and Authentication

There have been a few new changes that Samba administrators should be aware of when moving to Samba-3.

+   1. Encrypted passwords have been enabled by default in order to interoperate better with out-of-the-box Windows client installations. This does mean that either (a) a Samba account must be created for each user, or (b) “encrypt passwords = no” must be explicitly defined in *smb.conf*.

+   2. Inclusion of new *security = ads* option for integration with an Active Directory domain using the native Windows Kerberos 5 and LDAP protocols.

Samba-3 also includes the possibility of setting up chains of authentication methods (*auth methods*) and account storage backends (*passdb backend*). Please refer to the *smb.conf* man page and Chapter 10, “Account Information Databases”, for details. While both parameters assume sane default values, it is likely that you will need to understand what the values actually mean in order to ensure Samba operates correctly.

Certain functions of the **smbpasswd** tool have been split between the new **smbpasswd** utility, the **net** tool, and the new **pdbedit** utility. See the respective man pages for details.

# ### 34.4.4 LDAP

This section outlines the new features effecting Samba/LDAP integration.

# #### 34.4.4.1 New Schema

A new object class (*sambaSamAccount*) has been introduced to replace the old *sambaAccount*. This change aids in the renaming of attributes to prevent clashes with attributes from other vendors. There is a conversion script (examples/LDAP/convertSambaAccount) to modify an LDIF file to the new schema.

Example:

```
```
$ ldapsearch .... -LLL -b "ou=people,dc=..." > old.ldif
$ convertSambaAccount --sid <DOM SID> --input old.ldif --output new.ldif
```
```

The <*DOM SID*> can be obtained by running