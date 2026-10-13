
`777` 目录权限字符串前面的数字 `1` 被称为“粘滞位”。该粘滞位允许任何用户在目录中执行任何操作，这是 `777` 权限值的功劳。但此类权限仅限于特定用户创建的文件。否则，任何用户都可以删除或重命名 `/home/PublicShare` 目录中的任何文件，而不管文件的所有者是谁。

另外，权限仅限于组成员的目录可能具有 `2770` 权限，其中设置了 SGID 位，并向拥有该目录的组成员授予完全权限。

## 练习 15-1

## 配置 Samba 主目录共享

在本练习中，您将了解基本的主目录共享。您至少需要两台计算机，其中一台应为 Samba 服务器。另一台可以是 Linux 或 Microsoft Windows 工作站。您将从工作站连接到 Samba 服务器并访问 Samba 服务器上主目录中的文件。

这些步骤假设用户账户为 `michael`；请根据实际情况替换为你的常规用户账户名。

- 1. 安装并配置 Samba 以开始使用本章前面描述的方法。
- 2. 打开 `/etc/samba/smb.conf` 配置文件。查找 `workgroup` 的当前值。
- 3. 确保本地网络上的计算机具有相同的 `workgroup` 值。如果本地网络是 Windows 风格的域，请将 `workgroup` 设置为域的名称。
- 4. 使用 `testparm` 命令测试 Samba 配置文件的语法。
- 5. 阅读并解决 `testparm` 命令输出中出现的问题。修复输出中定义的任何 `smb.conf` 语法问题。
- 6. 使用以下命令在 Samba 服务器上激活 `samba_enable_home_dirs` 布尔值：
  ```
  # setsebool -P samba_enable_home_dirs on
  ```
- 7. 使用以下命令在 Samba 服务器的身份验证数据库中设置用户账户（在提示时输入适当的密码）：
  ```
  # smbpasswd -a michael
  ```
- 8. 使用以下命令使 Samba 重新读取 `smb.conf` 文件：
  ```
  # service smb reload
  ```
- 9. 前往同一域或工作组中的远程 Linux 或 Microsoft Windows 工作站。
- 10. 如果你能使用以下命令浏览 Samba 服务器的计算机列表，则浏览功能正常工作。将 `sambaserver` 替换为已配置的 Samba 服务器主机名。
  ```
  # smbclient -L sambaserver -U michael
  ```
- 11. 以 `root` 用户身份登录远程 RHEL 6 Samba 客户端。
- 12. 从该远程 RHEL 6 客户端，使用 `mount.cifs` 命令将远程 `[homes]` 目录共享配置到空的本地目录。例如，作为 `root` 用户，你可以使用以下命令将 `/share` 目录（如果需要则创建）挂载到本地：
  ```
  # mount "//sambaserver/michael" /share -o username=root
  ```
- 13. 测试结果。你能在远程计算机上浏览主目录吗？附加：禁用 `samba_enable_home_dirs` 布尔值并重试。会发生什么？

## Samba Web 管理工具

RHEL 6 不再包含用于配置 Samba 的专用 Red Hat GUI 工具。相反，Red Hat 包含了 Samba 开发者为此目的创建的基于 Web 的管理工具，称为 SWAT，你可以从 `samba-swat` RPM 安装它。

SWAT 在标准 RHEL 6 DVD 上不可用。因此，如果 Red Hat 考试中只有这些可用，你将无法使用它为 RHCE 配置 Samba。然而，SWAT 是一个如此出色且文档完善的工具，安装和激活它的麻烦是值得的。它可以帮助你更深入地了解 Samba。

在真正的 RHEL 6 系统上，它可从 RHEL Server Optional 仓库获得，可通过 https://rhn.redhat.com 上的 Red Hat Network 账户激活。在 Scientific Linux 重建发行版（以及可能的其他重建版）上，它可从 `/etc/yum.repos.d` 目录中配置的标准仓库获得。

![](img/9139201cfcaf4292284a0eed074928e5_847_0.png)

Red Hat Network 网站 https://rhn.redhat.com 现在是“Classic Subscription Management”的接口。有关最新的 RHN 接口，请参阅 https://access.redhat.com/kb/docs/DOC-47394 上的知识库文章。

SWAT 作为扩展的 Internet 超级服务器服务安装并运行在 `/etc/xinetd.d` 目录中，如第 10 章所述。一旦安装，你可以使用以下命令激活它：

```
# chkconfig swat on

# /etc/init.d/xinetd restart
```

接下来，打开 Web 浏览器并导航到 `http://localhost:901`。你将被提示输入用户名和密码；`root` 用户账户和密码应该可以工作。身份验证确认后，你将被带到与图 15-1 所示类似的屏幕。

如果你想从远程位置访问 SWAT，请在 `/etc/xinetd.d/swat` 文件中注释掉以下指令，然后在任何现有的本地防火墙中打开 TCP 端口 `901`。

```
only_from = 127.0.0.1
```
