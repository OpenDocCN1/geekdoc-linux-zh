
该值是一个被授予只读权限的用户列表。它会覆盖任何 `read-only=`、`writable=` 等语句，将列出的用户限制为只读访问。如果 `read list=` 上的任何用户也在该共享的 `write list=` 选项中，则 `read list=` 将被覆盖，该用户可以在目录中写入。

`read list=` 会覆盖 `valid users=` 吗？这是一个有趣的问题。当一个未出现在共享现有 `valid users=` 列表的用户出现在 `read list=` 列表中时，该用户会被提示输入密码，无论输入谁的密码，都会将该用户踢出。这种行为在 Samba 的 `smclient` 程序和 Windows® 网络中是完全对应的。因此，它并没有覆盖 `valid users=` 或 `invalid users=`。例如：

```ini
[spec_dir]
path = /home/everyone/spec
valid users = valerie,tackett
writable = yes
read list = valerie,tackett,myuid
write list = tackett
```

在这个示例中，目录 `/home/everyone/spec` 可以被 Valerie 和 tackett 读取，但不能被 myuid 读取（因为没有针对 myuid 的 `valid users=` 条目）。Valerie 无法写入该目录，因为她在 `read list=` 中的条目覆盖了 `writable=` 选项。然而，tackett 可以写入，因为他的 `write list=` 条目覆盖了他的 `read list=` 条目。

## `write list=` (S)

任何共享都可以包含一个可以向该共享写入的用户列表，无论 `writeable` 或 `read list+` 选项如何规定。这里有一个示例，为 `bill`、`tackett` 和 `myuid` 提供 `[billsdir]` 的写入权限，尽管该目录被设置为只读的：

```ini
[billsdir]
valid users = bill, tackett, myuid
read only = yes
write list = bill, tackett, myuid
```

## `path=` (S)

`path=` 是通过共享访问的目录。在打印共享的情况下，它是溢流目录（此处是在提交给 `printcap` 打印机之前，该打印机可能有自己的溢流目录）。注意，如果 `[global]` 节包含 `root dir=` 或 `root directory;`，路径将相对于指定为根的目录。

## `create mask=` and `create mode=` (S)

`create mask=` 和 `create mode=` 是同义词。它们指定了新创建文件的最大权限。DOS 权限（只读、隐藏等）会进一步限制它。默认值是 `744`，意味着用户获得所有权限，但组只有读取权限。如果所有者随后从 DOS 将文件标记为只读，则文件在 Linux 上的实际模式将变为 `544`，以反映写入权限的丢失。

## `browseable=` (S)

`browseable=` 条目指示 SMB 客户端在 SMB 客户端浏览器（如网络）中列出该共享。如果 `[global]` 节包含 `root dir=` 或 `root directory;`，路径将相对于指定为根的目录。

## `create mask=` and `create mode=` (S)

`create mask=` 和 `create mode=` 是同义词。它们指定了新创建文件的最大权限。DOS 权限（只读、隐藏等）会进一步限制它。默认值是 `744`，意味着用户获得所有权限，但组只有读取权限。如果所有者随后从 DOS 将文件标记为只读，则文件在 Linux 上的实际模式将变为 `544`，以反映写入权限的丢失。

## `browseable=` (S)

`browseable=` 条目指示 SMB 客户端在 SMB 客户端浏览器（如网络）中列出该共享。如果 `[global]` 节包含 `root dir=` 或 `root directory;`，路径将相对于指定为根的目录。

## 特殊约定

许多期望用户作为值的选项也可以接受组。在这些情况下，值是带有 `@` 符号（`@`）引导的组名。例如，组 `acct` 可以表示为 `@acct`。

在 `smb.conf` 中可以使用几个替换字符。它们在 `smb.conf` 的 man 页面上均有解释。其中，`%u` 和 `%H` 特别有用。`%u` 将替换为用户名，而 `%H` 将替换为用户的家目录。例如，这里有一个共享，将 `/home/everyone` 下的文档目录提供给每个用户，因为管理员已经在 `/home/everyone` 下创建了一个以用户名命名的目录：

```ini
[everyone]
comment = Accessible to everyone
path = /home/everyone/%u
browable = yes
public = no
writeable = yes
create mode = 700
```

注意，上述内容并非完成此任务的最佳方法。它仅仅是 `%u` 替换的演示。

## `read only=`, `writeable=`, `writable=`, and `write ok=` (S)

`writeable=`、`writable=` 和 `ok=` 是同义词，意味着它们可以完全互相替换。`read only=` 是 `writeable=`、`writable=` 和 `write ok=` 的反向同义词，这意味着 `read only=` 替换 `writeable=no`，以此此类推；`read only` 替换 `writeable=yes`，同样如此。这四个选项中只需指定一个来确定共享是否可写。如果在 `[global]` 节中指定了此选项，它将作为所有共享的默认值（所有可以放在共享定义中的选项都是如此）。注意，这些选项可以被 `write list=` 覆盖。

```ini
read only=no
writeable=yes
writeable=yes
write ok=yes
```

这四个选项的含义相同且可以互换。默认是 `read only=yes`。

## `valid users=`(S)

在任何共享中，缺少 `valid users=` 选项或等号后值为空会导致该共享对所有人开放（这可能不是你想要的）。要限制访问，请在等号后放置一个逗号分隔的有效用户列表：

```ini
valid users = myuid, tackett, @acct
```

此选项允许用户 `myuid`、`tackett` 以及组 `acct` 访问。此选项会被 `invalid users=` 选项覆盖。

## `invalid users=` (S)

这是一个无法访问此共享的用户列表。此列表会覆盖共享中 `valid users=` 选项中的任何用户。

```ini
[team]
valid users = myuid,tackett,art
invalid users = myuid,tackett
```

上述 `smb.conf` 代码段仅允许 `art` 访问 `[ateam]`。

## `read list=` (S)

该值是一个被授予只读权限的用户列表。它会覆盖任何 `read-only=`、`writable=` 等语句，将列出的用户限制为只读访问。如果 `read list=` 上的任何用户也在该共享的 `write list=` 选项中，则 `read list=` 将被覆盖，该用户可以在目录中写入。

`read list=` 会覆盖 `valid users=` 吗？这是一个有趣的问题。当一个未出现在共享现有 `valid users=` 列表的用户出现在 `read list=` 列表中时，该用户会被提示输入密码，无论输入谁的密码，都会将该用户踢出。这种行为在 Samba 的 `smclient` 程序和 Windows® 网络中是完全对应的。因此，它并没有覆盖 `valid users=` 或 `invalid users=`。例如：

```ini
[spec_dir]
path = /home/everyone/spec
valid users = valerie,tackett
writable = yes
read list = valerie,tackett,myuid
write list = tackett
```

在这个示例中，目录 `/home/everyone/spec` 可以被 Valerie 和 tackett 读取，但不能被 myuid 读取（因为没有针对 myuid 的 `valid users=` 条目）。Valerie 无法写入该目录，因为她在 `read list=` 中的条目覆盖了 `writable=` 选项。然而，tackett 可以写入，因为他的 `write list=` 条目覆盖了他的 `read list=` 条目。

## `write list=` (S)
