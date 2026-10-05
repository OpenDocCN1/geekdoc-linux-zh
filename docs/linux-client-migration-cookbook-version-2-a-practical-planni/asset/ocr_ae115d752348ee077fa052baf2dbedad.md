+   The password for the bind user (in plain text, so you secure the configuration file)

+   Scope to search

+   SSL enablement

+   A number of entries to map domain schema objects to objects needed by the NSS

An example configuration file for /etc/ldap.conf is shown in Example 9-10.

# Example 9-10 Partial /etc/ldap.conf file

```
host 192.168.100.110
base cn=Users,dc=AD6380,dc=LOCAL
binddn cn=ldapbind,cn=Users,dc=AD6380,dc=LOCAL
bindwp Webcome2006
scope up
sl no
nss_map_base_passwd cn=Users,dc=AD6380,dc=LOCAL?sub
nss_map_shadow cn=Users,dc=AD6380,dc=LOCAL?sub
nss_map_base_group cn=Users,dc=AD6380,dc=LOCAL?sub
nss_map_objectclass shadow posixAccount user
nss_map_objectclass uid SAMAccount user
nss_map_attribute uid SAMAccountName
nss_map_attribute udnNumber mSFU30UidNumber
nss_map_attribute gidNumber mSFU30GidNumber
nss_map_attribute loginShell mSFU30LoginShell
nss_map_attribute geos name
nss_map_attribute userpassword mSFU30Password
nss_map_attribute homedirectory mSFU30HomeDirectory
nss_map_objectclass posixGroupGroup
ss_map_attribute uniqueMember mSFU30PosixMember
nss_map_attribute cn cn
```

The following entries are changed in the NSS configuration to enable the domain users through LDAP:

```
passwd: files ldap
group: files ldap
```

To test this, use the command:

```
getent passwd
```

This should now show the testuser entry in the passwd output. This is shown in Example 9-11 on page 207.