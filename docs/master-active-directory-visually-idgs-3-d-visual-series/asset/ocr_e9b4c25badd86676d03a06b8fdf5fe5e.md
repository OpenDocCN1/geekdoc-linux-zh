# THE STRUCTURE OF THE ACTIVE DIRECTORY CONTINUED

![](bbox=[0.05, 0.22, 0.47, 0.48])

*Users can see a folder view of the Active Directory.*

# Active Directory names

In the Active Directory, every object, such as users, groups, computers, printers, and so forth, has a unique name. Four kinds of names are assigned to each object.

First, each object has a *distinguished name* (DN). The DN is unique from all other objects and contains the full information needed to retrieve the object. The DN contains the domain where the object resides and the path to the object. The DN is made up of these attributes (or qualities):

+   - Domain component name (DC)
+   - Organizational unit name (OU)
+   - Common name (CN)

For example, if you wanted to access a document called “Company mission” that resides in a particular domain, the DN may read:

```
`/DC=com/DC=mycompany/OU=acct/CN=documents/CN=Company Mission`
```

By using the DN, the Active Directory can begin at the top of the domain and work its way down to the actual folder or document.

Second, the Active Directory uses *relative distinguished names* (RDN). The RDN is the part of the DN that defines the actual object, called an attribute. This is the CN, or common name. Fortunately, all you need to know to search for objects are common names. You don't have to know or use the DN, and the DN itself is normally hidden from the users.

Third, the Active Directory uses *globally unique identifiers* (GUID), which are unique 128-bit numbers. The GUID is assigned to an object when it is created in the Active Directory and it never changes.

And fourth, Active Directory objects can be identified by *user principal names* (UPN), which are short, friendly names that look like an e-mail address, such as jwilliams@corp.com.

The major point to remember is that the Active Directory provides the DN, RDN, GUID, and UPN for objects to ensure uniqueness, ease of location for LDAP queries, and ease of use for users.