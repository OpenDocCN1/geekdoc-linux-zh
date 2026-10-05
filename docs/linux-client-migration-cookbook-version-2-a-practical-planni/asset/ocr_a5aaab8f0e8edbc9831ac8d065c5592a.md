# The windbind separator

Using windbind will lead to a choice for what is used as the windbind-separator. This is the character that will separate the domain name from the username in the Linux username. For example, AD6380+Administrator is the Linux username of the user Administrator in domain AD6380 when the windbind-separator is a plus (+). The impact of the chosen character has to be studied in all applications and network services used. Using the plus (+) character for separation generally is the best choice for Linux shells and applications.

**Planning tip:** Plan and test windbind and the windbind separator extensively to validate the setting prior to migrating clients.

# LDAP connect to changed Active Directory

Advantages:

+   - Mapping users to uid and gid is done within the AD, that is, centrally.
- LDAP is a general protocol to connect to AD.

Disadvantages:

+   - The AD schema needs to be changed.

Using LDAP means that it might be necessary to change the Active Directory schema to include UNIX-like information such as a uid and gid for users and groups. Microsoft's Service for UNIX can be used to do this.

> **Planning tip:** When planning to use LDAP with Active Directory to authenticate, check whether it is possible to extend the Active Directory schema in your organization.

# LDAP connect to directory synchronized with Active Directory

Advantages:

+   - Mapping users to uid and gid is done within a central directory.
- LDAP is a general protocol to connect to directories.

Disadvantages:

+   - The two different directories have to be synchronized.

Synchronizing two directories, each containing different objects with partially different definitions, is not a trivial exercise. This is one of the reasons that this method is not discussed in Chapter 9, "Integration how-tos" on page 195.