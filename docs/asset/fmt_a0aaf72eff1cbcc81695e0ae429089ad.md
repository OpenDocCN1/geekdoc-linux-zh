
## `chmod` 参数填充

If you enter a number with fewer than four digits as an argument to `chmod`, omitted characters are replaced with zeros starting from the left. In other words, `chmod 77` is the same as `chmod 0077`.

如果将少于四位数的数字作为 `chmod` 的参数输入，则省略的字符将从左侧开始用零填充。换句话说，`chmod 77` 与 `chmod 0077` 相同。

### 更改用户和组所有权

If the wrong user or group now owns a file or directory, the error can be repaired using the `chown` (change owner) and `chgrp` (change group) commands. Changing file ownership is a frequent system administrative task in environments where files need to be shared within a group.

如果错误的用户或组现在拥有文件或目录，可以使用 `chown`（更改所有者）和 `chgrp`（更改组）命令修复错误。在需要组内共享文件的环境中，更改文件所有权是频繁的系统管理任务。

The `chown` command can be applied to change both user and group ownership of a file/directory, while `chgrp` changes only the group ownership. Of course, the system will check if the user issuing one of these commands has sufficient permissions on the file(s) to be changed. The general syntax of `chown` is

`chown` 命令可用于更改文件/目录的用户和组所有权，而 `chgrp` 仅更改组所有权。当然，系统会检查发出其中一个命令的用户是否对要更改的文件具有足够的权限。`chown` 的一般语法是

```
chown [options] newuser[:newgroup] file
```

Instead of names, numeric `UID/GID` may be used instead.

可以使用数字 `UID/GID` 代替名称。

If a colon is used after the username and no group name is given, group ownership will be changed to the primary group of the (administrative) user issuing the command. If no username is provided but a `:newgroup` is specified, `chown` changes the group owner, performing the same function as `chgrp`, whose general syntax is

如果在用户名后使用冒号且未给出组名，则组所有权将更改为发出命令的（管理员）用户的初始组。如果未提供用户名但指定了 `:newgroup`，则 `chown` 会更改组所有者，执行与 `chgrp` 相同的功能，其一般语法是

```
chgrp [options] newgroup file
```

#### 注意

With SLES, instead of a colon in the `chown`/`chgrp` commands, you can use a period instead. However, it is a more standard convention to use a colon.

在 SLES 中，在 `chown`/`chgrp` 命令中使用冒号时，可以改用句点。然而，使用冒号是更标准的惯例。

Both `chown` and `chgrp` can be used to change ownership recursively, using the `-R` option. In that case, all underlying files and subdirectories of a given directory will belong to the given user and/or group.

`chown` 和 `chgrp` 都可以使用 `-R` 选项递归更改所有权。在这种情况下，给定目录下的所有底层文件和子目录都将属于指定的用户和/或组。

#### 提示

You can use the `--from=user[:group]` option with `chown` so that only those files and directories whose current owner and/or group match those specified will be assigned a new user and/or group owner. This capability is useful in reassigning ownership if the files and directories are scattered across a number of branches of a filesystem.

你可以使用 `chown` 的 `--from=user[:group]` 选项，以便只有当前所有者和/或组与指定项匹配的文件和目录才会被分配新的用户和/或组所有者。如果文件和目录分散在文件系统的多个分支中，此功能在重新分配所有权时很有用。

### 安全考虑

Incorrect file permissions may allow some users to read or modify files that they don’t supposedly have access to. The following are two incorrect file permission exploits a hacker will take advantage of: world-accessible (read and/or write) files and group-owned files.

不正确的 `access_mode_options` 使用 `+`、`-` 和 `=` 运算符来向给定组添加、移除或分配权限。允许使用逗号分隔的组合。以下示例授予 `test` 的所有者完全访问权限，同时移除组所有者和世界的所有访问权限。

```
Athena: /home/admin/demo # chmod u=rwx,go-rwx test
```

#### 注意

If you specify more than one mode option, as is in the preceding example, ensure there are no spaces before or after the comma. For example, if you used `chmod u=rwx, go-rwx test`, `chmod` considers what comes after the space (`go-rwx test`) as filenames and results in a “No such file or directory” error when trying to access `go-rwx`.

如果指定多个模式选项，如前例所示，请确保逗号前后没有空格。例如，如果你使用 `chmod u=rwx, go-rwx test`，`chmod` 会将空格后的内容 (`go-rwx test`) 视为文件名，并在尝试访问 `go-rwx` 时导致 “No such file or directory” 错误。

If a file’s owner currently has the `rw` permission, for example, `chmod u=rx` will overwrite the current access rights with the new ones, while `chmod u+rx` will add the execute permission (because the read permission already has been granted).

如果文件的所有者当前具有 `rw` 权限，例如，`chmod u=rx` 将用新权限覆盖当前访问权限，而 `chmod u+rx` 将添加执行权限（因为读权限已经授予）。
