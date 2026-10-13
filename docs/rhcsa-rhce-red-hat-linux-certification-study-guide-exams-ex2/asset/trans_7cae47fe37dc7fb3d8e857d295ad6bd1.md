
## 场景与解决方案

| 场景 | 解决方案 |
|---|---|
| 你需要在包含 Microsoft 计算机的网络上设置共享 | 安装 Samba，在 /etc/samba/smb.conf 中配置共享目录。确保共享目录（除用户主目录外）具有适当的文件类型 samba_share_t。 |
| 你想通过 Samba 设置用户主目录的共享 | 激活 [homes] 部分，在 Samba 身份验证数据库中设置适当的用户，打开 samba_enable_home_dirs 布尔值。 |
| 你想为 Samba 设置基于主机的安全性 | 在 smb.conf 中设置适当的 hosts allow 和 hosts deny 指令，或配置基于 iptables 的防火墙以限制访问。 |
| 你想为 Samba 设置基于用户的[content]
## 场景与解决方案

| 场景 | 解决方案 |
|---|---|
| 你需要在包含 Microsoft 计算机的网络上设置共享 | 安装 Samba，在 /etc/samba/smb.conf 中配置共享目录。确保共享目录（除用户主目录外）具有适当的文件类型 samba_share_t。 |
| 你想通过 Samba 设置用户主目录的共享 | 激活 [homes] 部分，在 Samba 身份验证数据库中设置适当的用户，打开 samba_enable_home_dirs 布尔值。 |
| 你想为 Samba 设置基于主机的安全性 | 在 smb.conf 中设置适当的 hosts allow 和 hosts deny 指令，或配置基于 iptables 的防火墙以限制访问。 |
| 你想为 Samba 设置基于用户的[content]
## 场景与解决方案

| 场景 | 解决方案 |
|---|---|
| 你需要在包含 Microsoft 计算机的网络上设置共享 | 安装 Samba，在 /etc/samba/smb.conf 中配置共享目录。确保共享目录（除用户主目录外）具有适当的文件类型 samba_share_t。 |
| 你想通过 Samba 设置用户主目录的共享 | 激活 [homes] 部分，在 Samba 身份验证数据库中设置适当的用户，打开 samba_enable_home_dirs 布尔值。 |
| 你想为 Samba 设置基于主机的安全性 | 在 smb.conf 中设置适当的 hosts allow 和 hosts deny 指令，或配置基于 iptables 的防火墙以限制访问。 |
| 你想为 Samba 设置基于用户的[content]
## 场景与解决方案

| 场景 | 解决方案 |
|---|---|
| 你需要在包含 Microsoft 计算机的网络上设置共享 | 安装 Samba，在 /etc/samba/smb.conf 中配置共享目录。确保共享目录（除用户主目录外）具有适当的文件类型 samba_share_t。 |
| 你想通过 Samba 设置用户主目录的共享 | 激活 [homes] 部分，在 Samba 身份验证数据库中设置适当的用户，打开 samba_enable_home_dirs 布尔值。 |
| 你想为 Samba 设置基于主机的安全性 | 在 smb.conf 中设置适当的 hosts allow 和 hosts deny 指令，或配置基于 iptables 的防火墙以限制访问。 |
| 你想为 Samba 设置基于用户的[content]
## 场景与解决方案

| 场景 | 解决方案 |
|---|---|
| 你需要在包含 Microsoft 计算机的网络上设置共享 | 安装 Samba，在 /etc/samba/smb.conf 中配置共享目录。确保共享目录（除用户主目录外）具有适当的文件类型 samba_share_t。 |
| 你想通过 Samba 设置用户主目录的共享 | 激活 [homes] 部分，在 Samba 身份验证数据库中设置适当的用户，打开 samba_enable_home_dirs 布尔值。 |
| 你想为 Samba 设置基于主机的安全性 | 在 smb.conf 中设置适当的 hosts allow 和 hosts deny 指令，或配置基于 iptables 的防火墙以限制访问。 |
| 你想为 Samba 设置基于用户的[content]
## 场景与解决方案

