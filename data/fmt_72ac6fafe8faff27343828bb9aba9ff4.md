
按照 `smb.conf` 的习惯，“@”指定的是组而不是用户。用户 `root` 以及组 `operator` 和 `techos` 获得写入权限，而 `matt`、`john` 和组 `mgmt` 获得只读权限。注意，由于 `matt` 同时出现在了 `write list` 和 `read list` 中，`matt` 实际上具有写入权限。

## valid users, invalid users

这些参数非常直观：`valid users` 允许你定义可以访问的用户或组，`invalid users` 允许你指定不允许访问。注意，如果你设置了 `valid users`，不在列表中的都会被拒绝。同样，如果你设置了 `invalid users`，所有指定的用户都是允许的。

## force group, force user

强制参数允许你强制连接到特定共享变为特定的组和用户。从 Samba 2.0.5 版本开始，如果 `force group` 参数前面带有“+”，且用户已经是该组的成员，则该组被强制作为用户在此会话中的主组。所有其他用户保留原始的主组。

注意，使用 `force user` 时，用户仍然需要指定有效的用户名和密码来连接资源。只是连接后，所有操作都将以 `force user` 指定用户的身份执行（可以是另一个用户）。这些强制选项可以用于并非所有用户都有 UNIX 账户且有一个可用共享的环境。在这种情况下，如果你在 `smb.conf` 中放入以下内容，你可能会创建一个 `install` 账户：

```
[install]
comment = "此共享用于软件安装"
path = /pc/install
read-only = yes
force user = install
```

那么，无论是谁连接，到 `install` 资源的连接都将由 `install` 用户执行。

## 与共享相关的参数

这些参数会更改定义所在特定共享的某些属性。涵盖的参数包括：`max connections`（最大连接数），指定允许同时连接的用户数；`volume`（卷），允许为共享返回一个卷名称；`locking`（锁定），控制 Samba 是否授予客户端请求的锁；`copy`（复制），允许你实现模板共享并进行无限次复制；以及最后是 `blocking locks`（阻塞锁），控制 Samba 是否允许对文件的部分而非整个文件进行锁定。

## max connections

`max connections` 参数允许你指定（并因此限制）到服务器的最大同时连接数。它的默认值为 0，意味着允许对服务进行无限次连接。当你对网络上提供的某个特定软件软件包有特定数量的许可时，这可能非常有用。当设置了 `max connections` 时，将使用锁文件来计算共享会话的数量，这些锁文件的位置在 `lock directory` 参数中指定。默认值为 `/tmp/samba`。

## volume

`volume` 参数允许你指定共享返回的卷标签。当你在 Windows 下查看驱动器属性时，会显示此标签，如图 10.1 所示。

图 10.1

Windows NT 返回的卷标签。

![](img/55bb92df8f8bd2a90a13c9a131fa64c0_200_0.png)

某些来自光盘的安装程序需要特定的卷标签，否则将无法运行，因此在这种情况下特别有用。

## locking

不同的连接客户端可以对某些文件指定锁定请求。此参数控制 Samba 是否实际执行这些锁定请求。默认情况下，`locking` 设置为 `yes`。如果将其设置为 `no`，锁定和解锁请求对客户端将显示为成功，但实际上并没有执行。只有当你遇到你认为可能是由锁定引起的特定问题时，你才可能需要更改此参数。

## copy

`copy` 参数非常有用。它允许此服务成为另一个服务的副本。当你为了向下兼容而为一个共享使用不同的名称时，通常会使用此参数。它也可以用于创建模板服务，以简化创建相似的服务。示例如下：

```
[templ1_mktg]
comment = 'share used for marketing dept'
create mask = 0770
guest ok = no

[usa_mktg]
copy = templ1_mktg
path = /groups/usa/marketing
```

这将把 `templ_mktg` 服务中指定的所有参数复制到 `usa_mktg` 服务。你可以在新服务中放入任何喜欢的其他参数——它们会覆盖模板服务的参数。在之前的示例中，`usa_mktg` 实际上看起来如下：

