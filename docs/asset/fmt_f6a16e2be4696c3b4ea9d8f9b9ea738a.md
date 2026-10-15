
# owner: bob
# group: bob
    user:mansoor:------R-----;------;allow
    user:mansoor:r----a-R-c-;------;deny
    owner@:rw-p--aRWcCos:------;allow
    group@:r----a-R-c-s:------;allow
read_
执行这些命令后，用户 `mansoor` 是否拥有对 `file.1` 的 `read_xattr` 权限？

## 14. 删除用户 `mansoor` 对 `file.1` 的 `read_xattr` 权限：

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

## 15. 为 `file.1` 上的用户 `mansoor` 添加 `r-----a-R-c--;------` 权限：

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

## 16. 删除 `file.1` 的位置 1 ACL 条目：

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

## 17. 删除 `file.1` 的位置 0 ACL 条目：

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

## 18. 为 `file.1` 上的用户 `mansoor` 添加位置 0 的 `r-----a-R-c--:------` ACL 条目：

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

## 19. 为 `file.1` 上的用户 `everyone@` 添加位置 0 的 `read_set` 条目：

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

以下步骤讨论 PC-BSD 目录。

## 20. 在主目录下创建一个名为 `dir_acl` 的新目录，并查看其默认 ACL 条目和权限：

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

## 21. 为目录 `dir_acl` 的用户 `mansoor` 添加 `r-----a-R-c--:------` 权限：

```
% setfacl -a 0 user:mansoor:r----a-R-c--:------:allow
dir_acl

% getfacl dir_acl

# file: dir_acl

# owner: bob

# group: bob

    user:mansoor:r----a-R-c--:------:allow

    owner@:rwxp--aARWcCos:------:allow

    group@:r-x---a-R-c-s:------:allow

    everyone@:r-x---a-R-c-s:------:allow
```

## 22. 在目录 `dir_acl` 上为用户 `mansoor` 在位置 0 添加一些额外权限：

```
% setfacl -a 0 user:mansoor:read_set/execute:file_inherit/
dir_inherit:allow dir_acl

% getfacl dir_acl

# file: dir_acl

# owner: bob

# group: bob

    user:mansoor:r-X---a-R-c--:fd---:allow

    user:mansoor:r----a-R-c--:------:allow

    owner@:rwxp--aARWcCos:------:allow

    group@:r-x---a-R-c-s:------:allow

    everyone@:r-x---a-R-c-s:------:allow
```

## 23. 删除 `dir_acl` 的位置 1 ACL 条目：

```
% setfacl -x 1 dir_acl

% getfacl dir_acl

# file: dir_acl

# owner: bob

# group: bob

    user:mansoor:r-X---a-R-c--:fd---:allow

    owner@:rwxp--aARWcCos:------:allow

    group@:r-x---a-R-c-s:------:allow

    everyone@:r-x---a-R-c-s:------:allow
```

## 24. 删除 `dir_acl` 的位置 0 ACL 条目：

```
% setfacl -x 0 dir_acl

% getfacl dir_acl

# file: dir_acl

# owner: bob

# group: bob

    owner@:rwxp--aARWcCos:------:allow

    group@:r-x---a-R-c-s:------:allow

    everyone@:r-x---a-R-c-s:------:allow
```

## 25. 为 `dir acl` 上的用户 `bob` 添加长格式权限

```
% setfacl -a 0 user:bob:read_data/write_data/execute:file_inherit/dir_inherit:allow / dir_acl
```

```
# file: dir_acl

# owner: bob

# group: bob

user:bob:rwx------------fd----:allow

owner@:rwxp--aARWcCos:------:allow

group@:r-x---a-R-c-s:------:allow

everyone@:r-x---a-R-c-s:------:allow
```
