into a client). I had file permission problems. Changing dylan's UID in Active Directory to 102,
the original value, fixed everything.

Also, in HP-UX the default GID for the users group is 20. But Server for NIS reserves
GIDs below 100. So, you either have to change the GID to a number over 100 in Server for NIS
 leave alone and ensure the name service switch consults files at some point. If you want to
 sure your name service switch works properly, use the nsquery utility. For example:

```
# /usr/contrib/bin/nsquery group users
```

Using "files nis" for the group policy.

```
Searching /etc/group for users
Group name: users
Group Id: 20
Group membership: root
Switch configuration: Terminates Search
```

Note that nsquery found the users group with GID 20, because the name service switch
consults /etc/group first.

![](bbox=[0.095, 0.493, 0.574, 0.918])

Figure 10–11 The UNIX Attributes tab. Run Start→Programs→Administrative Tools�Active
Directory Users and Computers. Then right-click the user and choose Properties.