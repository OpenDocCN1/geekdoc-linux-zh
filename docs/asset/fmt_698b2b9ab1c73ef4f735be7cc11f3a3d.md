
```bash
# 示例 /etc/sudoers 文件。
# 此文件必须以 root 身份使用 'visudo' 命令进行编辑。
# 查看 man 页面以获取如何编写 sudoers 文件的详情。
## 用户别名指定
# 六个用户

User_Alias FULLTIMERS=[逗号分隔的列表列表]
User_Alias PARTTIMERS=[逗号分隔的用户列表]

# * Runas 别名指定
# 他们以 root 身份运行
Runas_Alias OP=root,operator

## Cmnd 别名指定
# 他们可以运行的一些命令
Cmnd_Alias KILL=/usr/bin/kill
Cmnd_Alias PRINTING=[逗号分隔的命令列表]
Cmnd_Alias SHUTDOWN=/usr/etc/init/shutdown
Cmnd_Alias HALT=/usr/etc/halt,/usr/etc/fasthalt
Cmnd_Alias REBOOT=/usr/etc/reboot,/usr/etc/fastboot
Cmnd_Alias SHELLS=/usr/bin/sh,/usr/bin/csh,[more-shells]

Cmnd_Alias SU=/usr/bin/su
Cmnd_Alias VIPW=/usr/etc/vipw,/etc/vipw,/bin/passwd

# # 主机别名指定
## 某些主机
Host_Alias CSNETS=[逗号分隔的主机 IP 列表]
Host_Alias CUNETS=[逗号分隔的主机 IP 列表]

## ## 用户规范
# root 和 wheel 组中的用户可以在任何机器上以任何用户身份运行任何
root ALL=(ALL) ALL
%wheel ALL=(ALL) ALL
# 全职系统管理员无需密码即可在任何机器上运行任何命令
FULLTIMERS ALL=NOPASSWD:ALL
```

由于 `sudoers` 是一个安全导向的文件（类似于 `/etc/passwd`），在编辑它时必须采取特殊步骤。`sudo` 分发版带有一个专门为此目的设计的特殊工具：`visudo`。

# 使用 `visudo` 编辑 `/etc/sudoers`

`visudo` 与 `vipw`（之前讨论过的）非常相似。它的目的是为你提供一种安全、干净的方法来编辑 `/etc/sudoers`。`visudo` 在编辑期间会锁定 `sudoers` 文件，更重要的是，它会扫描语法错误并且不允许你将这些错误提交到磁盘。

## 访问控制

接下来，我们将快速介绍基本的访问控制。访问控制是任何选择性地授予或拒绝用户访问系统资源的技术，包括文件、目录、卷、驱动器、服务、主机、网络等。

接下来，我们将关注文件和目录的访问控制，这与单个用户和组有关。

## 权限与所有权

在 Linux 中，你通过建立权限来限制用户对文件和目录的访问。存在三种基本权限类型：

- 读取（Read）允许用户读取指定的文件。
- 写（Write）允许用户修改指定的文件。
- 执行（Execute）允许用户执行指定的文件。

![](img/238ef1f85709de12ba67e71734ee1e37_120_0.png)

当你分配这些权限时，Linux 会保留记录，稍后反映在文件列表中。每个文件的权限状态用令牌（tokens）表示。权限令牌为：

- `r`-读取访问
- `w`-写入访问
- `x`-执行访问

要确定文件或目录的权限，请使用 `ls -l` 命令以长格式格式列出它。以下是一些典型输出：

```
drwwxrxr-x 3 Nicole 1024 Apr 18 13:10 .
drw-xr-xr-x 5 root 1024 Apr 14 23:22 ..
-rw-r--r-- 1 Nicole 173 Apr 18 12:36 .bash_history
-rw--r--r-- 1 Nicole 674 Feb 5 1997 .bashrc
-rw--r--r-- 1 Nicole 602 Feb 5 1997 .
-rw--r--r-- 1 Nicole 116 Feb 5 1997 .login
-rw--r--r-- 1 Nicole 234 Feb 5 1997 .profile
drw-rxr-xr-x 3 Nicole 1024 Jun 2 1998 1g
-rw-xr-xr-x 1 Nicole 45 Apr 18 13:07 parse_out.pl
```

我们将使用 Nicole 的 Perl 脚本作为示例。查看最左侧的列查看权限：

```
-rw-rxr-x 1 Nicole 45 Apr 18 13:07 parse_out.pl
```

权限列包含 10 个字符。请参图 4.5。![](img/238ef1f85709de12ba67e71734ee1e37_120_0.png)

图 4.5 描述了以下权限令牌：

- `r`-读取访问
- `w`-写入访问
- `x`-执行访问

## 基础 Linux 系统管理

## 第4 章

| 八进制值 | 解释 |
|---|---|
| 2000 | 模式 2000 应用了 SETGID 位。请参阅本章后部分的“特殊权限文件”。 |
| 4000 | 模式 4000 应用了 SETUID。请参阅本章后部分的“特殊权限文件”。 |

当你使用硬八进制值时，需要将它们相加。这会产生一个表示所有授予权限的最终数字。但事情不必那么复杂。你可以使用这些值快速将所有者、组和其他和其他的权限简化为三位数字：

- 0 = 无权限
- 1 = 执行
- 2 = 写入
- 3 = 写入和执行（现较少使用）
- 4 = 读取
- 5 = 读取和执行
- 6 = 读取和写入
- 7 = 权限全开：

例如，你可能为你的内网开发开发了一个用于部署的脚本。为了让所有用户都能使用该脚本，你必须应用适当的权限。
