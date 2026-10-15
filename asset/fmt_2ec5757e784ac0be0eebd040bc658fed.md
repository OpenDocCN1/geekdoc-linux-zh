
| i | inherit_only | 传播，但不应用于当前目录 |

| n | no_propagate | 传播到新子目录，但不传播到其子目录 |

### Solaris 中的 NFSv4 ACL 查看

![](img/14d78e3cecac4581d37024baf1e94cca_217_0.png)

Solaris 已将其实 ACL 支持集成到 `ls` 和 `chmod` 中，这是一种不错的方法，也是对命令通常功能的直接扩展。POSIX 和 NFSv4 ACL 均以这种方式得到支持，尽管这里仅显示 NFSv4 示例。你看到或设置的 ACL 的具体类型取决于底层文件系统。

`ls -v` 显示文件系统对象的 ACL 信息。与 `-l` 一样，如果你想查看目录的 ACL，必须包含 `-d` 选项；否则 `ls -v` 会显示目录每个子项的 ACL。以下是一个简单的 (!) 示例：

```
solaris# mkdir /var/tmp/example
solaris# ls -dv /var/tmp/example
drwxr-xr-x 2 garth staff 2 jan 11 07:19 /var/tmp/example
0:owner@:deny
1:owner@:list_directory/read_data/add_file/write_data/add_subdirectory/append_data/write_xattr/execute/write_attributes/write_acl/write_owner:allow
2:group@:add_file/write_data/add_subdirectory/append_data:deny
3:group@:list_directory/read_data/execute:allow
4:everyone@:add_file/write_data/add_subdirectory/append_data/write_xattr/write_attributes/write_acl/write_owner:deny
5:everyone@:list_directory/read_data/read_xattr/execute/read_attributes/read_acl/synchronize:allow
```

这个新创建的目录似乎具有复杂的 ACL，但实际上它是假的——此 ACL 只是将第一行输出中显示的九位模式翻译成 ACLEse。它不需要文件系统存储实际的 ACL，因为 ACL 和模式是等效的。（此类 ACL 被称为“平凡的”。）如果目录具有实际的 ACL，`ls` 会在模式位末尾显示一个 `+`（即 `drwxr-xr-x+`）以指示 ACL 的存在。

每个编号的条款代表一个访问控制条目。格式为

`index:entity:permissions:inheritance_flags:type`

索引号由 `ls` 添加以提高清晰度，并不是实际 ACL 的一部分。它们可以在后面的 `chmod` 命令中用于标识要替换或删除的特定 ACE。

实体可以是关键字 `owner@`、`group@` 或 `everyone@`，或 `user:username` 或 `group:groupname` 这样的形式。

ACE 的类型为 `allow` 或 `deny`。理论上，`alarm` 和 `audit` 也是允许的，但 ZFS 并未实现这些功能。

权限和 `inheritance_flags` 都是以斜杠分隔的选项列表。奇怪的是，如果标志全部关闭，`ls` 会省略 `inheritance_flags` 字段（以及其中一个冒号分隔符），但它不会对权限做同样的处理。

为增加混乱，`ls` 对 `r`（读取数据/列出目录）、`w`（写入数据/添加文件）和 `p`（追加数据/添加子目录）权限位显示多个名称，仿佛它们是单独的权限。事实上，它们是同一位的文件和目录特定解释，并且会始终一起存在或一起缺失。

## 6.7 练习

**E6.1** 什么是 `umask`？创建一个 `umask`，使其对组或其他用户没有任何权限。

**E6.2** 硬链接和符号（软）链接有什么区别？

在什么情况下适合使用其中一种？

☆ **E6.3** 在你的系统上，要使 Windows NTFS 分区从本地硬盘自动挂载，需要哪些步骤？根据你系统的约定和你所在站点的约定，这种分区最合适的挂载点是什么？

☆ **E6.4** 在安装新系统时，重要的是设置系统卷，使每个文件系统（`/var`、`/usr` 等）都有足够的空间满足当前和未来的需求。Foobar Linux 发行版使用以下默认值：

