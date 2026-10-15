
```
% touch file.1
%
```

2. Delete the everyone@ entry in the ACLs for file.1:

```
% setfacl -x everyone@:r-----a-R-c-s------:allow file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
    owner@:rw-p--aARWcCos:------:allow
    group@:r-----a-R-c-s------:allow
```

3. Add a new everyone@ entry. Notice the -m option places the new entry at position 0:

```
% setfacl -m everyone@:r-----a-R-c-s------:allow file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
    everyone@:r-----a-R-c-s------:allow
    owner@:rw-p--aARWcCos:------:allow
    group@:r-----a-R-c-s------:allow
```

4. Delete file.1 and create a new version of it with the default ACLs:

```
% rm file.1
% touch file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
    owner@:rw-p--aARWcCos:------:allow
    group@:r-----a-R-c-s------:allow
    everyone@:r-----a-R-c-s------:allow
```

5. Modify the position 2 everyone@ entry to rw only:

```
% setfacl -m everyone@:rw:allow file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
```

6. Add an ACL entry to deny user mansoor the read_set privileges on file.1:

```
% setfacl -m user:mansoor:read_set:deny file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
        user:mansoor:r----a-R-c--:------:deny
            owner@:rw-p--aRWcCos:------:allow
            group@:r-----a-R-c-s:------:allow
            everyone@:rw-------:------:allow
Notice what predefined permissions are included in the read_set!
```

7. Add an ACL entry to deny everyone@ the read_set privileges on file.1:

```
% setfacl -m everyone@:read_set:deny file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
            everyone@:r----a-R-c--:------:deny
            user:mansoor:r----a-R-c--:------:deny
            owner@:rw-p--aRWcCos:------:allow
            group@:r-----a-R-c-s:------:allow
            everyone@:rw-------:------:allow
```

8. Delete the ACL entry to deny everyone@ the read_set privileges:

```
% setfacl -x everyone@:read_set:deny file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
            user:mansoor:r----a-R-c--:------:deny
            owner@:rw-p--aRWcCos:------:allow
            group@:r-----a-R-c-s:------:allow
```

9. Add the following privileges to everyone@ for file.1:

```
% setfacl -m everyone@:r-----a-R-c-s:------:allow file.1
% getfacl file.1
# file: file.1
```

# owner: bob
# group: bob
    user:mansoor:------R-----;------;allow
    user:mansoor:r----a-R-c-;------;deny
    owner@:rw-p--aRWcCos:------;allow
    group@:r----a-R-c-s:------;allow
read_
After these commands are executed, does user mansoor have read_xattr permission on file.1?

# 14. Delete read_xattr permission for user mansoor on file.1:

```
% setfacl -x user:mansoor:read_xattr::allow file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
    user:mansoor:r----a-R-c-;------;deny
    owner@:rw-p--aRWcCos:------;allow
    group@:r----a-R-c-s:------;allow
```

# 15. Add r-----a-R-c--;------ privileges for user mansoor on file.1:

```
% setfacl -a 0 user:mansoor:r-----a-R-c--;------;allow file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
    user:mansoor:r-----a-R-c--;------;allow
    user:mansoor:r----a-R-c-;------;deny
    owner@:rw-p--aRWcCos:------;allow
    group@:r----a-R-c-s:------;allow
```

# 16. Delete position 1 ACL entry for file.1:

```
% setfacl -x 1 file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
    user:mansoor:r-----a-R-c--;------;allow
    owner@:rw-p--aRWcCos:------;allow
    group@:r----a-R-c-s:------;allow
```

# 17. Delete position 0 ACL entry for file.1:

```
% setfacl -x 0 file.1
```

```
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
    owner@:rw-p--aARWcCos:------:allow
    group@:r-----a-R-c-s:------:allow
```

18. Add position 0 entry of r-----a-R-c--:------ ACL for user mansoor on file.1:

```
% setfacl -a 0 user:mansoor:r-----a-R-c--:------:allow file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
    user:mansoor:r-----a-R-c--:------:allow
    owner@:rw-p--aARWcCos:------:allow
    group@:r-----a-R-c-s:------:allow
```

19. Add position 0 entry of the read_set for everyone@ on file.1:

```
% setfacl -a 0 everyone@:read_set:allow file.1
% getfacl file.1
# file: file.1
# owner: bob
# group: bob
    everyone@:r-----a-R-c--:------:allow
    user:mansoor:r-----a-R-c--:------:allow
    owner@:rw-p--aARWcCos:------:allow
    group@:r-----a-R-c-s:------:allow
```

The following steps deal with PC-BSD directories.

20. Create a new directory, under your home directory, named dir_acl, and view its default ACL entries and permissions:

```
% mkdir dir_acl
% getfacl dir_acl
# file: dir_acl
# owner: bob
# group: bob
    owner@:rwxp--aARWcCos:------:allow
    group@:r-x---a-R-c-s:------:allow
    everyone@:r-x---a-R-c-s:------:allow
```

21. Add r-----a-R-c--:------ permissions to user mansoor for the directory dir_acl:
