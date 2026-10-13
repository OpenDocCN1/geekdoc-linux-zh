
我们选择在 Samba 服务器上使用加密密码，以避免第 10 小时和第 11 小时描述的明文密码问题。这意味着我们需要一个可以在测试和示例中使用的账户。本小时的所有配置将假设本地 `/etc/passwd` 文件中存在以下用户，每个用户都有一个 `smbaspasswd` 条目。

```
jerry:x700:Gerald Carter:/home/gary:/bin/bash

sam:x701:Sam Samba:/home/sam:/bin/bash

krist:x702:Krist Carter:/home/kristi:/bin/bash
```

如果你需要提醒如何创建 `smbaspasswd` 文件并向其中添加用户，请参考上一个小时“安全级别与密码”中的示例。

在这些用户主组字段中组 ID `gid` 100 和 900 在 `/etc/group` 中定义如下：

```
users:x:100:

guest:x:900:
```

## 基础的、组可访问的共享

本小时的第一个文件共享将是一个旨在支持 Unix 组成员协作的基础型服务。这与第 4 小时使用的场景类似，当时我们构建并安装了第一个 Samba 服务器。虽然与之前小时的示例会有少量重复，但总体而言，我们将从第 4 小时结束的地方继续。

### Samba——服务器 117

我们从一个名为 `[24hrs]` 的简单共享开始，它允许“users”成员对该目录具有读写权限。为了在磁盘上设置此目录，我们将创建文件夹并将权限设置为：所有者（root）为 `rwx`，组组（users）为 `rwx`，其他人为 `---`。

```
root# mkdir /export/24hrs

root# chgrp users /export/24hrs

root# chmod 770 /export/24hrs
```

接下来，我们将服务定义添加到 `smb.conf`。

```
### 组文件共享

[24hrs]

  comment = STY-Samba 的基础组共享

  path = /export/24hrs

  browseable = yes

  read only = no
```

Samba 总是向用户授予最严格的权限集。根据 `/export/24hrs` 的权限，只有“users”组的成员才能访问该共享，即使服务定义允许任何经过验证的用户，如果 kristi 尝试连接 `\\ppo24hrs`，Windows 也会报告“找不到网络名称”或“找不到共享目录”。

表 8.1 是 `[24hrs]` 服务中使用的每个参数含义的快速提醒。如果未显式设置选项，则使用默认值。

| 名称 | 默认值 |  |
| :--- | :--- | :--- |
| browseable | yes | 服务是否应显示在服务器的枚举共享列表中？如果禁用，客户端必须知道共享的 UNC 路径才能建立连接。 |
| comment | ** | 定义在查看共享属性时显示的字符串。 |
| path | /export/24hrs | 指定共享的路径。 |
| read only | no | smbd 是否允许客户端向共享写入？ |

默认情况下，`smbd` 在查找 Windows 客户端请求的文件时会执行不区分大小写的搜索。这种行为可以通过设置大小敏感的 `smbd.conf` 选项来禁用。

```
case sensitive = yes
```

> 启用大小敏感参数可能会导致许多 Windows 应用程序崩溃。你通常不需要设置此选项。

# 最常见的三个大小写选项有

- preserve case（保留大小写）
- short preserve case（保留短文件名大小写）
- default case（默认大小写）

当 Windows 客户端在 Samba 文件共享上创建新文件或目录时，`smbd` 必须确定磁盘上的实际文件名应该是。前两个参数分别定义了对长文件名和 DOS 8.3 文件名执行什么操作。默认情况下，Samba 将始终保留文件名的大小写。如果禁用了其中一个设置，`smbd` 将将所有对应的文件名转换为默认大小写。表 8.3 总结了大小写设置及其默认设置。

8.3 文件名由一到八个大写字母组成，后面紧跟一个点，然后是一到三个作为文件扩展名的大写字母。例如：`DEFAULT.TXT`。

服务级参数可以放置在 `smbd.conf` 的 `[global]` 部分，以定义特定于配置的默认值。通过全局设置这些参数来指定默认大小写策略是一个良好的做法。这些是我在生产服务器上常用的设置。

```
[global]
...
```

## 为文件共享定义全局大小写策略

```
case sensitive = no

preserve case = yes

short preserve case = no

default case = lower
```

### Samba—文件服务器

### 表 8.3 Samba 的大小写参数
| 名称 | 默认值 | 描述 |
|---|---|---|
| case sensitive | no | smbd 是否应该执行不区分大小写的文件/目录查找？ |
| preserve case | yes | smbd 是否应该保留长文件名的大小写？ |
| short preserve case | yes | smbd 是否应该保留(8.3)文件名的大小写？ |
| default case | lower | 未保留大小写的文件应转换为什么种大小写（小写或大写）？ |

![](img/e6dc042fe420c610acdd193e834a4772_136_0.png)

许多用户仍然需要 16 位和基于 DOS 的应用程序。通常，这些程序无法处理长文件名。与 FAT 和 NTFS 不同，Unix 文件系统不会为普通的长文件名存储一个关联的 8.3 文件名。Samba 不会代表文件系统存储这些信息，而是根据需要生成这些文件名。表 8.4 列出了控制 `smbd` 如何生成此新字符串的几个参数。在 `[24hrs]` 服务中，我们对所有这些混淆参数使用默认值。

### 表 8.4 大小写混淆参数
| 名称 | 默认值 | 描述 |
|---|---|---|
| mangle case | yes | Samba 是否为不是默认大小写的文件名生成 (8.3) 名称？这是在系统中同时看到 Mail 和 mail 的唯一方法。 |
| mangled names | yes | Samba 是否应该生成 8.3 文件名？如果没有，具有长文件名的文件/目录将无法供 DOS 客户端使用。 |
| mangling char | - | 应该使用什么字符作为替换 8.3 混淆名的字符的替代？ |

# 受限制访问的服务

我们的下一个文件共享命名为 `[software]`，它是上一节中介绍的组共享的变体。最初，我们的文件定义看起来与 `[24hrs]` 共享非常相似。

```
## 用于分发特定应用程序的文件共享

[software]

comment = 运行 Foo.exe 的限制访问

path = /export/foo

read only = no
```

# 第 8 小节

然而，我们在这一节中对访问控制有不同的需求。该共享应该只允许 `jerry` 和 `kristi` 用户访问。我们的问题是这些账户不属于同一个组，因此用于 `[24hrs]` 共享的解决方案（将访问控制完全委托给文件系统）将无法作用。

相反，我们回到了第 4 小节中使用的解决方案。在那个示例中，`force group`（见表 8.5）参数让 `smbd` 以特定组执行所有文件访问，而不是以身份验证用户的主组。我们不再使用组账户进行访问，而是使用 `force user` 参数。

首先，我们将专门为此共享创建一个新的用户账户。

```
software:783:900:Samba account:/dev/null:/bin/false
```

接下来，我们将 `/export/foo` 中所有文件的所有权交给该账户。

```
root# chown -R software /export/foo
```

最后，我们将新的 `force user` 值添加到 `[software]` 定义中。

```
[software]

comment = 运行 Foo.exe 的限制访问共享

path = /export/foo

read only = no

force user = software
```
