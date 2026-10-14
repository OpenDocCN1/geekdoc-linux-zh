⇒ To list the contents of the file /etc/group, type:

```
$ cat /etc/group [RET]
```

This command uses the cat tool to output the entire contents of the file (see Recipe 9.2 [Displaying Text], page 216), listing all fields. Use cut to output only certain fields (see Recipe 13.7.4 [Removing Columns from Text], page 324).

⇒ To output a list of all group names on the system, type:

```
$ cut -d : -f1 /etc/group [RET]
```

NOTES: For more information about the user group file, consult the group man page.

# 6.1.2 Listing the Groups a User Belongs To

To list a user's group memberships, use the groups tool. Give any number of usernames as arguments, and groups will output a line for each containing a list of all of the groups the user is a member of, preceded by the username and a colon character (:). With no arguments, groups lists your own group memberships.

⇒ To list your group memberships, type:

```
$ groups [RET]
steward galley crew
$
```

In this example, three groups are output: steward (the user's login group), galley, and crew.

⇒ To list the group memberships of user marlow, type:

```
$ groups marlow [RET]
marlow : marlow
$
```

In this example, the command outputs the given username, marlow, followed by the name of one group, marlow, indicating that user marlow belongs to only one group: his login group.