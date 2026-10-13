
### 示例

尽管本章大部分内容是概念性的，但下面的示例展示了如何实际使用 RBAC。对于你想要创建的每个角色，都应该制定一个规划表，然后按照所需的步骤在系统上配置并激活该角色。通过预规划角色，可以创建脚本来实现跨多个不同服务器的自动化。这里是一个规划条目的示例：

| 角色 | 目的/描述 | 分配的用户 | 使用的命令 |
|---|---|---|---|
| 用户管理 | 向系统添加用户 | paul, nalneesh | useradd, usermod, userdel, pwck |
| Web 维护 | 允许操作 Web 服务器 | paul, jane, jessica | httpd, apachectl |

- 一旦你确定了角色、用户和命令，接下来的三个步骤需要是：
1. 使用 `smrole` 命令创建每个角色。
2. 使用 `smrofile` 创建每个配置文件（profile）。
3. 使用 `smrole` 将每个用户分配给角色。
4. 验证文件中的更改。

### 命令参考

以下参考提供了与 RBAC 使用的不同命令的详细信息。

# smexec

`smexec` 命令用于在 `exec_attr` 数据库中创建、更新和删除行。执行命令时必须传递三个选项之一：`add`（添加条目）、`delete`（删除条目）或 `modify`（修改，更新条目）。要使用 `smexec`，用户必须拥有 `solaris.prof.execattr.write` 权限。有组参数可以传递给 `smexec`（取决于选择了哪种选项）：授权参数和每个选项的特定参数。

授权参数对每个选项都是通用的，它们指定了以下特征：

| - | - |
|---|---|
| `-domain` | 要管理的域 |
| `-hostname:port` | 执行操作的主机名和端口（默认端口为 898） |
| `-rolepassword` | 角色认证的密码 |
| `-password` | 用户密码而非角色的密码 |
| `-rolename` | 角色的名称 |
| `-username` | 用户的名称 |

使用 `smexec add` 添加条目时，可以在命令行上传递以下参数：

| - |  |
|---|---|
| `-c` | 指定要添加的新命令名称的完整路径 |
| `-g` | 指定执行新命令的有效 GID |
| `-G` | 指定执行新命令的实际 GID |
| `-n` | 指定命令关联的配置文件名称 |
| `-t cmd` | 指定该操作为命令 |
| `-u` | 指定执行新命令的有效 UID |
| `-U` | 指定执行新命令的实际 UID |

`smexec add` 操作的示例如下：

```
smexec -hostname localhost -password xyz123 -username root -n "Print Manager" -t cmd -c /usr/sbin/lpsched -u 0 -g 0
```

此条目为“Print Manager”角色添加了启动打印服务的权限，其有效 UID 和 GID 为 0 (root)。

使用 `smexec delete` 条目时，可以在命令行上传递以下参数：

| - |  |
|---|---|
| `-c` | 指定要删除的命令名称的完整路径 |
| `-n` | 指定命令当前关联的配置文件名称 |
| `-t cmd` | 指定该操作为命令 |

要删除 `lpsched` 的条目，你需要使用以下命令：

```
smexec delete -hostname localhost xyz123 -username root -n "Print Manager" -t cmd -c /usr/sbin/lpsched
```

使用 `smexec modify` 修改条目时，可以在命令行上传递以下参数：

| - |  |
|---|---|
| `-c` | 指定要修改的命令名称的完整路径 |
| `-g` | 指定执行新命令的修改后的有效 GID |
| `-G` | 指定执行新命令的实际 GID |
| `-n` | 指定命令关联的修改后的配置文件名称 |
| `-t cmd` | 指定该操作为命令 |
| `-u` | 指定执行新命令的修改后的有效 UID |
| `-U` | 指定执行新命令的修改后的实际 UID |

`smexec modify` 操作的示例如下：

```
smexec modify -hostname localhost -password xyz123 -username root -n "Print Manager" -t cmd -c /usr/some/new/path/lpsched -u 0 -g 0
```