| 场景 | 解决方案 |
|---|---|
| 你需要在包含 Microsoft 计算机的网络上设置共享 | 安装 Samba，在 /etc/samba/smb.conf 中配置共享目录。确保共享目录（除用户主目录外）具有适当的文件类型 samba_share_t。 |
| 你想通过 Samba 设置用户主目录的共享 | 激活 [homes] 部分，在 Samba 身份验证数据库中设置适当的用户，打开 samba_enable_home_dirs 布尔值。 |
| 你想为 Samba 设置基于主机的安全性 | 在 smb.conf 中设置适当的 hosts allow 和 hosts deny 指令，或配置基于 iptables 的防火墙以限制访问。 |
| 你想为 Samba 设置基于用户的安全性 | 在 smb.conf 中设置适当的 valid users 和 invalid users 指令 |
| 你需要为组协作设置一个共享 | 设置一个共享段，将 valid users 设置为特定组，并为目录掩码（2770）和创建掩码（2770）设置适当的值。按照第 8 章为组设置共享目录。确保共享目录设置为 samba_share_t。 |

## 认证总结

Samba 允许 Linux 计算机在基于 Microsoft Windows 的网络上像其他 Microsoft 计算机一样出现。Samba 基于 Server Message Block 协议，该协议允许 Microsoft 计算机在 TCP/IP 网络上通信。随着 Microsoft 将 SMB 适配为通用互联网文件系统，Samba 随之演进。对 Samba 的网络通信通过端口 137、138、139 和 445 进行。关键的 SELinux 布尔值是 samba_enable_home_dirs。共享目录应设置为 samba_share_t 文件类型。

主要 Samba 配置文件 /etc/samba/smb.conf 包含全局设置和共享定义的独立部分。smbpasswd 命令可用于在本地 Samba 身份验证数据库中设置现有的 Linux 用户。Red Hat SWAT 工具具有基于 Web 的界面，提供另一种配置 smb.conf 的方式，以及 smbpasswd 命令的前端。

就故障排除而言，对 smb.conf 的更改可使用 testparm 实用程序轻松测试。Samba 包含指令的许多同义词；一些正确指令基于拼写错误。虽然基本 Samba 服务日志消息可在 /var/log/messages 文件中找到，但大多数 Samba 日志信息可在 /var/log/samba 目录中找到。该目录中的许多文件包含客户端名称或 IP 地址。

## 两分钟速览

以下是第 15 章认证目标中的一些关键点。

### Samba 服务

- Samba 允许 Microsoft Windows 计算机使用 TCP/IP 协议栈上的 Server Message Block（SMB）协议在网络间共享文件和打印机。
- Samba 包含客户端和服务器。`mount -t cifs` 或 `/sbin/mount.cifs` 命令的变体支持挂载共享的 Samba 甚至共享的 Microsoft 目录。
- 主要 Samba 配置文件是 `/etc/samba/smb.conf`。你可以在文本编辑器或 SWAT 等 GUI 工具中配置它。
- Samba 支持将 Linux 计算机配置为 Microsoft Windows 服务器。它甚至可以在 Active Directory 网络上提供 Microsoft 浏览、WINS 和域控制器服务。

### Samba 作为客户端

- `smbclient` 命令可以显示来自指定远程 Samba 和 Microsoft 服务器的共享目录和打印机。
- `mount.cifs` 命令可以挂载来自 Samba 或 Microsoft 服务器共享的目录。
- Samba 共享可以通过 `/etc/fstab` 配置文件的帮助在启动过程中挂载。

### Samba 故障排除

- `testparm` 命令对主要 Samba 配置文件 `/etc/samba/smb.conf` 执行语法检查。
- Samba 守护进程的日志可能写入 `/var/log/messages` 文件。
- 大多数 Samba 日志文件可在 `/var/log/samba` 目录中找到。不同日志文件可按客户端和守护进程区分。

