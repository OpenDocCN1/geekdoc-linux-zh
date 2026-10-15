
## ACL inheritance

Like POSIX ACLs, NFSv4 ACLs allow newly created objects to inherit access control entries from their enclosing directory. However, the NFSv4 system is a bit more powerful and a lot more confusing. Here are the important points:

- Any ACE can be flagged as inheritable. Inheritance for newly created subdirectories (`dir_inherit` or `d`) and newly created files (`file_inherit` or `f`) are flagged separately.
- You can apply different access control entries to new files and new directories by creating separate access control entries on the parent directory and flagging them appropriately. You can also apply a single ACE to all new child entities (of whatever type) by turning on both the `d` and `f` flags.
- From the perspective of access determination, access control entries have the same effect on the parent (source) directory whether or not they are inheritable. If you want an entry to apply to children but not to the parent directory itself, turn on the ACE’s `inherit_only` (`i`) flag.
- New subdirectories normally inherit two copies of each ACE: one with the inheritance flags turned off, which applies to the subdirectory itself; and one with the `inherit_only` flag turned on, which sets up the new subdirectory to propagate its inherited ACEs. You can suppress the creation of this second ACE by turning on the `no_propagate` (`n`) flag on the parent directory’s copy of the ACE. The end result is that the ACE propagates only to immediate children of the original directory.
- Don't confuse the propagation of access control entries with true inheritance. Your setting an inheritance-related flag on an ACE simply means that the ACE will be copied to new entities. It does not create any ongoing relationship between the parent and its children. If you later change the ACE entries on the parent directory, the children are not updated.

Table 6.10 summarizes these various inheritance flags.

### Table 6.10 NFSv4 ACE inheritance flags

| Code | Verbose name | Meaning |
|---|---|---|
| f | file_inherit | Propagate this ACE to newly created files |
| d | dir_inherit | Propagate this ACE to newly created subdirectories |
| i | inherit_only | Propagate, but don't apply to the current directory |
| n | no_propagate | Propagate to new subdirectories, but not their children |

## NFSv4 ACL viewing in Solaris

![](img/14d78e3cecac4581d37024baf1e94cca_217_0.png)

Solaris has integrated its ACL support into **ls** and **chmod**, which is a nice approach and a straightforward extension of the commands’ usual functions. Both

POSIX and NFSv4 ACLs are supported in this manner, although here we show only NFSv4 examples. The specific flavor of ACLs that you see or set depends on the underlying filesystem.

ls -v shows ACL information for filesystem objects. As with -l, you must include the -d option if you want to see the ACL for a directory; otherwise ls -v shows the ACL of every child of the directory. Here’s a simple (!) example:

```
solaris# mkdir /var/tmp/example
solaris# ls -dv /var/tmp/example
drwxr-xr-x 2 garth staff 2 jan 11 07:19 /var/tmp/example
0:owner@:deny
1:owner@:list_directory/read_data/add_file/write_data/add_subdirectory/append_data/write_xattr/execute/write_attributes/write_acl/write_owner:allow
2:group@:add_file/write_data/add_subdirectory/append_data:deny
3:group@:list_directory/read_data/execute:allow
4:everyone@:add_file/write_data/add_subdirectory/append_data/write_xattr/write_attributes/write_acl/write_owner:deny
5:everyone@:list_directory/read_data/read_xattr/execute/read_attributes/read_acl/synchronize:allow
```

This newly created directory seems to have a complex ACL, but in fact it’s a fake—this ACL is just the nine-bit mode shown on the first line of output translated into ACLEse. It is not necessary for the filesystem to store an actual ACL because the ACL and the mode are equivalent. (Such ACLs are termed “trivial.”) If the directory had an actual ACL, ls would show the mode bits with a + on the end (i.e., drwxr-xr-x+) to indicate the presence of the ACL.

Each numbered clause represents one access control entry. The format is
index:entity:permissions:inheritance_flags:type

The index numbers are added by ls for clarity and are not part of the actual ACL. They can be used in later chmod commands to identify a specific ACE to be replaced or deleted.

The entity can be the keywords owner@, group@, or everyone@, or a form such as user:username or group:groupname.

The type of an ACE is either allow or deny. Theoretically, alarm and audit are allowed as well, but ZFS doesn’t implement these features.

Both the permissions and the inheritance_flags are slash-separated lists of options. Strangely, ls omits the inheritance_flags field (and one of the colon delimiters) if the flags are all turned off, but it does not do the same with the permissions.

For added confusion, ls displays multiple names for the r (read data/list directory), w (write data/add file), and p (append data/add subdirectory) permission bits, as if they were separate permissions. In fact, they are file- and directory-specific interpretations of the same bits and will always be present or absent together.
