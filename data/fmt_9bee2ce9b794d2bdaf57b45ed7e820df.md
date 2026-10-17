
最初，如果`/etc/pam.conf`中的任何条目不正确，或者无法打开模块，所有PAM服务都会失败，用户不被允许访问系统。使用新的值-动作对，可以允许不同的行为。例如，您可能允许在模块实际失败之前出现六个`bad item`返回代码。同样，如果系统缺少`/etc/pam.d`中的适当文件，或者`/etc/pam.conf`文件已被删除，由于`login`是依赖PAM的第一个应用程序，没有人能够登录到系统。要修复此问题，系统管理员必须使用单用户模式来纠正错误的文件或完全重新安装PAM。

如果您的系统配置为为每个应用使用不同的认证方案，每个应用都将拥有位于`/etc/pam.d`中的自己的配置文件。`/etc/pam.d`配置文件的一般语法如下：

```
module_type control_flag module_path [arguments]
```

在Red Hat 7.3中，`/etc/pam.d/login`配置文件看起来如清单15.5所示。让我们逐步检查它的工作原理。

### 清单 15.5：Red Hat 的 `/etc/pam.d/login` 配置文件

```
#%PAM-1.0
auth        required    /lib/security/pam_sepermit.so
auth        required    /lib/security/pam_stack.so service=system-auth
auth        required    /lib/security/pam_nologin.so
account     required    /lib/security/pam_stack.so service=system-auth
```

```
password        required    /lib/security/pam_stack.so service=system-auth
session        required    /lib/security/pam_stack.so service=system-auth
session        optional    /lib/security/pam_console.so
```

在这个示例中，`auth`服务引用的第一个库是`pam_security.so`。该库用于防止`root`用户通过网络登录。如果用户试图以`root`身份进行身份验证，该模块会确定尝试来自哪个终端，然后检查`/etc/security`配置文件，查看该终端是否被列出。默认情况下，`/etc/security`文件仅列出物理连接到该机器的那些终端。这是一个必需模块，因此如果此处失败，将导致此应用整个身份验证方案失效。

`auth`序列中的下一个库实际上是一系列库检查堆栈，引用了`/etc/pam.d`目录中的`system-auth`文件。该目录在Red Hat 7.0中引入。在此之前，每个库都在`login`文件中拥有自己的行。因此，`pam_stack.so`这一行实际执行的是清单15.6中所示`system-auth`文件`auth`部分中的功能。

### 清单 15.6: `system-auth` 文件

```
#%PAM-1.0
# This file is auto-generated.
# User changes will be destroyed the next time authconfig is run.
auth    required    /lib/security/pam_env.so
auth    sufficient    /lib/security/pam_unix.so likeauth nullok
auth    sufficient    /lib/security/pam_smb_auth.so use_first_pass
auth    sufficient
    nologin
auth    required    /lib/security/pam_deny.so

account   required    /lib/security/pam_unix.so

password    required    /lib/security/pam_cracklib.so retry=3 type=
password    sufficient    /lib/security/pam_unix.so nullok use_authtok
md5 shadow
password    required    /lib/security/pam_deny.so

session   required    /lib/security/pam_limits.so
session   required    /lib/security/pam_unix.so
```

结果，`auth`服务调用的第一个模块是`pam_env.so`；正如您可能猜测的那样，该模块设置了必要的环境变量。`auth`服务使用的下一个模块是`pam_unix.so`，这是主要的身份验证模块。参数为`likeauth`和`nullok`。`likeauth`参数使得该模块作为凭证设置模块和身份验证模块被调用时返回相同的值。默认情况下，它拒绝空密码，但`nullok`参数会覆盖此行为。我们建议移除`nullok`参数，以防止系统接受空密码。完成这一系列库检查后，控制权返回到`/etc/pam.d/login`，其中`auth`服务的最后一步执行`pam_nologin.so`，以检查`/etc/nologin`文件是否要求拒绝登录。

`/etc/nologin`文件用于阻止任何用户从控制台登录。在关机期间需要此步骤，以便在系统关闭时新用户无法登录。

PAM的库位于`/lib/security/`中。如果您在登录过程中遇到问题，明智的做法是检查`/etc/pam.d/login`文件以确定需要哪些PAM库，并确保它们存在于`/lib/security`目录中。此外，您应该花些时间了解常用的PAM文件。您越了解它们，就越能更好地排查问题。

PAM之美在于其可配置性。PAM的模块化设计使其易于使用且易于更改。任何开发为支持PAM的应用程序都通过不需要用户为每个应用学习单独的密码来简化用户的生活。要了解有关在Linux中实现PAM的更多信息，请参阅《系统管理员指南》，地址为`http://www.us.kernel.org/pub/linux/libs/pam/Linux-PAM-html/pam.html`。

## 文件权限

我们在第5章和第7章中讨论过文件权限，但在安全上下文中重温这一主题很有价值。正如您在第4章关于`chmod`命令的讨论中记得的那样，每个文件都被分配一个权限字符串。该字符串决定了授予文件所有者、文件组成员以及外部其他人访问的文件类型。可授予的访问类型为读取 (`r`)、写入 (`w`) 和执行 (`x`)。这是一个示例权限字符串：

```
-rw-r-x-r-x 1 owner group 240 May 1 11:00 file
```

在Linux下，每个文件都被分配一个所有者和一个组。在此示例中，所有者名为`owner`，组名为`group`。所有权的归属与组成员资格完全独立，也就是说，文件的所有者不必属于该文件的组。权限字符串按以下顺序指定权限：所有者、组和其他人。查看权限字符串，我们看到`file`的所有者对其具有读取、写入和执行权限。组`group`的成员具有读取和执行权限。其他所有人也具有读取和执行权限。

在Red Hat中，当创建用户时，会创建一个同名的组，该组仅包含该命名的用户作为成员。Red Hat将这些称为用户私有组。第5章描述了这一做法。

要为文件或目录设置适当的访问级别，您需要考虑其用途。例如，如果您计划对目录执行`ls`命令，则需要为该目录分配读取权限。显然，需要查看的文件要求读取访问权限。同样，需要修改的文件要求写入访问权限。需要作为可执行文件运行的文件当然需要执行权限。然而，当该文件是目录时，这些要求可能不那么明显。通常，任何您想要搜索或列出其内容的目录都需要读取访问权限。任何要更改其内容的目录都需要写入访问权限。如果您希望将当前目录更改为目标目录，目录必须允许您拥有执行权限。表15.1列出了某些命令和所需的文件/目录权限。

**表 15.1: 常用命令的权限要求**

| 命令 | 文件权限 | 目录权限 |
| :--- | :--- | :--- |
| `ls /home/user` | 无需权限 | 读取 |
| `ls -l /home/user` | 无需权限 | 读取和执行 |
| `cd /home/user` | 无需权限 | 执行 |
| `rm /home/user/file` | 无需权限 | 执行和写入 |
| `cat /home/user/file` | 读取 | 执行 |
| `binary` | 执行 | 执行 |
| `script` | 读取和执行 | 执行 |
| `rm -r /home/user/testdir` | N/A | 读取、写入和执行 |
| `binary > file` | 写入 | 执行 |

*注意：仅适用于已存在的文件*