## 自测

以下问题将帮助衡量你对本章所呈现材料的理解。由于 Red Hat 考试中没有多项选择题，本书中也没有多项选择题。这些问题专门测试你对本章的理解。即使你有执行任务的另一种方法也可以。Red Hat 考试中重要的是取得结果，而不是死记硬背琐事。这些问题中的许多可能有不止一个答案。

### Samba 服务

1. 一个偏好 Microsoft 服务器的团队已设置 Windows 2008 服务器来处理文件和打印共享服务。该服务器正确引用 192.168.55.3 上的 WINS 服务器进行名称解析，并通过 192.168.55.8 上的 DC 配置所有用户登录。如果你将本地 Linux 系统配置为 DC，至少需要在本地 Samba 配置文件中配置什么指令？

2. 你最近修改了 Samba 配置文件，并且不想断开任何当前用户。什么命令可强制 Samba 服务重新读取配置文件，而无需断开 Microsoft 用户或重启服务？

3. Samba 服务器要与远程系统配合工作，必须打开哪些端口？

4. 通过 Samba 共享主目录时，适当的 SELinux 设置是什么？

5. Samba 上共享目录适当的 SELinux 文件类型是什么？

6. 哪个 Samba 指令限制对 example.org 网络系统的访问？

7. 哪个 Samba 指令限制对用户 tim 和 stephanie 的访问？

8. 哪个 Samba 指令将共享段中的访问限制为名为 ilovelinux 的配置组？

9. 哪个 Samba 指令支持共享段中所有用户的访问？

10. 什么命令将用户 elizabeth 添加到 smbpasswd 或 tdb sam Samba 身份验证数据库？

### Samba 作为客户端

11. 可以使用什么命令挂载远程共享的 Microsoft 目录？

### Samba 故障排除

12. 你对 Samba 配置文件做了几次快速更改，需要快速测试其语法错误。什么命令测试 smb.conf 的语法错误？

## 实验问题

这些实验中的几个涉及配置练习。你应该只在测试机器上执行这些练习。假设你正在诸如 KVM 之类的虚拟机上运行这些练习。对于本章，还假设你可能正在更改用于此类虚拟机的物理主机系统的配置。

Red Hat 以电子方式呈现其考试。出于这个原因，本章及以后章节的实验可从随书附带的 CD 中获得，位于 Chapter15/ 子目录中。如果尚未在系统上设置 RHEL 6，请参阅第 1 章的安装说明。

每个实验的答案在填空自测题的自测答案之后。

## 自测答案

### Samba 服务

1. 至少，要将 Linux 系统配置为 DC，需要配置 `security = user` 指令。如果它在活动目录系统上，使用 `security = ads` 指令更好。

2. 强制 Samba 服务重新读取配置文件而不断开 Microsoft 用户或重启服务的命令是 `service smb reload`。

3. 与 Samba 服务器通信相关的打开端口是 TCP 端口 137、138、139 和 445。

4. 与 Samba 上共享主目录相关的 SELinux 布尔值是 `samba_enable_home_dirs`。

5. 共享 Samba 目录适当的 SELinux 文件类型是 `samba_share_t`。

6. 限制对 example.org 网络系统访问的 Samba 指令是

    `hosts allow .example.org`

    以下指令也是可接受的答案：

    `allow hosts .example.org`

7. 限制对所述用户的访问的一个 Samba 指令是

    `valid users = tim stephanie`

8. 限制对所述组的访问的一个 Samba 指令是

    `valid users = +ilovelinux`

    `@ilovelinux` 组也将被接受。

9. 支持共享段中所有用户访问的一个 Samba 指令是

    `guest ok = yes`

10. 将用户 elizabeth 添加到任一 Samba 身份验证数据库的命令是

    `# smbpasswd -a elizabeth`
