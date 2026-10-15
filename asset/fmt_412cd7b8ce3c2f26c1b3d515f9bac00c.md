
| only | 仅更新 LDAP 密码，并让 LDAP 服务器处理其他字段。此选项仅在支持 `LDAP_EXOP_X_MODIFY_PASSWORD` 的某些 LDAP 服务器上可用。 |

**表 10.5 MySQL passdb 后端的基本 `smb.conf` 选项**

| 字段 | 内容 |
|---|---|
| mysql host | 主机名，默认为 `'localhost'` |
| mysql password |  |
| mysql user | 默认为 `'samba'` |
| mysql database | 默认为 `'samba'` |
| mysql port | 默认为 3306 |
| table | 包含用户的表名称 |

| 字段 | 类型 | 内容 |
|---|---|---|
| logon time column | int(9) | 用户最后登录的 UNIX 时间戳 |
| logoff time column | int(9) | 用户最后注销的 UNIX 时间戳 |
| kickoff time column | int(9) | 用户应从工作站被踢出的时刻的 UNIX 时间戳（未强制执行） |
| pass last set time column | int(9) | 密码上次设置时刻的 UNIX 时间戳 |
| pass can change time column | int(9) | 从此时刻开始可以更改密码的 UNIX 时间戳 |
| pass must change time column | int(9) | 必须更改密码的时刻的 UNIX 时间戳 |
| username column | varchar(255) | UNIX 用户名 |
| domain column | varchar(255) | NT 用户所属的域 |
| nt username column | varchar(255) | NT 用户名 |
| fullname column | varchar(255) | 用户全名 |
| home dir column | varchar(255) | UNIX 主目录路径（相当于 `logon home` 参数） |
| dir drive column | varchar(2) | 目录驱动器路径（例如 "H:"） |
| logon script column | varchar(255) | 登录时在客户端端运行的批处理文件 |
| profile path column | varchar(255) | 配置文件路径 |
| acct desc column | varchar(255) | 一些 ASCII NT 用户数据 |
| workstations column | varchar(255) | 用户可以登录的工作站（或 `NULL` 表示所有） |
| unknown string column | varchar(255) | 未知字符串 |
| munged dial column | varchar(255) | 未知 |
| user sid column | varchar(255) | NT 用户 SID |
| group sid column | varchar(255) | NT 组 SID |
| lanman pass column | varchar(255) | 加密的 lanman 密码 |
| nt pass column | varchar(255) | 加密的 nt 密码 |
| plain pass column | varchar(255) | 明文密码 |
| acct ctrl column | int(9) | NT 用户数据 |
| unknown 3 column | int(9) | 未知 |
| logon divs column | int(9) | 未知 |
| hours len column | int(9) | 未知 |
| bad password count column | int(5) | 在禁用账户之前失败的密码尝试次数 |
| logon count column | int(5) | 登录尝试次数 |
| unknown 6 column | int(9) | 未知 |

# 组映射：MS WINDOWS 和 UNIX

从 Samba-3 开始，新增了组映射功能，用于创建 Windows 组 SID 与 UNIX 组之间的关联。`net` 工具中包含的 `groupmap` 子命令可用于管理这些关联。

将 NT 组映射到 UNIX 系统组的新功能允许管理员决定哪些 NT 域组应暴露给 MS Windows 客户端。只有映射到具有非默认值 `-1` 的 UNIX 组的 NT 组才会暴露在给域用户和组提供访问权限的工具中的组选择列表中。

> **警告**
>
> 域管理组参数已在 Samba-3 中被移除，因此不应再在 `smb.conf` 中指定该参数。在 Samba-2.2.x 中，此参数用于赋予列出的用户成为 Windows“域管理员”组成员的权限，这给予了他们在其工作站上的本地管理员权限（在默认配置下）。

## 11.1 功能与优势

Samba 允许管理员创建 MS Windows NT4/200x 组账户，并将其任意与 UNIX/Linux 组账户关联。

可以使用 MS Windows NT4 或 MS Windows 200x/XP Professional MMC 工具管理组账户。如果希望在使用这些工具时自动创建 UNIX/Linux 系统账户，则应在 `smb.conf` 中提供适当的接口脚本。如果缺少这些脚本，且 `winbindd` 正在运行，则通过这些工具创建的 Samba 组账户将从 *smb.conf* 文件中由 `idmap uid`/`idmap gid` 参数指定的 ID 范围中分配 UNIX UID 和 GID。

**图 11.1 IDMAP：组 SID 到 GID 的解析。**

![](img/86d74c6cc862465e3a42e6dc3c90935a_235_0.png)

在这两种情况下，当 `winbindd` 未运行时，只能识别本地可解析的组。请参阅图 11.1 和图 11.2。`net groupmap` 用于建立 UNIX 组到 NT SID 的映射，如图 11.3 所示。

管理员应注意，当 *smb.conf* 组接口脚本直接调用 UNIX/Linux 系统工具（如 `shadow` 实用程序、`groupadd`、`groupdel`、`groupmod`）时，生成的 UNIX/Linux 组名将受到这些工具施加的任何限制。如果工具不允许使用大写字母或空格字符，则尝试创建名为 *Engineering Managers* 的 MS Windows NT4/200x 风格组将试图创建一个同名 UNIX/Linux 组，而这一尝试当然会失败。

对于操作系统工具的限制，有几种可能的变通方法。一种方法是使用生成符合操作系统限制的 UNIX/Linux 系统组名称的脚本，然后仅将 UNIX/Linux 组 ID（GID）返回给调用 Samba 接口。这将提供动态的变通解决方案。

另一种变通方法是手动创建 UNIX/Linux 组，然后在 Samba 服务器上手动创建 MS Windows NT4/200x 组，并使用 `net groupmap` 工具将两者连接起来。

![](img/86d74c6cc862465e3a42e6dc3c90935a_236_0.png)

![](img/86d74c6cc862465e3a42e6dc3c90935a_236_1.png)

## 11.2 讨论

当您在计算机上安装 MS Windows NT4/200x 时，安装程序会创建默认的用户和组，特别是 Administrators 组，并赋予该组执行基本系统任务所需的权限，例如更改日期和时间或终止（或关闭）本地机器上运行的任何进程。

Administrator 用户是 Administrators 组的成员，因此继承 Administrators 组的权限。如果创建一个名为 joe 的用户并成为 Administrators 组的成员，joe 将与用户 Administrator 拥有完全相同的权限。

当 MS Windows NT4/200x/XP 机器成为域成员时，PDC 的“Domain Admins”组会被添加到工作站的本地 Administrators 组中。Domain Admins 组的每个成员在登录到工作站时都会继承本地 Administrators 组的权限。

以下步骤说明了如何使 Samba PDC 用户成为 Domain Admins 组的成员。

1. 创建一个 UNIX 组（通常在 `/etc/group` 中）；我们称之为 domadm。
2. 将必须成为“管理员”的用户添加到该组中。例如，如果您希望 joe、john 和 mary 成为管理员，您在 `/etc/group` 中的条目将如下所示：

```
domadm:x:502:joe,john,mary
```
