# Getting Information About Your Userid with id

Occasionally, you may need to find out information about your userid, such as your userid's numeric value and to what groups you belong. This information is essential when you're sharing files (as discussed in Chapter 5) because you'll need it to let people access your files and to access theirs. You can easily get information about your userid with id, as shown in Code Listing 7.13.

# To check userid information using id:

+   - id

At the shell prompt, type id to find the numeric value of your userid and to what groups you belong (by name and numeric userid value) you belong (see Code Listing 7.13). See Finding Out Which Group You're In, in Chapter 5, for more about the /etc/group file.

# Tips

+   - You can also check someone else's status with id to find out what groups they're in. Just use id userid (substituting the other person's userid for userid, of course).
+   - Use groups to find out which groups—in human-readable terms—a specific userid is in. For example, ejr is in the ejr, wheel, and users groups, as shown in Code Listing 7.13.

```
[ejr@hobbes ejr]$ id
uid=500(ejr) gid=500(ejr) groups=500(ejr),10(wheel),100(users)
[ejr@hobbes ejr]$ id deb
uid=505(deb) gid=505(deb) groups=100(users)
[ejr@hobbes ejr]$ groups ejr
ejr : ejr wheel users
```

Code Listing 7.13 Use id to get information about userids and group memberships.