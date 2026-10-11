
- 步骤 3. 更新 `/etc/fstab` 文件中的条目，以反映凭据读取方式的变化：

```
//172.168.1.1/company_data /opt/test cifs credentials=/etc/samba/mbcreds 0 0
```

你可以使用 `mount` 命令卸载 Samba 共享并重启系统，以确保共享在系统重启时能够正确挂载。

## 总结

Samba 非常适合与 Windows 系统共享文件。它还可以为 Windows 域控制器提供良好的备份策略。本章展示了一些极大的优势，例如提供打印服务和 Windows 登录服务。学习配置 Samba 有许多信息需要吸收。幸运的是，配置文件有详尽的文档帮助你。在下一章中，我们将查看 FTP 服务器和客户端。

380 红帽考试实战指南：RHCSA™ 和 RHCE® 认证指南与实验手册

## 复习题

- 1. 本章讨论了哪两种后端认证机制？
- 2. 在创建共享时，没有选项可以使其可浏览。对的还是错？
- 3. `testparm` 命令的作用是什么？
- 4. 使用什么命令为 Samba 创建用户？
- 5. 你可以使用什么命令来查看已挂载的 Samba 共享？
- 6. Samba 服务器只能向用户提供文件。对的还是错？

## 复习题答案

- 1. 本章描述了 `tdbsm` 和 `smbpasswd` 后端认证。
- 2. 错。每个共享都有 `browseable` 选项。
- 3. `testparm` 命令允许你检查 `/etc/samba/smb.conf` 文件中的语法错误。
- 4. 使用 `smbpasswd` 命令来创建 Samba 用户。
- 5. `smbstatus` 命令向你显示当前已挂载的 Samba 资源。
- 6. 错。Samba 服务器还可以向用户提供打印服务等。

## 实验

Samba

到目前为止，你在客户端连接到 Samba 服务器方面做得很好。你需要知道，任何没有被添加到 `/etc/fstab` 的挂载共享在系统重启时都会被卸载。为了解决这种情况，你可以在 `/etc/fstab` 文件中创建一个条目。

- 步骤 1. 在 `/etc/fstab` 文件中创建一个条目：

```
//172.168.1.1/company_data /opt/test cifs user=user01,pass=<password> 0 0
```

有人能发现这有什么问题吗？用户名和密码以明文形式暴露，所有人都能看到。另一种在不暴露凭据的情况下创建 `/etc/fstab` 文件条目的方法是将凭据放在文件中，然后在 `/etc/fstab` 文件中引用。

- 步骤 2. 将你想使用的凭据放入文件中：

```
# echo "username=user01" > /etc/samba/mbcreds
# echo "password=password" >> /etc/samba/mbcreds
```

> 考试提示

确保正确设置了 `/etc/samba/mbcreds` 的权限。

- 步骤 3. 更新 `/etc/fstab` 文件中的条目，以反映凭据读取方式的变化：

```
//172.168.1.1/company_data /opt/test cifs credentials=/etc/samba/mbcreds 0 0
```

你可以使用 `mount` 命令卸载 Samba 共享并重启系统，以确保共享在系统重启时能够正确挂载。

## 总结

Samba 非常适合与 Windows 系统共享文件。它还可以为 Windows 域控制器提供良好的备份策略。本章展示了一些极大的优势，例如提供打印服务和 Windows 登录服务。学习配置 Samba 有许多信息需要吸收。幸运的是，配置文件有详尽的文档帮助你。在下一章中，我们将查看 FTP 服务器和客户端。

FTP

在本章中，我们使用 `vsftpd`，其全称为 Very Secure FTP Daemon。这种特定的 FTP 服务器提供了功能使其更安全。

安装 FTP 服务器

为了向网络提供 服务，你需要确保相应的软件包已安装。以下是方法：

- 步骤 1. 获取所需的包：

```
# yum install vsftpd
```

- 步骤 2. 安装完成后，验证已安装：

