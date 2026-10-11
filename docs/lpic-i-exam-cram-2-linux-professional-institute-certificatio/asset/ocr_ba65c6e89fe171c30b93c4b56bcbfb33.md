> **NOTE**
> 
> The primary group for a user is special; if a user is assigned a primary group in the */etc/passwd*, she does not have to be listed as a member in the */etc/group* file because the GID in the */etc/passwd* entry supersedes secondary group membership.

+   > **Secondary**—The user’s name appears in the */etc/group* entry for that group, the user is a member of that group, and she gets access to the resources that group is the group owner of.

> **ALERT**
> 
> A group assigned as a primary group to any user cannot be deleted because doing so would orphan the user’s account and cause untold problems for you and the user.

Groups are organized in much the same way that users are as far as the GID numbering group ID (GID) associated with the name. Two tables of static. Some interesting accounts are listed here:

+   > **0**—The root group; anyone who is a member of this group may have access to resources that are restricted to the root account.

+   > **1**—The bin group is similar to the bin account.

+   > **100**—The users group is where you can place normal users and then give them access to resources by assigning that group ownership of things that all users should have access to.

> **ALERT**
> 
> The *wheel* group is not implemented by default on Linux systems. On BSD-related systems, a user cannot use the *su* command unless her account is a member of the *wheel* group, even if she knows the root password! Linux does not use this, but the group is there for compatibility.

A special situation exists primarily on Red Hat machines, in which a user account is created without a specific primary group assigned. In this case, the system creates and assigns a group whose GID matches the numerals in the user’s UID, or the next incremented number available.

This is a security feature. If you have created a user and haven’t assigned her a primary group, the system might assign her the users group as a primary group. This is a security risk because this user might be a contractor or an auditor and by default should not have access to the users group resources.

Debian creates the user with the primary group set to the users (100 group.