| Filesystem | Size |
|---|---:|
| `/` | 2GB |
| `/var` | 100MB |
| `/boot` | 100MB |
| `<swap>` | 2GB |
| `/usr` | remaining space |

在繁忙的服务器上，这种安排会有什么潜在问题？

☆ **E6.5** 为什么将某些分区（例如 `/var`、`/home` 和 swap）放在与其它数据文件和程序不同的驱动器上是个好主意？`/tmp` 呢？请针对列出的每个文件系统给出具体原因。

☆ **E6.6** 编写一个脚本来查找文件系统上的所有硬链接。

☆ **E6.7** 给出完成以下任务的命令。

- a) 将文件 **README** 的权限设置为所有者可读/写，其他人只读。
- b) 在不更改（或不知道）当前权限的情况下打开文件 setuid 位。
- c) 列出当前目录的内容，按修改时间排序，并将最近修改的文件排在最后。
- d) 将名为 **shared** 的文件组从“user”更改为“friends”。

☆ **E6.8** 按惯例，`/tmp` 目录对所有想要在那里创建文件的用户开放。什么可以防止一个用户读取或删除另一个用户的临时文件？什么可以防止一个不满的用户用垃圾文件填满 `/tmp`？这种攻击会有什么后果？

# 7 添加新用户

![](img/14d78e3cecac4581d37024baf1e94cca_222_0.png)

在大多数系统上，添加和删除用户是例行工作。这些任务很简单，但也很无聊；大多数管理员会调整操作系统提供的工具以自动化该过程，然后将实际工作委托给助手或操作员。

如今，我们看到集中式服务器的复兴，这些服务器为数百人提供登录账户，同时还有只有两个用户的分布式服务器。管理员需要透彻理解用户账户系统，以便管理网络服务并为本地计算环境适当配置账户。通常，服务器上的账户管理只是整个企业账户配置难题中的一个环节。

当今的企业环境需要的不仅仅是向特定机器添加用户的工具，还需要一个在整个计算环境中管理用户及其众多账户和密码的工具——即身份管理系统。Microsoft 的 Active Directory、OpenLDAP 和 Fedora Directory Server 等目录服务被广泛使用，因此我们将详细介绍这些系统如何影响账户管理任务。 （通常情况下，目光短浅的 Microsoft 除非让 Active Directory 主导，否则与其他系统配合不好。唉。）

一些站点的需求可能超过了即使这些系统的能力。我们不介绍商业身份管理系统，但会指出一些候选产品。它们可能是非常大站点的正确解决方案，尤其是在需要遵守 HIPAA 或萨班斯-奥克斯利法案（在美国）等监管制度的情况下。参见第 203 页。

账户卫生是系统安全的重要决定因素。很少使用的账户以及密码容易猜到的账户都是攻击者的主要目标。即使你使用系统的自动化工具来添加和删除用户，了解工具所做的更改也很重要。因此，我们从必须修改以向单台机器添加用户的平面文件开始讨论账户管理。

然后我们检查随每个示例操作系统分发的自动化工具以及控制其行为的配置文件。令人惊讶的是（或令人困惑的是），用户管理工具在我们的每个示例系统上都称为 `useradd`、`userdel` 和 `usermod`，即使程序不一定相同。 （此外，AIX 通过用驱动脚本包装其原生的 `mkuser`、`rmuser` 和 `chuser` 工具来实现这种命名一致性。）

默认的 `useradd` 工具实际上相当不错，对于大多数站点的需求来说已经足够了。不幸的是，`userdel` 并不是总像我们希望的那样彻底。

大多数系统还具有用于添加和删除用户的简单 GUI 工具，尽管这些工具通常不实现批处理模式或高级本地化。它们足够简单，我们认为详细回顾其操作没有帮助，但我们会为每个工具指向供应商的文档。

在本章中，我们专门关注添加和删除用户。许多与用户管理相关的话题实际上存在于其他章节中，在这里仅作引用。例如，

- 用于密码加密和强制执行强密码的可插拔认证模块（PAM）涵盖在第 22 章 *Security* 中。参见第 908 页的材料。
- 用于管理密码的密码库在第 4 章 *Access Control and Rootly Powers* 中描述（参见第 117 页）。
