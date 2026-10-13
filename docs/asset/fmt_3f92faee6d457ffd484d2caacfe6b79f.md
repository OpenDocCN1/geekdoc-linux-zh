
` solaris.admin.fsmgr `::挂载和共享：

` solaris.admin.fsmgr.read `::查看挂载和共享：help=`AuthFsmgrRead.html`

` solaris.admin.fsmgr.write `::管理和共享文件：help=`AuthFsmgrWrite.html`

` solaris.admin.logsvc `::删除日志

` solaris.admin.logsvc.purge `::删除日志文件：help=`AuthLogsvcPurge.html`

` solaris.admin.logsvc.read `::查看日志文件：help=`AuthLogsvcRead.html`

` solaris.admin.logsvc.write `::管理日志设置：help=`AuthLogsvcWrite.html`

` solaris.admin.serialmgr `:::串口管理器：

` solaris.admin.usermgr `:::用户账户：

` solaris.admin.usermgr.passwd `::更改密码：help=`AuthUserMgrPSwd.html`

` solaris.admin.usermgr.read `::查看用户和角色：

help=`AuthUserMgrRead.html`

` solaris.admin.usermgr.write `::管理用户：help=`AuthUserMgrWrite.html`

你可以看到 Solaris 定义了多种授权，包括文件系统管理 (`fsmgr`)、日志管理 (`logsvc`)、端口管理 (`serialmgr`) 和用户管理 (`usermgr`)。相应的帮助文件也列出了。

授权的一个重要方面是可以使用 `grant` 关键字将权限转移给他人。一个字符串允许向其他用户委托授权。例如，`solaris.admin.usermgr.grant` 授权结合 `solaris.admin.usermgr.pswd`，允许被委托的用户执行密码更改。

角色、权限和授权是如何结合的？图 11-3 显示了授权与特定配置关联，而配置反过来又被分配了各种角色的用户使用。RBAC 将用户从直接使用命令和授权中抽象出来的方式由图中的虚线所示。

# 第 11 章：基于角色的访问控制 247

![](img/11bcccd1804574cca0c3018732958dd5_276_0.png)

图 11-3 角色、配置方案和授权的集成

## 操作

在实现 RBAC 时，通常会执行以下操作。

### sudo

`sudo` 设施通过 `/etc/sudoers` 文件配置。该文件包含所有可以访问 `sudo` 设施的用户列表，并定义了他们的权限 `/etc/sudoers` 中的一个典型条目如下：

```
jdoe ALL=(ALL) ALL
```

此条目允许用户 `jdoe` 以超级用户的身份访问所有应用程序。要让用户 `jdoe` 以超级用户身份运行命令，她只需要在命令字符串前加上 `sudo`。因此，若要以 root 身份执行 `format` 命令，`jdoe` 将输入以下命令字符串：

```
$ sudo format
```

随后将显示以下输出：

我们相信你已经接受了本地系统管理员的常规讲解。这通常归结为以下两点：

- #1) 尊重他人的隐私。
- #2) 在输入之前先思考。

密码：

如果 `jdoe` 正确输入了他的普通密码，`format` 命令将以 root 权限执行。如果 `jdoe` 错误输入密码最多三次，在每个提示后都会出现以下消息：

去吃片压力缓解药并仔细考虑。

密码：
你这个愚蠢、扭曲的男孩。
密码：
他掉进水里了！
密码输入不正确

此时，系统会将警报邮件发送给超级用户，告知他们潜在的安全违规——此类重复的登录尝试可能意味着恶意用户正在进行密码猜测攻击。同样，这也可能表明某人输入的密码错误（可能是大写锁定已开启），或者他们正在输入 root 密码而不是自己的密码。

为了列出允许该用户的所有权限，该用户只需运行带有 `-l` 选项的 `sudo`：

```
$ sudo -l
```

你可以在此主机上运行以下命令：

`(ALL) ALL`

除了授予完全超级用户访问外，`sudo` 还可以更灵活地将授权授予特定个人。例如，你可以创建与 `sudoers` 执行的限制命令集对应的命令别名：

```
Cmnd_Alias TCP=/usr/bin/tcpd
```

在这种情况下，你正在赋予用户对 TCP 守护进程的控制权。你还可以指定除 `ALL` 之外的共享执行不同类命令能力的的用户组：

```
User_Alias DEVELOPERS=pwatters,tgibes

User_Alias ADMINS=maya,natashia
```

因此，`DEVELOPERS` 组可以被分配访问 `ADMINS`无法使用的特定设施。将所有内容结合，你可以创建如下复杂的用户规范：

```
ADMINS ALL=(ALL) NOPASSWD: ALL

DEVELOPERS ALL=TCPD
```
