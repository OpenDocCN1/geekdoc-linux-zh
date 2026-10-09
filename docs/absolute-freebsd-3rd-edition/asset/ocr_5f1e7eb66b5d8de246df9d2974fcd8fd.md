# ## /etc/group

The file /etc/group contains all group information except for the user's primary group (which is defined with the user account in /etc/masterpasswd). Each line in /etc/group contains four colon-delimited fields: the group name, the group password, the group ID number, and a list of members.

Here's a sample entry:

```
wheel: *:0: root,mwlucas,xistence
```

The group name is a human-friendly name for the group. This group is named wheel. Group names are arbitrary; you can call a group of users lackeys if you wish. Choose group names that give you an idea of what the groups are for; while you might remember that your lackeys may edit the company web page, will your coworkers understand that?

The second field, the group password, was a great idea that turned out to be a security nightmare. Modern Unix-like systems don't do anything with the group password, but the field remains because old programs expect to find something in this space. The asterisk is a placeholder to placate such software.

The third field gives the group's unique numeric group ID (GID). Many programs use the GID rather than name to identify a group. The wheel group has a GID of 0, and the maximum GID is 65535.

Last is a comma-delimited list of all users in the group. The users root, mwlucas, and xistence are members of the group wheel.

# ### Changing Group Memberships

If you want to add a user to a group, add his username to the end of the line for that group. For example, the wheel group is the list of users that may use the root password. Here, I add rwatson to the wheel group:

```
wheel: *:0: root,mwlucas,xistence,rwatson
```

Mind you, the odds of me convincing rwatson (leading security researcher and ex-FreeBSD Foundation President) to assume sysadmin