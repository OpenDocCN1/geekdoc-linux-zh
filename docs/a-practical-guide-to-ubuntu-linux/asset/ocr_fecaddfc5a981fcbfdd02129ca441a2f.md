# userdel: REMOVES A USER ACCOUNT

The userdel utility deletes a user's account. If appropriate, back up the files belonging to the user before deleting them. The following command removes Max's account. The --remove (-r) option causes the command to remove his home directory:

```
$ sudo userdel --remove max
```

See the userdel man page for more information.

# usermod MODIFIES A USER ACCOUNT

To turn off a user's account temporarily, you can use usermod to change the expiration date for the account. Because it specifies that his account has expired in the past (December 31, 2009), the following command line prevents Max from logging in:

```
$ sudo usermod -e "12/31/09" max
```

See the usermod man page for more information.

# grouppadd ADDS A GROUP

Just as useradd adds a new user to the system, grouppadd adds a new group by adding an entry to /etc/group (page 492). The following example creates a group named pubs:

```
$ grouppadd -g 1024 pubs
```

Unless you use the -g option to assign a group ID, the system picks the next available sequential number greater than 1000. The -g option allows the group ID to be nonunique, which allows you to assign multiple names to a group ID.

# groupdel REMOVES A GROUP

The analogue of userdel for groups is groupdel, which takes a group name as an argument. You can also use groupmod to change the name or group ID of a group, as in the following examples:

```
$ sudo groupmod -g 1025 pubs
$ sudo groupmod -n manuals pubs
```

The first example gives the previously created pubs a new group ID number.
The second example renames the pubs group to manuals.

# Changing group ID numbers

The group utility does not change group numbers in /etc/passwd when you renumber a group. Instead, you must edit /etc/passwd and change the entries manually. If you change the number of a group, files that are associated with the group will no longer be associated with the group. Rather, they may be associated with no group or another group with the old group ID number.

> caution