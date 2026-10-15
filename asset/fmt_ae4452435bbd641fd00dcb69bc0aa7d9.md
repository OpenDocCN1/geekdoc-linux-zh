
`/etc/password:jobob:x:503:503::/home/jobob:/bin/bash`

# 第 21 章：管理用户和组

`/etc/shadow:jobob::11589:0:99999:7:::`  
`/etc/group:jobob:x:503:`

参考之前关于密码文件和 shadow 文件格式的讨论，以理解这些文件中显示的字段的含义。注意，该账户已禁用（密码字段中的第一个 `!`），并且没有设置密码（如密码字段中的第二个 `!` 所示）。同时请记住，组文件中的条目代表为 `jobob` 创建的用户私有组。

![](img/d1fb1ff3244ecb66d002a5e633e6f729_622_0.png)

Red Hat 修改了标准的 `useradd` 命令以支持其 UPG（用户私有组）方案。

下一个命令使用了 `useradd` 的一些命令行选项来覆盖默认值：

```bash
# useradd -c "Mary Sue" -e 2001-09-30 -n f 3 -n marysue
```

`-c "Mary Sue"` 将账户 (GECOS) 字段设置为 Mary Sue；`-e 2001-09-30` 设置账户的过期日期；`-f 3` 在密码过期后三天（如果未更改）禁用账户，而 `n` 禁用 UPG 方案。以下是为 `/etc/passwd`、`/etc/shadow` 和 `/etc/group` 中的 `marysue` 创建的条目：

```bash
# grep marysue /etc/passwd /etc/shadow /etc/group
/etc/password:marysue:x:503:1000:Mary Sue:marysue::/bin/bash
/etc/shadow:marysue::11589:0:99999:7:3:11595:
```

首先，`/etc/group` 没有添加条目，因为 `n` 防止了 `marysue` 组的创建。相反，`useradd` 使用了默认 GID 100，它对应于 `users` 组。注意，添加到 `/etc/passwd` 的记录中出现了注释 Mary Sue，而不是像 `jobob` 那样的留空字段（由 `:` 所示）。最后，注意添加到 `/etc/shadow` 的条目略有不同，这反映了对账户过期信息的使用。

要设置或更改账户密码，请使用 `passwd` 命令。创建新账户后，您需要使用 `passwd` 设置账户密码，除非您使用 `useradd` 的 `-p` 选项指定了加密密码。`passwd` 的语法非常简单：

```bash
passwd [-l] [-u [-f]] [-d] [-S] [username]
```

`username` 表示要操作的用户账户。如果不指定，`passwd` 将对当前用户账户进行操作。`-l` 通过在 `/etc/shadow` 中的密码前加 `!` 来锁定用户账户；相反，`-u` 解锁用户账户。还要记住，如果账户密码仅为 `!`，即没有密码，则必须使用 `-f` 选项来启用账户。`-d` 通过删除密码来禁用账户，而 `-S` 显示账户状态（是否已锁定）。只有 `root` 用户才能使用这些选项。事实上，普通用户只能调用 `passwd` 更改自己的密码。只有 `root` 可以使用 `passwd` 的任何命令行选项。

# 第四部分：Red Hat Linux 系统维护

## 同时添加多个用户 (SIMANEOUSLY)

在忙碌的环境中，系统管理员经常发现有必要创建多个账户。使用 `useradd` 创建一两个账户相对简单，但如果需要创建十个或二十个就会变得繁琐。幸运的是，`password` 软件包包含了用于创建多个账户的实用。`username` 是要操作的账户名称。如果不指定，`passwd` 将对当前用户账户进行操作。`-l` 通过在 `/etc/shadow` 中的密码前加 `!` 来锁定用户账户；相反，`-u` 解锁用户账户。如果账户密码仅为 `!`，即没有密码，则必须使用 `-f` 选项来启用账户。`-d` 通过删除密码来禁用账户，而 `-S` 显示账户状态（是否已锁定）。只有 `root` 用户才能使用这些选项。事实上，普通用户只能调用 `passwd` 更改自己的密码。只有 `root` 可以使用 `passwd` 的任何命令行选项。以下命令显示了 `/etc/passwd`、`/etc/group` 和 `/etc/shadow` 中的用户条目：

