The value is a list of users to be given read-only access. This overrides any **read only=**, **writable=**, and so on, restricting the listed users to read-only access. If any user on the **read list=** list is also on the **write list=** option for the share, **read list=** is overridden and that user can write in the directory.

Does **read list=** override **valid users=?** That's an interesting question. When a user not appearing in an existing **valid users=** list for the share appears in the **read list=** list, that user is prompted for a password. No matter whose password is input, the user is kicked out. This behavior is exactly mirrored by Samba's **smbclient** program and Windows Network Neighborhood. Here is an example:

```
```
[spec_dir]
path = /home/everyone/spec
valid users = valerie, tackett
writable = yes
read list = valerie, tackett, myuid
write list = tackett
```
```

In this example, the **/home/everyone/spec** directory can be read by **valerie** and **tackett**, but not by **myuid** (no **valid users=** entry for **myuid**). User **valerie** cannot write the directory because her entry in **read list=** overrides the **writable=** option. However, **tackett** can write it because his **write list=** entry overrides his **read list=** entry.

# write list= (S)

Any share can have a list of users who can write to that share, no matter what the **writable=** or **read list=** options say. Here's an example giving write access to [bill**dir**] for **bill**, **tackett**, and **myuid**, in spite of the fact that the directory is option to be read-only:

```
```
[billdir]
valid users = bill, tackett, myuid
read only = yes
write list = bill, tackett, myuid
```
```

# path= (S)

This is the directory accessed through the share. In the case of a print share, it's the spool directory (spool here before submitting to the printcap printer, which may also have its own spool). Note that, if the **[global]** section contains a **root=**, **root dir=**, or **root directory=**, the **path=** will be relative to the directory specified as the **root**.