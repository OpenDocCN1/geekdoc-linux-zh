
如你所示，通过这种方式创建非常复杂的登录脚本非常容易。

## 映射主驱动器

主驱动器映射是一个非常简单的过程。使用以下命令完成主驱动器映射，这些命令应放置在 `[global]` 部分中：
`logon home = \\%u drive = h:`

`logon home` 参数指定了用户特定目录的位置。因为 `%l` 扩展为 PDC 的名称，而 `%u` 指定为用户名，这将使用用户的主目录映射到与 PDC 上用户名匹配的共享——这完美匹配了 `[homes]` 部分。第二个选项实际上是在登录时将主共享映射到驱动器器号，以便用户更容易访问其数据。

## 映射组和用户

Samba 面临的挑战之一是将其两个安全系统集成到一体的能力——特别是 UNIX 密码和 Windows 数据库。Windows NT 的安全系统有许多用户可以所属的默认组。属于这些组定义了特定用户在系统上的权限。显然，Windows NT 有域用户管理器来管理此类关系，但 Samba 究竟是如何做到的？当然，Samba 使用 `smpasswd` 文件，但 `smpasswd` 只存储用户和机器帐户，不存储组信息。

Samba 通过两个新的全局选项定义 NT 组：`domain group map`（组映射）和 `local group map`（本地组映射）。在深入细节之前，重要的是你充分了解这些选项的作用。首先，`domain group map` 提供了一种方法，当用户位于指定的 UNIX 组时，Samba 会通过该方法将 UNIX 组与 Windows NT 域组关联起来。这为你通过使用 `/etc/group` 文件将用户添加到 NT 域组提供了一种简单、方便的方法。

以下是 `domain group map` 的工作原理。放在 `[global]` 部分的 `domain group` 指向一个组映射文件，如下：
`domain group map = /usr/local/samba/domaingroup.map`

> 注意
`domaingroup.map`、`localgroup.map` 和 `domainuser.map` 文件必须对所有用户可读！通过输入以下两个命令使其可读：
`chmod u+r domaingroup.map`
`chmod u+r localgroup.map`

此文件应包含以下格式的映射信息：

`UNgroup = NTgroup`

为了让 `domain group map` 正常工作，指定的 UNIX 组必须存在。重启 Samba 后，你可以通过将用户添加到相应的 UNIX 组，将其添加到特定的 Windows NT 组。这通过编辑 `/etc/group` 轻松实现。

关于使用 `domain group map` 选项的注意事项是，如果你想将 UNIX 用户添加到 NT 组，则 `domaingroup.map` 文件中的拼写必须完全匹配。在 `domaingroup.map` 文件中，拼写必须与匹配。以下是示例的 `domaingroup.map` 文件，定义了所有标准 NT 组：

- `admin` = "Domain Admins"
- `guest` = "Domain Guests"
- `user` = "Domain Users"
- `power` = "Power Users"
- `account` = "Account Operators"
- `system` = "System Operators"
- `print` = "Print Operators"
- `backup` = "Backup Operators"
- `replic` = "Replicators"

使用 `domain group map` 选项的一个注意事项是，如果你想将 UNIX 用户添加到 NT 组，则 `domaingroup.map` 文件中的拼写必须完全匹配。在 `domaingroup.map` 文件中，拼写必须完全匹配。

要使用这一点，只需在 `smb.conf` 的全局部分添加以下行：
`domain group map = /usr/local/samba/domaingroup.map`

在将这些数据添加到 `domaingroup.map` 文件后，创建之前列出的组（`admin`、`guest`、`user`），重启 Samba，并编辑 `/etc/group` 将你想要的用户添加到这些组。Samba 然后会将这些人视为相应 NT 组的成员。

`local group map` 选项的工作原理几乎相同，只是它指向一个将 UNIX 组映射到本地组的文件。这里的 `localgroup.map` 文件定义了所有标准 NT 组：

- `admin` = "Administrators"
- `user` = "Users"
- `guest` = "Guests"
- `power` = "Power Users"
- `account` = "Account Operators"
- `system` = "System Operators"
- `print` = "Print Operators"
- `backup` = "Backup Operators"
- `replic` = "Replicators"

在将这些数据添加到 `localgroup.map` 文件后，在 `smb.conf` 全局部分添加以下内容：
`local group map = /usr/local/samba/localgroup.map`

现在不仅你有 NT 用户，还有 NT 组！此外，Microsoft 服务器现在更容易与你的安全数据库协作。

一个额外的选项也有助于此。当然，Windows NT 和 UNIX 在使用用户名方面存在不同之处。假设你希望在 Samba 数据库中拥有这些长用户名。你可以通过 `domain user map` 选项来实现。它的指定方式与其他两个选项类似：

```
domain user map = /usr/local/samba/domainuser.map
```

此外，`domainuser.map` 文件的格式也相似：

```
UNIXUser = NTUser
```

在你设置之后，任何指定的 UNIX 用户在 NT 中都被视为相应的 NT 用户。你可能在想哪个帐户应该添加到 `smpasswd` 文件。好问题！只需添加 UNIX 用户，Samba 将自动执行转换。这样，你就不需要在 `/etc/password` 中为 NT 用户创建 UNIX 用户帐户，这正是你想要避免的。

## 漫游和配置文件

实现漫游配置文件并不困难。第一步是在你的 `smb.conf` 中添加以下信息：

```
[global]

logon path = \%Lprofiles\%U..[profiles]

  comment = user profiles

  path = /usr/local/samba/profiles

  create mode = 0600

  directory mode = 0700

  force group = %G

  force user = %U

  writeable = yes

  browseable = yes
```

通过向 Samba 添加这些信息，你现在有一个名为 `profiles` 的共享。确保你的配置文件目录允许完全访问，对所有用户开启读、写、执行权限：

```
chmod 1777 /usr/local/samba/profiles
```
