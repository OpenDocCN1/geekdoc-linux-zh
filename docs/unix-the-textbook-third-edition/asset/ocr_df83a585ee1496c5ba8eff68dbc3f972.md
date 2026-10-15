# # UNIX System Administration Fundamentals

```
```
# zfs set aclinherit=discard tank/usr/home/bob
# mkdir test5.dir
# setfacl -m user:bob:read_data/write_data/execute:dir inherit:allow test5.dir
# getfacl test5.dir
# file: test5.dir
# owner: bob
# group: bob
user:bob:rwx------------d----:allow
owner@:rwxp--aARWcCos:------:allow
group@:r-x---a-R-c-s:------:allow
everyone@:r-x---a-R-c-s:------:allow
```
```

If, at a later time, you decide to tighten the permission bits on a directory, the nontrivial ACL is discarded. For example:

```
```
# chmod 744 test5.dir
# getfacl test5.dir
# file: test5.dir
# owner: bob
# group: bob
owner@:rwxp--aARWcCos:------:allow
group@:r-x---a-R-c-s:------:allow
everyone@:r-x---a-R-c-s:------:allow
```
```

Finally, we will illustrate ACL inheritance with the ACL inherit mode set to noallow.

In the following ACLs allows read_data, two nontrivial ACLs with file inheritance are set. One ACL allows read_data, and one ACL denies read_data permission. Again, you must change the dataset name from tank/usr/home/bob to the whatever ZFS dataset you are working on in your system, and execute the zfs set command as superuser.

```
```
# zfs set aclinherit=noallow tank/usr/home/bob
# mkdir test6.dir
# setfacl -m user:bob:read_data:file inherit:deny test6.dir
# setfacl -m user:mansoor:read_data:file inherit:allow test6.dir
# getfacl test6.dir
# file: test6.dir
# owner: bob
# group: bob
user:mansoor:r-----------------:f----:allow
user:bob:r-----------------:f----:deny
owner@:rwxp--aARWcCos:------:allow
group@:r-x---a-R-c-s:------:allow
everyone@:r-x---a-R-c-s:------:allow
```
```