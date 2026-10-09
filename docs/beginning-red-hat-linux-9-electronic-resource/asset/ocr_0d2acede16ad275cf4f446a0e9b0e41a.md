He can also remove users from that group:

```
```
$ gpaswd -d deepakt authors
Removing user deepakt from group authors
```
```

# # Revoking a User's Permission to Manage Membership of a Group

Finally, we can see what happens when root revokes administration rights for *eziom*. This can be done passing an empty list to the `-A` option:

```
```
# gpaswd -A '' authors
```
```

To test that this command has indeed revoked *eziom*'s right to manage the *authors* group, we can switch users to *eziom* and use that account context to try to reinsert *deepakt* as a member of the *authors* group:

```
```
# su - eziom
$ gpaswd -a deepakt authors
Permission denied.
```
```

As you can see, *eziom* no longer has the rights to add members to the *authors* group.

If you want to find out something more about *gpaswd*, you can check its manual page with `man gpaswd` at your shell prompt.

> When you add new members to a group, or remove members from a group, your changes are not visible until the next login, either via `su` – or by logging out completely and logging back in. If you use `su` – followed by your account name (or even `newgrp` followed by a group you've just been given access to), only commands you type in that shell (try for example `id`) will be affected by the new membership.

# # Deleting Groups

It is advisable to delete a group only when it doesn't contain any members. It is possible to delete secondary groups with user accounts still associated to it. Moreover, deleting a group (just like deleting a user account) could leave “stale” files whose group no longer exists. You can run the following command periodically as root on your system, to identify these files:

```
```
# find / -nouser -o -nogroup
```
```

From there, you can reassign these files to valid users or groups.

To delete a group via the Red Hat User Manager GUI utility, you need to select the group, and click the *Delete* button.

> Beware: the group is deleted immediately, and *without confirmation*!