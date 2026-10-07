
```
password        required    /lib/security/pam_stack.so service=system-auth
session        required    /lib/security/pam_stack.so service=system-auth
session        optional    /lib/security/pam_console.so
```

在这个示例中，auth 服务引用的第一个库是 pam_security.so。该库用于防止 root 用户通过网络登录。如果用户试图以 root 身份进行身份验证，该模块会确定尝试来自哪个终端，然后检查 /etc/security 配置文件，查看该终端是否被列出。默认情况下，/etc/security 文件仅列出物理连接到该机器的那些终端。这是一个必需模块，因此如果此处失败，将导致此应用整个身份验证方案失效。

auth 序列中的下一个库实际上是一系列库检查堆栈，引用了 /etc/pam.d 目录中的 system-auth 文件。该目录在 Red Hat 7.0 中引入。在此之前，每个库都在 login 文件中拥有自己的行。因此，pam_stack.so 这一行实际执行的是清单 15.6 中所示 system-auth 文件 auth 部分中的功能。

### 清单 15.6: system-auth 文件

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

结果，auth 服务调用的第一个模块是 pam_env.so；正如您可能猜测的那样，该模块设置了必要的环境变量。auth 服务使用的下一个模块是 pam_unix.so，这是主要的身份验证模块。参数为 likeauth 和 nullok。likeauth 参数使得该模块作为凭证设置模块和身份验证模块被调用时返回相同的值。默认情况下，它拒绝空密码，但 nullok 参数会覆盖此行为。我们建议移除 nullok 参数，以防止系统接受空密码。完成这一系列库检查后，控制权返回到 /etc/pam.d/login，其中 auth 服务的最后一步执行 pam_nologin.so，以检查 /etc/nologin 文件是否要求拒绝登录。

**注意** /etc/nologin 文件用于阻止任何用户从控制台登录。在关机期间需要此步骤，以便在系统关闭时新用户无法登录。

PAM 的库位于 /lib/security/ 中。如果您在登录过程中遇到问题，明智的做法是检查 /etc/pam.d/login 文件以确定需要哪些 PAM 库，并确保它们存在于 /lib/security 目录中。此外，您应该花些时间了解常用的 PAM 文件。您越了解它们，就越能更好地排查问题。

PAM 之美在于其可配置性。PAM 的模块化设计使其易于使用且易于更改。任何开发为支持 PAM 的应用程序都通过不需要用户为每个应用学习单独的密码来简化用户的生活。要了解有关在 Linux 中实现 PAM 的更多信息，请参阅《系统管理员指南》，地址为 http://www.us.kernel.org/pub/linux/libs/pam/Linux-PAM-html/pam.html。

## 文件权限

我们在第 5 章和第 7 章中讨论过文件权限，但在安全上下文中重温这一主题很有价值。正如您在第 4 章关于 chmod 命令的讨论中记得的那样，每个文件都被分配一个权限字符串。该字符串决定了授予文件所有者、文件组成员以及外部其他人访问的文件类型。可授予的访问类型为读取 (r)、写入 (w) 和执行 (x)。这是一个示例权限字符串：

```
-rw-r-x-r-x 1 owner group 240 May 1 11:00 file
```

在 Linux 下，每个文件都被分配一个所有者和一个组。在此示例中，所有者名为 owner，组名为 group。所有权的归属与组成员资格完全独立，也就是说，文件的所有者不必属于该文件的组。权限字符串按以下顺序指定权限：所有者、组和其他人。查看权限字符串，我们看到 file 的所有者对其具有读取、写入和执行权限。组 group 的成员具有读取和执行权限。其他所有人也具有读取和执行权限。

在 Red Hat 中，当创建用户时，会创建一个同名的组，该组仅包含该命名的用户作为成员。Red Hat 将这些称为用户私有组。第 5 章描述了这一做法。