```
[usa_mktg]
comment = 'share used for marketing dept'
create mask = 0770
guest ok = no
copy = templ1_mktg
path = /groups/usa/marketing
```

能够这样做对管理非常有帮助，特别是当你有很多设置了相似选项且被复制的共享时。

## blocking locks

SMB 客户端可以对打开文件的某个区域指定字节范围锁。该请求带有时间过期限制，如果无法立即授予锁，它将进入队列并持续尝试，直到时间过期。在 Samba 2.x 系列中，此设置默认认为 `true`。如果将其设置为 `false`，Samba 将立即失败锁定请求，忽略请求的过期参数。如果你有损坏的客户端应用程序以错误的方式请求此锁，你可能需要这样做——这会导致你可能认为是由于 Samba 引起的明显延迟。现在很少使用此参数了，因为大多数应用程序的行为都是正确的。

## 影响共享资源中文件的参数

下一组参数影响文件在共享中如何显示给用户使用。涵盖的参数包括：`delete readonly`（删除只读），允许连接用户覆盖文件的只读位以允许删除文件；`dont descend`（不向下进入），导致某些目录显示为空；`hide files`（隐藏文件）和 `hide dot files`（隐藏点文件），在共享中从视图隐藏某些文件，尽管它们仍然可见；以及 `veto`（否决），使某些文件无法访问。

### delete readonly

此参数允许删除只读文件。你通常需要设置此项。它的默认值为 `no`。如果你有一个特定的目录树，其所有文件都设置了只读参数，而该共享的管理员（不熟悉 UNIX）使用另一个共享进行管理但指向了设置了该参数的地方，你可能会发现它有用。这允许管理员删除可能不再需要的文件。

### dont descend

`dont descend` 参数允许你指定一个逗号分隔的目录列表，Samba 将其显示为空。如果你在共享下的某些目录路径不希望让 SMB 客户端访问，这将非常有用。UNIX 系统上还有诸如 `/proc` 和 `/dev` 等区域，对于用户进入是没有意义的。示例如下：

```
dont descend = /proc, /dev, /stand
```

### hide files, hide dot files

第一个隐藏参数 `hide files` 指定了仍然可以访问但在该共享中从视图中隐藏的文件。这些文件用“-”分隔，并可能包含空格以及 `*` 和 `?` DOS 通配符。`hide dot files` 隐藏所有以点开头的的文件。默认情况下，`hide dot files` 设置为 `yes`。

### veto files, delete files, oplocks

`veto files` 选项简单地隐藏文件，但它不是隐藏文件而是让它们无法访问。如果这是你想要的，将 `delete files` 设置为 `true`。

## Samba 进阶指南

在本章中，你学习了一些有趣且不寻常的 `samba.conf` 参数，你可以在文件服务中使用它们来实现特定的效果。

本章从讨论 `preexec` 和 `postexec` 参数开始。这些选项允许在客户端连接和断开共享时执行 UNIX 命令或脚本。

下一节介绍了名称转换（name mangling）过程，并展示了它如何允许 DOS 和 Windows 3.1 客户端访问 UNIX 文件名。你还学习了可能需要调整系统性能的选项。

接下来讨论了影响共享的选项，例如添加卷标签（`volume`）或限制同时连接数（`max connections`）。

最后，你学习了适用于共享文件的选项。你学习了某些隐藏文件但保持可访问的选项（`hide files`），以及其他使其无法访问的选项（`veto files`）。

1. 你想让 UNIX 系统上的文件共享映射到光盘。你挂载光盘的目录是 `/mnt`。你在 `samba.conf` 文件中添加什么文件共享部分？

2. 什么是“名称转换”（name mangling）？

3. 如何在 SMB 客户端查看的文件共享中隐藏但仍允许访问所有以“-”和“$”开头的 UNIX 文件名？

4. 图设计部门使用的软件存储在运行 Samba 的 UNIX 上。用户连接到共享以访问该软件。软件许可规定允许四个并发用户使用。你如何遵守许可要求？