```bash
# rpm -qa | grep vsftpd
vsftpd-2.2.2-el16.x86_64
```

- 步骤 3. 确保服务在系统启动时启动：

```
# chconfig vsftpd on
```

- 步骤 4. 验证服务启动状态：

```
# chconfig vsftpd --list
vsftpd 0:off 1:off 2:on 3:on 4:on 6:off
```

## 配置 vsftpd

要开始配置 FTP 服务器，你需要查看配置文件。对于 `vsftpd`，只有一个主配置文件，位于 `/etc/vsftpd/vsftpd.conf`，这是你配置 FTP 服务器设置的地方。

- 步骤 1. 查看配置文件中有哪些选项：

```bash
# grep -v '^#' vsftpd.conf
anonymous_enable=YES
local_enable=YES
write_enable=YES
local_umask=022
dirmessage_=YES
xferlog_enable=YES
connect_from_port_20=YES
xferlog_std_format=YES
listen=YES
pam_service_name=vsftpd
userlist_enable=YES
tcp_wrappers=YES
```

- 步骤 2. 现在我们解释一下这些选项的用途：

`anonymous_enable=YES`

默认设置：设置安全性，虽然为了更好的主机安全性应将其更改为 NO

`local_enable=YES`

允许用户登录

`write_enable=YES`

允许用户写入目录

`local_umask=022`

为所有上传的文件设置 umask

`dimmessage_enable=YES`

显示目录消息

`xferlog_enable=YES`

将所有流量活动记录到 `/var/log/xferlog`

`connect_from_port_20=YES`

强制端口传输源自 20 端口

`xferlog_std_format=YES`

以标准传输格式记录所有内容

`listen=YES`

允许服务器监听连接

`pam_service_name=vsftpd`

指定用于 PAM 服务的名称

`userlist_enable=YES`

允许服务查询 user_list 列表

`tcp_wrappers=YES`

根据 TCP Wrappers 配置允许入站请求

`userlist_deny=YES`

允许 user_list 中列的用户通过 FTP 登录

这些针对 `vsftpd` 服务的默认设置使你能够快速上手并使用 FTP 服务。在任何时候，你系统中的任何用户都能够登录到 `vsftpd` 服务，但由于默认启用了防火墙，连接将被拒绝。在向用户开放连接之前，也许可以花些时间熟悉在 FTP 服务器上可以配置的各种选项。配置文件对于每个选项的作用有详尽的文档说明。

# 考试提示

如果你在配置文件中找不到或忘记某个特定选项的作用，你可以在考试期间参考它的帮助页（man page）。要访问配置帮助页，请使用此命令：

```bash
# man vsftpd.conf
```

如果你翻阅这些页面，你会发现有大量的选项可以用来配置和锁定 `vsftpd` 服务，尽管你已经设置的选项对于基础使用来说已经足够了。虽然考试只需要基础配置，但你可以让此服务成为一个可行的选项，以安全、集中的方式为你的用户提供文件或托管项目。

# 考试提示

在编辑配置文件时，请确保在你使用的选项与其赋值的值之间不要包含任何空格。这可能会导致服务启动期间出现错误。

# 386 红 Hat考试实战指南：RHCSA® 和 RHCE® 认证指南与实验手册

# 防火墙和 SELinux 配置

在开始使用 FTP 服务之前，你还需要对防火墙进行一些调整并对 SELinux 进行更改。让我们从防火墙规则开始。FTP 同时使用 TCP 端口 20 和 21，你可以在防火墙上开启这些端口。

步骤 1. 使用 `iptables` 命令创建你的防火墙规则：

```bash
# iptables -I INPUT 5 -p tcp -m tcp --dport 20 -j ACCEPT
# iptables -I INPUT 5 -p tcp -m tcp --dport 21 -j ACCEPT
```

步骤 2. 保存你刚刚创建规则：

```bash
# service iptables save
Saving firewall rules to /etc/sysconfig/iptables: [ OK ]
```

步骤 3. 重启防火墙服务使更改生效：
