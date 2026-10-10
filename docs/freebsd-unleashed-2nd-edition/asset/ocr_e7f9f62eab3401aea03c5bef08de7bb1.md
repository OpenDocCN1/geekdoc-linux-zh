If you then run the `getfacl` command again, you get the following output:

```
```
#file:acltest.txt
#owner:0
#group:0
user::rww-
user:fooBar:rw-          # effective: r--
group::r--
mask::r--
other::---
```
```

Notice that the user `fooBar` still has read and write permissions listed. However, because of the mask, fooBar’s effective permissions are read-only.

You can also add several ACLs with a single command line by separating them with commas. Here’s an example:

```
```
# setfacl -n -m u:fooBar:rw,g:guest:r,g:visitors:r acltest.txt
```
```

This command gives read and write access to the user fooBar, read access to the user guest, and read access to the group visitors. In addition, the use of the `-n` option prevents the mask from being updated, even if the current mask doesn’t allow some of the permissions you assign in this statement.

# ## Denying Access with ACLs

Just as an ACL can be used to allow users and groups to have access to a file or directory that they otherwise could not access, it can also be used to deny access to users and groups that otherwise would have access. For example, the following command creates an ACL entry for the user fooBar that contains no permissions:

```
```
# setfacl -m u:fooBar: acltest.txt
```
```

In this case, the user fooBar is denied all access to the file `acltest.txt`, even if fooBar is a member of the group that owns the file and that group has access to the file. The ACL overrules the standard file permissions and denies the user access, even if the standard file permissions would allow the user access.

# ## Deleting an ACL Entry

Use the `-x` option with `setfacl` to delete an ACL entry. For example, the following command removes the entire entry for the user fooBar:

```
```
# setfacl -x u:fooBar: acltest.txt
```
```