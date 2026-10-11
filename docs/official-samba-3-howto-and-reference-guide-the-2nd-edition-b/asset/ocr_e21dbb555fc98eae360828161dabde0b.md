**Table 10.3 Attributes in the sambaSamAccount ObjectClass (LDAP). Part B**

| sambaUserWorkstations | Here you can give a comma-separated list of machines on which the user is allowed to login. You may observe problems when you try to connect to a Samba domain member. Because domain members are not in this list, the domain controllers will reject them. Where this attribute is omitted, the default implies no restrictions. |
|---|---|
| sambaSID | The security identifier (SID) of the user. The Windows equivalent of UNIX UIDs. |
| sambaPrimaryGroupSID | The security identifier (SID) of the primary group of the user. |
| sambaDomainName | Domain the user is part of. |

**Table 10.4 Possible ldap passwd sync Values**

| Value | Description |
|---|---|
| yes | When the user changes his password, update SambaNTPassword, SambaLMPassword, and the password fields. |
| no | Only update SambaNTPassword and SambaLMPassword. |
| only | Only update the LDAP password and let the LDAP server worry about the other fields. This option is only available on some LDAP servers and only when the LDAP server supports LDAP_EXOP_X_MODIFY_PASSWORD. |

**Table 10.5 Basic smb.conf Options for MySQL passdb Backend**

| Field | Contents |
|---|---|
| mysql host | Host name, defaults to 'localhost' |
| mysql password | |
| mysql user | Defaults to 'samba' |
| mysql database | Defaults to 'samba' |
| mysql port | Defaults to 3306 |
| table | Name of the table containing the users |