

# /etc/shadow 和 /etc/security/passwd 文件

自 Unix 元以来。它支持 /etc/datemsk 中指定的约 30 种格式，同时也支持 Linux 使用的 yyyy-mm-dd 格式。

- 第九字段预留备用。Linux 和 HP-UX 遵循这一惯例，而 Solaris 使用最后 4 位来计算登录失败的次数。

让我们来看示例 shadow 行：

```
millert:$md5em5j8hl$aIQ3pXe0sakadRaRFyyt7Ppj::1446:0:180:::
```

在这个示例中，用户 millert 在 2009 年 8 月 13 日更改了密码。
密码必须在 180 天内更改，且 millert 将在这一期间的最后两周收到需要更改密码的警告。该账户没有过期日期。

在 Solaris、HP-UX 和 Linux 上，你可以使用 `pwconv` 将 shadow 文件的内容与 passwd 文件进行协调，拾取任何不再出现在 passwd 文件中的新增或删除项。在 Linux 中，`pwconv` 会根据 /etc/login.defs 中定义的默认值填充 shadow 参数。

![](img/579efec8c67772f31ecf34844bbb71a2_233_0.png)

Solaris 上的 root 可以命令 `-f username` 强制用户在下次登录时更改密码。如果你经常运行 crack 来发现选择不当（不安全）的密码，这个功能非常有用。（在 Linux 下，该 `-f` 标志允许用户更改其 finger 信息。）

![](img/579efec8c67772f31ecf34844bbb71a2_233_1.png)

AIX 不使用 shadow 密码，但它使用了相同的概念。AIX 的加密密码存储在 /etc/security/passwd 中，其格式与 /etc/passwd 文件完全不同。这里是一个 AIX 安装的示例，其中密码算法默认为 crypt：

trent:

```
password = u10.YaXRx4ql
lastupdate = 1224876639
flags = ADCMCH
```

```
password = Plir2gOPabZ.Q
lastupdate = 1235785246
flags =
```

这种格式应该是自显自明的的。一个或多个空行分隔不同的条目。同样的格式也用于 /etc/security 下的 AIX 配置文件，其中用户名被泛化为正在被控制或记录的任何对象。

AIX 提供了无数种控制选项来管理登录和密码的所有方面。某些选项是面向用户的，某些是面向端口的（用于控制特定用户可以登录的 TTY 端口）。详情请参阅 /etc/security/login.cfg 和 /etc/security/user 中的注释。一个实用的命令是 `pwadm`，它可以让你强制用户在下次登录时更改密码。

- 切换到更强的加密算法应该是 AIX 设备待办清单上的高优先级任务。

![](img/579efec8c67772f31ecf34844bbb71a2_233_2.png)

# 7.3 /ETC/GROUP 文件

/etc/group 文件包含 UNIX 组的名称以及每个组的成员列表。这里是 AIX 系统组文件的一个部分：

```
system!:0:root,pconsole,esaadmin
staff!:1:ipsec,esaadmin,trent,ben,garth,evi
bin!:2:root,bin
sys!:3:root,sys
adm!:4:bin,adm
nobody!:4294967294:nobody.lpd
```

每一行代表一个组，包含四个字段：

- 组名
- 加密密码或占位符
- GID 编号
- 成员列表，用逗号分隔

与 /etc/passwd 来说，字段由冒号分隔。为了兼容性，组名应限制在八个字符以内，许多系统并不要求此。可以输入组密码以允许不属于该组的用户通过 `newgrp` 命令进入该组，但只有 Linux 对组密码有真正的支持。可以使用 `passwd` 命令设置密码；加密形式存储在 /etc/gshadow 文件中。密码很少被使用。

对于用户名和 UID，在通过网络文件系统共享文件的机器之间，组名和 GID 应该保持一致。在异构环境中，这种一致性很难维护，因为不同的操作系统对同一个组使用不同的 GID。

我们发现，处理此问题的最佳方法是避免将系统组作为用户的默认登录组。某些系统结合所有权和权限位来控制命令的执行。系统之间的 GID 不一致会给全站性的软件更新和安装系统带来混乱。

如果用户在 /etc/passwd 中默认为某个特定组，但根据 /etc/group 似乎并不属于该组，则以 /etc/passwd 的结果为准。登录时授予的组成员关系实际上是 passwd 和 group 文件中发现成员的并集。

某些系统限制了用户可以所属组的数量。以前8是一个常见的限制，但现在 Solaris 上是 16，HP-UX 上是 20，其他系统无限制。

要为用户设置密码，使用 `passwd` 命令。要删除密码，使用 `passwd -l` 标志。

# 添加用户：基本步骤

为了减少工作量，我们建议从 GID 500 或更高开始，以避免与使用 1000 以下 GID 的系统账户冲突。

添加用户，使用 `useradd` 命令。这会在 passwd、shadow 和 group 文件中创建条目，并创建主目录。

修改用户账户，使用 `usermod` 命令。删除用户，使用 `userdel` 命令。

要更改密码，使用 `passwd` 命令。这对于用户来说也是必要的。

![](img/579efec8c67772f31ecf34844bbb71a2_235_0.png)

# 第 7 章 添加新用户

要求：
- 让新用户签署协议
- 编辑 shadow 文件
- 将用户添加到 /etc/group（并非绝对必要，但很有帮助）
- 设置初始密码
- 创建、更改所有（chown）和权限（chmod）用户的主目录。
- 配置角色和权限（如果你使用 RBAC；见第 190 页）。

对于用户：
- 将默认启动文件复制到用户的主目录。
- 设置用户主目录邮件别名。

对于你：
- 验证账户已设置完毕。
- 将用户的联系信息和账户状态添加到你的数据库中。

![](img/579efec8c67772f31ecf34844bbb71a2_235_1.png)

