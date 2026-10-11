# Table 6-4

| Section | Entry Name | Description |
| :--- | :--- | :--- |
| | ldap port = | Specifies the port used for secure LDAP communications between Samba and the LDAP server (eDirectory). This value can be changed if your network uses a different port for secure LDAP communications. **Default**: ldap port = 636 |
| | ldap server = | Specifies the LDAP server’s hostname. Either the full DNS name or the IP address can be used. **Example**: ldap server = nnls.provo.novell.com **Default**: ldap server = *IP address* where *IP address* is the IP address of the eDirectory server. |
| | security = | This specifies the security mode. The value must be set to *user*. For more information, see www.samba.org. **Example**: security = user |
| | encrypt passwords = | This specifies that passwords received from Windows clients will be encrypted. This value must be set to *yes*. For more information, see www.samba.org. **Example**: encrypt passwords = yes |
| | workgroup = | This specifies the Windows workgroup that the Samba server will either join (if it exists) or effectively create (if the name is new). **Example**: workgroup = workgroup |
| | netbios name = | This is the LDAP name and context of the LDAP (eDirectory) server used for secure LDAP authentication. **Example**: netbios name = cn=hamachi,o=novell |