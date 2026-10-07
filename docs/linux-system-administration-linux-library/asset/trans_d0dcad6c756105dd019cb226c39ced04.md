
这些依赖于 PAM。要修复此，系统管理员必须使用单用户模式来纠正错误的文件或重新安装 PAM。

如果你的系统设置为为每个应用程序使用不同的身份验证方案，则每个程序都有其自己的位于 `/etc/pam.d` 的配置文件。`/etc/pam.d` 配置文件的通用语法如下：

```
module_type control_flag module_path [arguments]
```

在 Red Hat 7.0 上，`/etc/pam.d/login` 配置文件如列表 7.5 所示。

```
%%PAM-1.0
auth required /lib/security/pam_security.so
auth required /lib/security/pam_stack.so service=system-auth
      /lib/security/pam_nlogin.so
account required /lib/security/pam_stack.so service=system-auth
password required /lib/security/pam_stack.so service=system-auth
session required /lib/security/pam_stack.so service=system-auth
session optional /lib/security/pam_console.so
```

在这个示例中，`auth` 服务引用的第一个库是 `pam_security.so`。该库用于防止 root 用户通过网络登录。如果用户尝试以 root 身份进行身份验证，模块将确定尝试来自哪个终端，然后检查 `/etc/security` 配置文件以查看该终端是否在列表中。默认情况下，`/etc/security` 文件仅列出物理连接到该机器的终端。它是一个强制模块，因此如果此处失败，将导致该应用程序的整个身份验证方案失败。

`auth` 序列中的下一个库实际上是库检查的堆栈，是对 `/etc/pam.d` 目录中 `system-auth` 文件的引用。这是 Red Hat 7.0 的新特性。在此之前，每个库在 `login` 文件中都有自己的一行。因此，`pam_stack.so` 行实际上运行了列表 7.6 所示 `system-auth` 文件中 `auth` 部分的函数。

## 列表 7.6 system-auth 文件

```
##PAM-1.0
# 此文件自动生成。
# 用户更改将在下次运行 authconfig 时删除。
auth        sufficient /lib/security/pam_unix.so leaveauth nullock
                                 =md5 shadow
auth        required /lib/security/pam_deny.so
account     sufficient /lib/security/pam_unix.so
account     required /lib/security/pam_deny.so
password    required /lib/security/pam_cracklib.so retry=3
password    sufficient /lib/security/pam_unix.so nullock
                                 use_authok md5 shadow
password    required /lib/security/pam_deny.so
session     required /lib/security/pam_limits.so
session     required /lib/security/pam_unix.so
```

结果是`auth` 服务使用的下一个模块是 `pam_unix.so`，即身份验证模块。参数如 `likeauth`、`nullock`、`md5` 和 `shadow`。`likeauth` 参数使模块在作为凭据设置模块和身份验证模块被调用时返回相同的值。默认情况下，它会拒绝 NULL 密码，但 `nullock` 参数会覆盖此设置。我们倾向于移除 `nullock` 参数以防止系统接受 NULL 密码。`shadow` 参数强制系统检查套件是否确保了登录被拒绝，例如如果账户已过期。通过此模块也是必须的。

PAM 的库位于 `/lib/security/`。如果你在登录过程中遇到问题，明智之是检查 `/etc/pam.d/login` 文件以确定需要哪些 PAM 库，并确保它们存在于 `/lib/security` 目录。此外，你应该花些时间理解常用的 PAM 文件。你对它们越熟悉，就越能排除故障。

PAM 的美之处在于其可配置性。PAM 的模块化设计使其易于使用和更改。任何开发为感知 PAM 的应用程序都可以通过不需要用户为每个应用程序学习单独的密码来让生活变得更容易。

要了解更多关于在 Linux 中实现 PAM 的信息，请参见《系统管理员指南》，网址：http://www.us.kernel.org/pub/linux/libs/pam/Linux-PAM-html。

## 文件权限

我们在第 3 章和第 6 章讨论过文件权限，但在安全背景下，这个主题值得再次回顾。正如你从第 4 章的 `chmod` 命令中所记忆的，每个文件都被分配了一个权限字符串。该字符串决定了授予文件所有者、组组成员以及外部其他人员的访问类型。可以授予的访问类型有读 (r)、写 (w) 和执行 (x)。这里有一个权限字符串示例：

```
-rwxrxr-xr 1 owner group 240 May 1 11:00 file
```

在 Linux 下，每个文件都分配有一个所有者和一个组。在这个示例中，所有者被称为 `owner`，组被称为 `group`。所有权与组成员是完全分离的，这意味着所有者不属于文件的组。权限字符串按以下顺序指定权限：所有者、组和其他。查看权限字符串，我们看到文件的所有者对它具有读、写和执行权限。`group` 组成员也有读和执行权限。

在 Red Hat Linux 下，创建用户时，会创建一个同名的组，且只有指定的用户是成员。Red Hat 将这些称为用户私有组。第 6 章描述了这种做法。

要为文件或目录设置适当的访问级别，你需要考虑对它的用途。例如，如果你计划在目录上执行 `ls` 命令，则需要为该目录分配读权限。显然，需要查看的文件需要读访问。同样，需要更改的文件需要写访问。要作为可执行文件运行的文件自然需要执行权限。然而，当文件是目录时，这些要求可能不那么明显。通常，任何你想要搜索或列出其内容的目录都需要读访问。任何要更改的目录内容都需要写访问。如果你想将当前目录更改为目标目录，则该目录必须允许你执行权限。表 7.1 列出了一些命令和所需的文件/目录权限。

## 7.1 常用命令的权限要求

| 命令 | 文件权限 | 目录权限 |
| :--- | :--- | :--- |
| ls /home/user | 无需 | 读 |
| ls -l /home/user | 无需 | 读和执行 |
| cd /home/user | 无需 | 执行 |
| rm /home/user/file | 无需 | 执行和写 |
| cat /home/user/file | 读 | 执行 |
| binary | 执行 | 执行 |
| script | 读和执行 | 执行 |
| rm -r /home/user/testdir | 不适用 | 读、写和执行 |
| binary > file | 写 | 执行 |

你可以看到，如果你想让某能够在特定目录中执行 `ls` 命令，你必须设置权限字符串，使得该用户或其组在该目录中具有读权限。如果你想让用户能够查看文件，则必须为用户或该用户组设置读权限，并且目录必须在用户或组级别上允许访问权限。同样的原理也适用于你尝试仅访问特定组的情况。在这种情况下，创建一个名称如 `project1` 的组。（有关如何执行此操作的说明参见第 6 章。）让每个应该拥有访问权限的个人成为 `project1` 组的成员。（再次参见第 6 章）。现在将存储要访问文件的目录权限设置为类似 `drwx------` 的内容，从而允许目录所有者和 `project1` 组的成员读、写和执行。在该目录中创建的每个文件也必须允许 `project1` 成员读、写和执行权限。

文件权限是一项重要的安全措施，但你真的不想让潜在的入侵者达到那么远。必须采取某些措施来防止任何授权的人员进入系统。

![](img/4fb617eb648f87def380ef5d92052d01_242_0.png)
