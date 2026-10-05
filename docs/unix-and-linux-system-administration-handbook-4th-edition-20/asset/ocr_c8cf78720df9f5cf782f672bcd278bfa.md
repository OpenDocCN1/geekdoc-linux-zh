# LDAP and security

memberOf: CN=Enterprise Admins,CN=Users,DC=boulder,DC=atrust,DC=com
name: ned
sAMAccountName: ned
userPrincipalName: ned@boulder.atrust.com
lastLoginTimestamp: 12908695248943974
mail: ned@atrust.com

ldapsearch -h and -p flags specify the host and port of the LDAP server you want to query, respectively.

You usually need to authenticate yourself to the LDAP server. In this case, the -x flag requests simple authentication (as opposed to SASL). The -D flag identifies the distinguished name of a user account that has the privileges needed to execute the query, and the -W flag allows ldapsearch prompt you for the password.

The -b flag tells ldapsearch where in the LDAP hierarchy to search. The parameter is known as the baseDN; by default, ldapsearch returns all entries below the baseDN; you can change this behavior with the -s flag.

The last argument is "filter," which is a description of what you're searching. It doesn't require an option flag. This filter, cn=ned*, returns all LDAP entries that have a common name that starts with “ned”. The filter is quoted to protect the search from shell globbing.

If you want to extract all entries below a given baseDN, just use objectClass=* as the search filter—or leave the filter out, since that is the default.

Any arguments that follow the filter select specific attributes to return. For example, if you added givenName to the command line line, ldapsearch will return only those attributes of matching entries.

# LDAP and security

Traditionally, LDAP was used more in the manner of a phone directory than anything else, and it was usually acceptable. As a result, the “standard” LDAP implementation grants unencrypted access through TCP port 389. However we strongly advise against the use of unencrypted LDAP for the transmission of authentication information, even if passwords are individually hashed or encrypted.

As an alternative, LDAP-over-SSL (known as LDAPS, usually running on TCP port 686) is available in most situations (including the Microsoft world) on both the client and server. This access method is preferred because it protects the information contained in both the query and the response. Use LDAP when possible.

A system as complex as LDAP inevitably has the potential to be misconfigured in a way that weakens security. Of course it is likely to contain some old-fashioned security holes, too. Caveat administrator.