此条目修改了为“Print Manager”配置文件启动运行服务的命令，其路径从 `/usr/sbin/lpsched` 修改为 `/usr/some/new/path/lpsched`。

# smultiprouser

`smultiprouser` 命令用于执行批量函数，例如添加或删除大量用户。当已存在一个指定所有所需数据的文件时，这特别有用。例如，备份系统可能需要一个与当前生产系统类似的设置。与其直接复制文件系统，可以执行与新创建相关的所有操作（如创建家目录）。此外还可以更新指定用户的文件。

使用 `smultiprouser` 进行 `add`、`delete` 和 `modify` 操作时，可以在命令行上传递以下参数：

| - |  |
|---|---|
| `-I` | 指定要读取的输入文件，其中包含所有要添加、修改或删除的条目的数据 |
| `-L` | 指定日志文件名，记录单个操作是成功还是失败 |

在下面的示例中，从 `/home/paul/newaccounts.txt` 读取了一组记录并将其添加到系统：

```
smultiprouser -hostname localhost -password xyz123 -username root -I /home/paul/newaccounts.txt
```

# smuser

`smuser` 命令用于对用户账户进行操作，数据从本地数据库或 NIS/NIS+ 获取。尽管与 `smultiprouser`，但它通常只用于添加单个用户而不是批量用户。除了添加、删除和修改用户记录外，还可以检索现有的用户数据。执行命令时必须传递四个选项之一：`add`（添加条目）、`delete`（删除条目）、`list`（列出所有现有条目）或 `modify`（更新条目）。要使用 `smuser add`、`delete` 或 `modify`，用户必须拥有 `solaris.prof.mngr.ecatt.write` 权限。然而，列出条目需要 `solaris.domain.username.write` 权限。有两组参数传递给 `smuser`（取决于选择了哪种选项）：授权参数和每个选项的特定参数。授权参数对每个选项都是通用的，并指定了以下特征：

| - |  |
|---|---|
| `-domain` | 要管理的域。可以是本地数据库 (`file`)、`NIS` (`nis`)、`NIS+` (`nisplus`)、`DNS` (`dns`) 或 `LDAP` (`ldap`)。要使用 LDAP 管理 `foxtrot.cassuary.net`，你指定的域为 `ldap://foxtrot/cassuary.net`。 |
| `-hostname:port` | 执行操作的主机名和端口。默认端口为 898。 |
| `-password` | 用户密码而非角色的密码 |
| `-rolename` | 角色的名称 |
| `-rolepassword` | 角色认证的密码 |
| `-username` | 用户的名称 |

使用 `smuser add` 添加条目时，参数与第12章中介绍的使用 `useradd` 添加用户的参数相似。可以在命令行上传递以下参数：

| - | - | - |
| - | - | - |
| `-c` | 指定账户描述，例如“Joe Bloggs” |
| `-d` | 指定用户的家目录 |
| `-e` | 指定账户的过期日期 |
| `-f` | 指定账户在过期前非活动天数的限制 |
| `-F` | 为账户指定全名，该名称不能被域内的其他账户使用 |
| `-g` | 指定账户 QID |
| `-n` | 指定账户名 |
| `-P` | 指定账户密码 |
| `-s` | 指定默认 shell |
| `-u` | 指定账户 UID |

此处显示了一个 `smuser add` 命令的示例：

```
# smuser add -H localhost -p xyz123 -u root -F "Paul Watters" walrus -c "Paul A Watters Director" -P jimmy123 -g 10 -u 1025
```

该命令为 Paul Watters 在系统中添加了一个名为 `walrus` 的账户，密码为 `jimmy123`。该账户的 UID 为 1025，GID 为 10。

使用 `smuser delete` 删除条目时，仅需在命令行传递指定账户名的 `-n` 参数。以下命令将删除 `localhost` 上的 `walrus` 账户：

```
# smuser delete -H localhost -p xyz123 -u root -- -n walrus
```

使用如下命令时，`smuser list` 命令可以在不带任何参数的情况下显示用户列表：
```