```bash
# grep marysue /etc/passwd /etc/shadow /etc/group
/etc/password:marysue:x:503:1000:Mary Sue:marysue::/bin/bash
/etc/shadow:marysue::11589:0:99999:7:3:11595:
```

首先，`/etc/group` 没有添加条目，因为 `n` 防止了 `marysue` 组的创建。相反，`useradd` 使用了默认 GID 100，它对应于 `users` 组。注意，添加到 `/etc/passwd` 的记录中出现了注释 Mary Sue，而不是像 `jobob` 那样的留空字段（由 `:` 所示）。最后，注意添加到 `/etc/shadow` 的条目略有不同，这反映了账户过期信息的使用。以下命令显示了 `/etc/passwd`、`/etc/group` 和 `/etc/shadow` 中的用户条目：

```bash
# grep jobob /etc/passwd /etc/shadow /etc/group
/etc/password:jobob:x:503:503::/home/jobob:/bin/bash
```

`/etc/shadow:jobob::11589:0:99999:7:::`  
`/etc/group:jobob:x:503:`

参考之前关于密码文件和 shadow 文件格式的讨论，以理解这些文件中显示的字段的含义。注意，该账户已禁用（密码字段中的第一个 `!`），并且没有设置密码（如密码字段中的第二个 `!` 所示）。同时请记住，组文件中的条目代表为 `jobob` 创建的用户私有组。Red Hat 修改了标准的 `useradd` 命令以支持其 UPG 方案。下一个命令使用了 `useradd` 的一些命令行选项来覆盖默认值：

```bash
# useradd -c "Mary Sue" -e 2001-09-30 -n f 3 -n marysue
```

`-c "Mary Sue"` 将账户 (GECOS) 字段设置为 Mary Sue；`-e 2001-09-30` 设置账户的过期日期；`-f 3` 在密码过期后三天（如果未更改）禁用账户，而 `n` 禁用 UPG 方案。以下是为 `/etc/passwd,/etc/shadow` 和 `/etc/group` 中的 `marysue` 创建的条目：

```bash
# grep marysue /etc/passwd /etc/shadow /etc/group
/etc/password:marysue:x:503:1000:Mary Sue:marysue::/bin/bash
/etc/shadow:marysue::11589:0:99999:7:3:11595:
```

首先，`/etc/group` 没有添加条目，因为 `n` 防止了 `marysue` 组的创建。相反，`useradd` 使用了默认 GID 100，它对应于 `users` 组。注意，添加到 `/etc/passwd` 的记录中出现了注释 Mary Sue，而不是像 `jobob` 那样的留空字段（由 `:` 所示）。最后，注意添加到 `/etc/shadow` 的条目略有不同，这反映了账户过期信息的使用。

要设置或更改账户密码，请使用 `passwd` 命令。创建新账户后，您需要使用 `passwd` 设置账户密码，除非您使用 `useradd` 的 `-p` 选项指定了加密密码。`passwd` 的语法非常简单：

```bash
passwd [-l] [-u [-f]] [-d] [-S] [username]
```

`username` 表示要操作的用户账户。如果不指定，`passwd` 将对当前用户账户进行操作。`-l` 通过在 `/etc/shadow` 中的密码前加 `!` 来锁定用户账户；相反，`-u` 解锁用户账户。如果账户密码仅为 `!`，即没有密码，则必须使用 `-f` 选项来启用账户。`-d` 通过删除密码来禁用账户，而 `-S` 显示账户状态（是否已锁定）。只有 `root` 用户才能使用这些选项。事实上，普通用户只能调用 `passwd` 更改自己的密码。只有 `root` 可以使用 `passwd` 的任何命令行选项。

## 同时添加多个用户 (SIMANEOUSLY)

在忙碌的环境中，系统管理员经常发现有必要创建多个账户。使用 `useradd` 创建一两个账户相对简单，但如果需要创建十个或二十个就会变得繁琐。幸运的是，`password` 软件包包含了用于创建多个账户的实用。以下命令显示了 `/etc/passwd`、`/etc/group` 和 `/etc/shadow` 中的用户条目：

```bash
# grep marysue /etc/passwd /etc/shadow /etc/group
/etc/password:marysue:x:503:1000:Mary Sue:marysue::/bin/bash
```
