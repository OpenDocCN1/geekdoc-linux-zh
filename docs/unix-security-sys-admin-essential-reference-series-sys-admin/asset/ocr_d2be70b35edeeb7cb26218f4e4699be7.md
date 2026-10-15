The password files of the client machines are then modified. These files will typically contain +::+::0:0::: as the final entry. A UID of + indicates that the entire NIS passwd map should be appended to the local passwd file. The disabled password for the user + is used to maintain security on some older systems, and the user and group IDs of 0 are included so the line has the format of a valid entry. The entire NIS map does not need to be included, so the +::+::0:0::: entry is removed and replaced with entries of the form +@netgroup, where netgroup is the name of a netgroup containing user accounts with access to the machine. Figure 6.2 shows a portion of a passwd file from an NIS client that only allows logins from NIS users in the sales netgroup.

Similarly, you can exclude netgroups of users from the password file by retaining the +::+::0:0::: and including -@netgroup entries. Figure 6.3 shows a segment from a passwd file allowing logins from all NIS users except those in the staff netgroup.

# Figure 6.1 A segment of a netgroup file specifying groups and members.

```
staff:(tim,)(jill,)
sales:(brad,)(randy,)(mark,)
```

# Figure 6.2 A segment of a passwd file allowing logins for only the sales netgroup.

```
root:x:0:1:Super-User:/:/sbin/sh
daemon:x:1:1:::/
...
+@sales
```

# Figure 6.3 A segment of a passwd file allowing logins for all users except the staff netgroup.

```
root:x:0:1:Super-User:/:/sbin/sh
daemon:x:1:1:::/
...
-@staff
+::+::0:0:::
```