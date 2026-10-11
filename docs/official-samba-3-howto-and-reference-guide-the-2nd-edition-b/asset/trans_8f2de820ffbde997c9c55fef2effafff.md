
# 组映射：MS WINDOWS 和 UNIX

从 Samba-3 开始，新增了组映射功能，用于创建 Windows 组 SID 与 UNIX 组之间的关联。`net` 工具中包含的 `groupmap` 子命令可用于管理这些关联。

将 NT 组映射到 UNIX 系统组的新功能允许管理员决定哪些 NT 域组应暴露给 MS Windows 客户端。只有映射到具有非默认值（-1）的 UNIX 组的 NT 组才会暴露在给域用户和组提供访问权限的工具中的组选择列表中。

> **警告**
> 域管理组参数已在 Samba-3 中被移除，因此不应再在 smb.conf 中指定该参数。在 Samba-2.2.x 中，此参数用于赋予列出的用户成为 Windows“域管理员”组成员的权限，这给予了他们在其工作站上的本地管理员权限（在默认配置下）。

## 11.1 功能与优势

Samba 允许管理员创建 MS Windows NT4/200x 组账户，并将其任意与 UNIX/Linux 组账户关联。

可以使用 MS Windows NT4 或 MS Windows 200x/XP Professional MMC 工具管理组账户。如果希望在使用这些工具时自动创建 UNIX/Linux 系统账户，则应在 smb.conf 中提供适当的接口脚本。如果缺少这些脚本，且 winbindd 正在运行，则通过这些工具创建的 Samba 组账户将从 *smb.conf* 文件中由 *idmap uid*/*idmap gid* 参数指定的 ID 范围中分配 UNIX UID 和 GID。

**图 11.1 IDMAP：组 SID 到 GID 的解析。**

![](img/86d74c6cc862465e3a42e6dc3c90935a_235_0.png)

在这两种情况下，当 winbindd 未运行时，只能识别本地可解析的组。请参阅图 11.1 和图 11.2。**net groupmap** 用于建立 UNIX 组到 NT SID 的映射，如图 11.3 所示。

管理员应注意，当 *smb.conf* 组接口脚本直接调用 UNIX/Linux 系统工具（如 *shadow* 实用程序、*groupadd*、*groupdel*、*groupmod*）时，生成的 UNIX/Linux 组名将受到这些工具施加的任何限制。如果工具不允许使用大写字母或空格字符，则尝试创建名为 *Engineering Managers* 的 MS Windows NT4/200x 风格组将试图创建一个同名 UNIX/Linux 组，而这一尝试当然会失败。

对于操作系统工具的限制，有几种可能的变通方法。一种方法是使用生成符合操作系统限制的 UNIX/Linux 系统组名称的脚本，然后仅将 UNIX/Linux 组 ID（GID）返回给调用 Samba 接口。这将提供动态的变通解决方案。

另一种变通方法是手动创建 UNIX/Linux 组，然后在 Samba 服务器上手动创建 MS Windows NT4/200x 组，并使用 **net groupmap** 工具将两者连接起来。

![](img/86d74c6cc862465e3a42e6dc3c90935a_236_0.png)

![](img/86d74c6cc862465e3a42e6dc3c90935a_236_1.png)

## 11.2 讨论

当您在计算机上安装 MS Windows NT4/200x 时，安装程序会创建默认的用户和组，特别是 Administrators 组，并赋予该组执行基本系统任务所需的权限，例如更改日期和时间或终止（或关闭）本地机器上运行的任何进程。

Administrator 用户是 Administrators 组的成员，因此继承 Administrators 组的权限。如果创建一个名为 joe 的用户并成为 Administrators 组的成员，joe 将与用户 Administrator 拥有完全相同的权限。

当 MS Windows NT4/200x/XP 机器成为域成员时，PDC 的“Domain Admins”组会被添加到工作站的本地 Administrators 组中。Domain Admins 组的每个成员在登录到工作站时都会继承本地 Administrators 组的权限。

以下步骤说明了如何使 Samba PDC 用户成为 Domain Admins 组的成员。

1. 创建一个 UNIX 组（通常在 /etc/group 中）；我们称之为 domadm。
2. 将必须成为“管理员”的用户添加到该组中。例如，如果您希望 joe、john 和 mary 成为管理员，您在 /etc/group 中的条目将如下所示：
```
domadm:x:502:joe,john,mary
```
3. 通过运行以下命令将此 domadm 组映射到“Domain Admins”组：
```
root# net groupmap add ngroup="Domain Admins" unixgroup=domadm
```

由于组名中包含空格，“Domain Admins”周围的引号是必要的。此外，请确保等号（=）周围没有空白。现在，joe、john 和 mary 就是域管理员。

也可以将任何任意 UNIX 组映射到任何 Windows NT4/200x 组，并使任何 UNIX 组成为 Windows 域组。例如，如果您希望将某个 UNIX 组（例如 acct）包含在域成员机器上本地文件或打印机的 ACL 中，您需要在 Samba PDC 上运行以下命令将该组标记为域组：

```
root# net groupmap add rid=1000 ngroup="Accounting" unixgroup=acct
```

如果 ngroup 值包含空格字符，必须使用引号，以防止空格被解释为命令分隔符。

请注意，RID 参数是一个无符号 32 位整数，通常应从 1000 开始。然而，此 RID 不得与分配给用户的任何 RID 重叠。验证方式取决于您使用的 passdb 后端。未来版本的工具可能会自动执行验证，但目前责任在于您。

### 11.2.1 警告：用户私有组问题

Windows 不允许用户和组账户具有相同的名称。这对使用私有组账户的所有站点都有严重的影响。私有组账户是一种管理实践，即每个用户都拥有自己的组账户。Red Hat Linux 以及几个免费的 Linux 发行版默认创建私有组。

在将 UNIX/Linux 组映射到 Windows 组账户时，通过确保 Windows 域组名称不与任何用户账户名称重叠，可以避免所有冲突。

### 11.2.2 嵌套组：将 Windows 域组添加到 Windows 本地组

此功能称为嵌套组，首次添加于 Samba-3.0.3。

自 Windows NT 3.10 发布以来，所有 MS Windows 产品都支持嵌套组的使用。许多 Windows 网络管理员依赖此功能，因为它大大简化了安全管理。

嵌套组架构的设计前提是，日常用户和组成员管理应在域控制器数据库上进行。组安全的实施应在域成员服务器上使用本地组来实现。在域成员服务器上，所有文件系统安全控制都限制为使用本地组，这些本地组将包含域全局组和域全局用户。

你可能会问，这种安排有什么好处？对于深入研究过 Windows 网络架构深层奥秘的人来说，答案是很明显的。试想一下，一台服务器上存储着 200,000 个文件，每个文件都有独立的域用户和域组设置。拥有该文件服务器的公司被另一家公司收购，导致服务器被移动到另一个位置，然后被添加为另一个域的成员。你认为谁现在拥有所有文件和目录？答案是：Account Unknown（未知账户）。

解开文件所有权的混乱是一项艰巨的管理任务，只需使用本地组来控制所有文件和目录访问控制即可避免。在这种情况下，损失的只是本地组的成员。存储子系统上的文件和目录仍由本地组拥有。共享上所有 ACL 的情况也是如此。从管理角度看，删除本地组内的 Account Unknown 成员条目，并在新域中用适当的域全局组条目替换，要简单得多，因为该服务器已加入此新域。

使用嵌套组的另一个显著例子涉及在域成员工作站和服务器上实施管理权限。每个域成员机器上的内置本地组 Administrators 的所有成员都被授予管理权限。为了确保所有域管理员在成员服务器或工作站上拥有完整权限，在加入域时，Domain Admins 组会被添加到本地 Administrators 组中。因此，作为 Domain Admins 组成员登录到域的每个人，在每个域成员上都会获得本地管理权限。

UNIX/Linux 没有嵌套组支持的概念，因此 Samba 长期以来也不支持它们。问题在于，你必须将 UNIX 组作为辅助成员输入到 /etc/group 中的某个组中。这行不通，因为在实施 UNIX 文件系统安全模型时，这并不是设计要求。从 Samba-2.2.9 开始，winbind 守护程序可以通过获取 Samba 服务器所属于的域控制器的用户和组信息，按需提供 /etc/group 条目。

实际上，Samba 通过动态的 libnss_winbind 机制补充 /etc/group 数据。从 Samba-3.0.3 开始，此设施用于提供本地组，在相同
