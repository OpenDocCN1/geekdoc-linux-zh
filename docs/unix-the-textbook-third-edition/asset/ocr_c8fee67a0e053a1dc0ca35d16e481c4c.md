```
% zfs get aclinherit tank/usr/home/bob
NAME              PROPERTY      VALUE          SOURCE
tank/usr/home/bob aclinherit     noallow        local
% su
Password: xxx
# zfs set aclinherit=restricted tank/usr/home/bob
# exit
Exit
```

For more information, see Section 23.9.3.1.3, “ACL Inheritance.”

# 23.9.3.3.1 Granting ACLs that Are Inherited by Files

This section identifies the file ACEs that are applied when the file_inherit flag is set.

In the following example, read_data/write_data permissions are added for files in the test2.dir directory for user bob so that he has read access on any newly created files.

```
% mkdir test2.dir
% setfacl -m user:bob:read_data/write_data:file_inherit:allow test2.dir
% getfacl test2.dir
# file: test2.dir
# owner: bob
# group: bob
    user:bob:rw----:ARWc---:f----:allow
    owner@:rwxp--aARWcCos:-----:allow
    group@:r-x---a-R-c--s:-----:allow
    everyone@:r-x---a-R-c--s:-----:allow
```

In the following example, user bob’s permissions are applied on the newly created test2.dir/file.2. The ACL inheritance granted, read_data:file_inherit:allow, means user bob can read the contents of any newly created file.

```
% touch test2.dir/file.2
% getfacl test2.dir/file.2
# file: test2.dir/file.2
# owner: bob
# group: bob
    user:bob:r-----:------:------:allow
    owner@:rw-p--aARWcCos:-----:allow
    group@:r-----a-R-c--s:-----:allow
    everyone@:r-----a-R-c--s:-----:allow
```

Thus, user bob does not have write_data permission on file.2 because the group permission of the file does not allow it.