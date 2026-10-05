

## 第三步：禁用旧主服务器

10.3.3.3 在 HP-UX 上，禁用 NIS 主服务器最简单的方法是通过 SAM。启动 SAM，选择 Networking and Communications（网络与通信），然后点击 NIS 图标。进入 NIS 配置界面（见图 10–10）。从菜单栏中选择 Actions（操作）→Disable Server（禁用服务器）。要将系统变为新主服务器（Windows 2000 系统）的 NIS 客户端，选择 Actions→Disable Client（禁用客户端），然后选择 Actions→Set Domain Name（设置域名）。将域名设置为迁移过程中创建的新新域名。在我的案例中，我将域名设置为 mydomain 而不是 book.local。然后，运行 Actions→Enable Client（启用客户端）。

![](img/1c1e7552b53cca888836b6c6895bdb48_180_0.png)

图 10–10 SAM 中的 NIS 配置界面。

## 10.3.4 迁移过程中的问题

10.3.4.1 UID 由于我的测试平台非常小，没有什么需要担心的，所以我毫无顾忌地运行迁移。我遇到的唯一问题是 Active Directory 账户 dylan 似乎没有保留该用户的 UNIX UID（值为 102）。在图 10–11 中，我展示了 dylan 账户的 UNIX Attributes（Unix属性）选项卡。由于我选择不覆盖 Windows 对象的任何数据，UID 被设置了一个不同的数字。结果是，虽然我可以以用户 dylan 登录 HP-UX 系统（在将主服务器转换为客户端后），但我遇到了文件权限问题。将 Active Directory 中 dylan 的 UID 改回原始值 102 后，一切都解决了。

此外，在 HP-UX 中，用户组的默认 GID 是 20。但 Server for NIS 保留了 100 以下的 GID。因此，你必须在 Server for NIS 中将 GID 改为100以上的的数字，并确保 name service switch（名称服务切换）在某些时刻查询文件。如果你想确保你的名称服务切换正常工作，请使用 nsquery 工具。例如：

```bash
# /usr/contrib/bin/nsquery group users
```

对组策略使用 "files" nis"。

```
Searching /etc/group for users
Group name: users
Group Id: 20
Group membership: root
Switch configuration: Terminates Search
```

注意，nsquery 找到了 GID 为 20 的 users 组，因为名称服务切换首先查询 /etc/group。

![](img/1c1e7552b53cca888836b6c6895bdb48_181_0.png)

图 10–11 UNIX Attributes 选项卡。运行 Start→Programs→Administrative Tools→Active Directory Users and Computers。然后右键点击用户并选择 Properties（属性）。

## 10.3.4.2 密码

由于 dylan 账户已存在于 Active Directory 中，该账户的 UNIX 密码被设置为与 HP-UX 系统上的密码相同。然而，dylan 的 Windows 2000 密码并没有。为了同步密码，我以 dylan 的身份登录我的 Windows-2000 服务器并更改了密码：（在默认的域控制器策略对象中，我必须授予用户组本地登录的权限才能执行此）。结果是两个密码都更改了，并且 NIS 密码被推送到 HP-UX 客户端。

然而，当我以 dylan 的身份登录 hpux/ 时，我使用 ypasswd 更改了 NIS 密码：

```bash
$ ypasswd
Changing password for dylan on NIS server
Old NIS password:
New password:
Re-enter new password:
NIS (YP) passwd/attributes changed on w2kserv, the master NIS server.
```

确实，NIS 密码更改了。但是，Windows 2000 密码并没有变。只有通过安装并配置 SFU 中独立的密码同步工具才能实现双向同步。

## 10.3.4.3 创建新用户

在迁移期间，迁移向导创建了一个新的 Windows 用户，因为在迁移时没有对应的用户，该用户在 Active Directory 中的 UNIX 密码将与现有的 UNIX 密码相同。但是，用户将在下次登录 Windows 时被更改密码。

由于 Windows 2000 域控制器现在是 NIS 主服务器，你可以使用 Active Directory Users and Computers 工具为 Windows 和 UNIX 客户端创建新用户。如果你这样做，则只会设置 Windows 密码；不会有 NIS 密码。换句话说，登录 Windows 需要密码；而登录 UNIX 客户端则不需要。正如我们所看到的，登录 UNIX 并使用 passwd 将设置域控制器上的 NIS 密码，同步密码的唯一方法（除非你使用密码同步工具）是让用户登录 Windows 客户端系统并在那里更改密码。

## 10.3.4.4 主目录

如果你在运行 Server for NIS 的域控制器上创建新用户，该用户将有一个主目录，默认映射到迁移的 passwd 映射。例如，如果你的 UNIX 主目录在 /home。Active Directory 将在其 UNIX Home Directory 属性中指定 /home/username。那么，这些主目录在哪里查找？嗯，除非你使用 NFS 或 Common Internet File System (CIFS) 将其集中，你必须。

## 10.3.4.5 映射管理

映射管理方面有好消息也有坏消息。好消息是你可以可以使用 Active Directory 管理你的组和主机映射。坏消息是，除非你使用 NFS 或 Common Internet File System (CIFS) 将其集中，你必须。

## 10.4 总结

如果你开始看到可能会出现一些复杂性，在本章及之前的章节中，我们看到了许多身份验证方案：本地、NIS、NTLM、Kerberos。在下一章，我们将转向文件共享。