要为文件或目录设置适当的访问级别，您需要考虑其用途。例如，如果您计划对目录执行 ls 命令，则需要为该目录分配读取权限。显然，需要查看的文件要求读取访问权限。同样，需要修改的文件要求写入访问权限。需要作为可执行文件运行的文件当然需要执行权限。然而，当该文件是目录时，这些要求可能不那么明显。通常，任何您想要搜索或列出其内容的目录都需要读取访问权限。任何要更改其内容的目录都需要写入访问权限。如果您希望将当前目录更改为目标目录，目录必须允许您拥有执行权限。表 15.1 列出了某些命令和所需的文件/目录权限。

**表 15.1: 常用命令的权限要求**

| 命令 | 文件权限 | 目录权限 |
| :--- | :--- | :--- |
| ls /home/user | 无需权限 | 读取 |
| ls -l /home/user | 无需权限 | 读取和执行 |
| cd /home/user | 无需权限 | 执行 |
| rm /home/user/file | 无需权限 | 执行和写入 |
| cat /home/user/file | 读取 | 执行 |
| binary | 执行 | 执行 |
| script | 读取和执行 | 执行 |
| rm -r /home/user/testdir | N/A | 读取、写入和执行 |
| binary > file | 写入 | 执行 |
<br>
*注意：仅适用于已存在的文件*

您可以看到，如果希望某人能够在特定目录中执行 ls 命令，必须设置权限字符串，使该用户或其组在该目录中具有读取权限。如果希望用户能够查看文件，该文件必须为用户或用户组设置读取权限，并且目录必须在用户或组级别允许访问权限。同样的原则应应用于其他尝试仅向特定组授予访问权限的情况。在这种情况下，创建一个名为 project1 的组。（有关如何执行此操作的说明，请参见第 7 章。）使每个应拥有访问权限的个人成为组 project1 的成员。（再次参见第 7 章。）现在将存储要访问的文件所在的目录的权限设置为类似 drwxrwX---，从而允许目录所有者和组 project1 的成员具有读取、写入和执行权限。在此目录中创建的每个文件也必须允许 project1 的成员具有读取、写入和执行权限。

文件权限是一项重要的安全措施，但您真的不希望潜在的入侵者走到那一步。必须采取一些措施来防止任何未经授权的人员进入系统。

## 防止网络入侵

关于安全的最大任务之一是保护网络免受入侵。只要您拥有网络，特别是连接到 Internet 的网络，就存在入侵的可能性。可以采取许多措施来最大限度地减少危险，但没有方法是万无一失的。通常使用多种方法的组合，以最大化捕获或阻止入侵者的机会。这些方法包括防火墙、TCP Wrappers 和破坏后的分析（通过从错误中学习）以增强预防能力。

## 防火墙

防火墙的目的是双重的。防火墙阻止潜在的入侵者进入，并阻止本地系统用户离开。如果公司希望保护专有信息，它可以阻止来自公司范围之外的任何 IP 地址对系统的访问。通常，这比完全将机器从 Internet 上断开更可取，因为这允许公司内部的远程用户保持访问。如果同一公司希望阻止其用户访问某些外部网站，它可以设置防火墙，限制某些 IP 地址能够通过防火墙向 Internet 上的指定站点发送数据包。数据包本身分为两部分：标头和数据。标头包含发送方的 IP 地址、预期的接收方、数据包大小以及其他相关信息。因此，防火墙无需在数据包的数据部分上浪费时间，而是检查标头以确定如何处理数据包。

最初的防火墙只是不路由的计算机，配有两个网卡，一个连接到 Internet，另一个连接到局域网。如果您需要 Internet 访问权限，请登录防火墙服务器并从中执行功能，将显示导出到您的本地机器。您在防火墙机器上运行的任何内容都同时具有两个网络的访问权限。如今，这种类型的防火墙实现很少使用，至少不是以这种简单的形式；此配置要求所有需要 Internet 访问权限的人都在防火墙上拥有账户。如果您不确定所有获得此类访问权限的用户都是可靠的，您绝对不想这样做。

