LDAP server is installed, you can start, stop, and restart the LDAP server (slapd) with the ldap startup script:

```
service ldap restart
```

> Tip Red Hat clients can enable LDAP services and select an LDAP server using the Red Hat authentication tool (authconfig-gtk) accessible as the Authentication entry in the System Settings menu and window (see Chapter 4).

# LDAP Configuration Files

All LDAP configuration files are kept in the /etc/openldap directory. These include slapd.conf, the LDAP server configuration file, and ldap.conf, the LDAP clients and tools configuration file. To enable the LDAP server, you have to manually edit the slapd.conf file, and change the domain value (dc) for the suffix and rootdn entries to your own network's domain address. This is the network that will be serviced by the LDAP server. To enable LDAP clients and their tools, you have to specify the correct domain address in the ldap.conf file in the BASE option, along with the server's address in the HOST option (domain name or IP address). For clients, you can either edit the ldap.conf file directly or use the System Settings Authentication tool, clicking the Configure LDAP button on either the User Information or Authentication panel. Here you can enter the domain name and the LDAP server's address.

# LDAP Tools

An entry in an LDAP database consists of a name (known as a distinguished name) followed by a set of attributes and their values. For example, a name could be a username and the attribute would be the user's e-mail address, the address being the attribute's value. Allowable attributes are determined by object class sets defined in the /etc/openldap/schema directory. To actually make or change entries in the LDAP database, you use the ldapadd and ldapmodify utilities. With ldapdelete, you can remove entries. Once you have created an LDAP database, you can then query it, through the LDAP server, with ldapsearch. For the LDAP server, you can create a text file of LDAP entries using an LDAP Data Interchange Format (LDIF) format. Such text files can then be read in all at once to the LDAP database using the slapadd tool. The slapcat tool extracts entries from the LDAP database and saves them in an LDIF file. To reindex additions and changes, you use the slapindex utility.

> Tip You can enable and designate LDAP servers with the authconfig-gtk tool (Authentication in the System Settings window and menu, see Chapter 4). You can also use the LDAP Browser/Editor or the GNOME Directory Administrator to manage and edit LDAP directories.

# LDAP and PAM

With LDAP, you can also more carefully control the kind of information given out and to whom. Using a PAM module (pam_ldap), LDAP can perform user authentication tasks, providing centralized authentication for users. Login operations that users perform for different services such as mail POP server, system login, and Samba logins can all be carried