
5. 对于数据库中的“Base for users（用户基准）”，输入：`ou=Users,dc=ldap,dc=corp,dc=com`

6. 对于数据库中的“Base for groups（组基准）”，输入：`ou=Groups,dc=ldap,dc=corp,dc=com`

7. 对于数据库中的“Group Membership（组关系）”，输入：`ou=Groups,dc=ldap,dc=corp,dc=com`

8. 对于服务器中的“Encryption method（加密方法）”，选择“MD5”。

9. 对于服务器中的“Users to add（要添加的用户）”，选择“Create（创建）”。

10. 最后，点击“Save（保存）”。

## 用于 OpenLDAP 的其他图形化界面

作为一个一站式工具，Webmin 并不是配置 Linux 许多方面的最佳选择。然而，对于特定的 LDAP 任务，有一些备选方案，专门用于处理您的日常 LDAP 任务。由于这些软件包都不在 Fedora 内部，每个包都有自己的安装方法，因此请务必仔细阅读下载页面上的注意事项。以下是关于我们安装和运行的一些见解：

- Luma: http://luma.sourceforge.net/ 因为我当时使用的是 GNOME 桌面，我发现 Luma 用起来有点笨拙。它拥有预装插件，可以独立于 LDAP 数据库运行。我无法无法创建 OU 或在 OU 之间移动用户。安装此包需要安装 KDE 开发工具以及最新版本的 Python 脚本语言。如果你已经在使用 KDE，你可能会觉得安装起来比我当时时要简单，但你仍然需要安装 KDE 开发库以及可能需要升级 Python。

- Directory administrator: http://diradmin.open-it.org/index.php 我尝试为 RedHat 9 安装 rpms，但没有成功。根据他们的建议，我重新下载了整个包，并尝试从该源码创建一个 rpm。这失败了。我尝试从源码编译整个包。这成功了，但我找不到图标。一旦我创建了一个符号链接来帮助程序找到图标，它就运行了，并带有一个迷人的启动向导。运行后，界面非常整洁，允许我更改用户的各种属性（包括 Unix 和 Windows 属性），但我无法在 LDAP 中创建 OU 或移动用户。总体印象是：比 Webmin 模块好，但无法创建 OU 是一很遗憾的。

- PHPLDAPadmin: http://www.phpldapadmin.com/ 这需要你先安装并运行 Apache Web 服务器。我没有尝试测试它，但网站上有一个非常精彩的在线演示，真实地展示了这个工具。该工具允许管理员创建 OU 以及 Windows 和 Linux 用户账户以及许多其他 LDAP 对象。只需 50 美元，这看起来物超所值，并且包含了支持和用户社区。总而言之，它看起来像是一个真正的赢家。

- LDAP Administrator 3.1: http://www.ldapadministrator.com 这里有一个转折：一个管理 OpenLDAP 的 Windows 应用程序。Softferra 的 LDAP Administrator 3.1 就是这样。它可以管理 Active Directory，所以是一个一站式工具。它有点偏极客——你必须熟悉想要管理的特定属性——但它有一些很棒的报告功能，界面也无可比拟。许可证费用为 215 美元，非常值得。如果你试图同时管理 Active Directory 和 OpenLDAP（或其他 LDAP 服务器），请看看这个。他们还有一个 100% 免费的工具，允许对 LDAP 目录进行只读检查。

## 第 2 章 Linux 认证服务

你收到的响应应该以以下行结束：

```
nur1:x:505:503:Nurse One:/home/nurse1:/bin/sh
nur2:x:506:503:Nurse Two:/home/nurse2:/bin/sh
do1:x:507:504:Doctor One:/home/doctor1:/bin/sh
do2:x:508:504:Doctor Two:/home/doctor2:/bin/sh
```

如果 `getent passwd` 没有列出护士和/医生账户：

- 尝试 `ldapsearch -x` 命令。在输出的末尾，你应该看到关于护士和医生账户的信息。如果是这样，请务必重读该章节（并在过程中进行验证）“登录服务器时利用 LDAP 认证”。

- 如果 `ldapsearch` 没有列出新账户，那么你可能在 Webmin 管理期间收到了错误。返回并检查“初始化 LDAP 数据库”部分中的工作内容。

## 将 Linux 客户端认证到 OpenLDAP 服务器

接下来，你需要确定是否可以让你的 Linux 客户端系统 `LinCli1` 使用 `LinServer1` 上的 LDAP 服务进行认证。为了实现这一点，你将配置 `LinCli1` 向你的服务器数据库请求认证。

早些时候，你配置了服务器（`LinServer1`）使用其自身的 LDAP 服务进行认证。现在，你告诉 `LinCli1` 使用 `LinServer1` 进行 LDAP 查询。

要让 Linux 客户端通过 LDAP 进行认证：

1. 在 `LinCli1` 上，从应用程序菜单中选择 系统设置 (System Settings) ➤ 认证 (Authentication)。将出现“认证配置 (Authentication Configuration)”。

2. 你将默认位于“用户信息 (User Information)”选项卡。勾选“启用 LDAP 支持 (Enable LDAP Support)”。

3. 点击“配置 LDAP (Configure LDAP)”按钮。出现“LDAP 设置 (LDAP Settings)”对话框。首先，勾选“使用 TLS 加密连接 (TLS to encrypt connections)”框框。然后将 LDAP 搜索基 DN 设置为 `dc=ldap,dc=corp,dc=cm`，并将 LDAP 服务器名称设置为 `linserver1.corp`。

4. 点击“确定”按钮返回“认证配置 (Authentication Configuration)”对话框。

5. 选择“认证 (Authentication)”选项卡并勾选“启用 LDAP 支持 (Enable LDAP Support)”。然后点击出现的“配置 LDAP (Configure LDAP)”对话框，如图 2.11 所示。再次勾选“使用 TLS 加密连接 (TLS to encrypt connections)”框框，并将 LDAP 搜索基 DN 设置为 `dc=ldap,dc=corp,dc=cm`，并将 LDAP 服务器名称设置为 `linserver1.corp`。

6. 点击“确定”按钮返回“认证配置 (Authentication Configuration)”对话框。

接下来，你需要确定是否可以让你的 Linux 客户端系统 `LinCli1` 使用 `LinServer1` 上的 LDAP 服务进行认证。为了实现这一点，你将配置 `LinCli1` 向你的服务器数据库请求认证。

早些时候，你配置了服务器（`LinServer1`）使用其自身的 LDAP 服务进行认证。现在，你告诉 `LinCli1` 使用 `LinServer1` 进行 LDAP 查询。

要让 Linux 客户端通过 LDAP 进行认证：

1. 在 `LinCli1` 上，从应用程序菜单中选择 系统设置 (System Settings) ➤ 认证 (Authentication)。将出现“认证配置 (Authentication Configuration)”。

2. 你将默认位于“用户信息 (User Information)”选项卡。勾选“启用 LDAP 支持 (Enable LDAP Support)”。

3. 点击“配置 LDAP (Configure LDAP)”按钮。出现“LDAP 设置 (LDAP Settings)”对话框。首先，勾选“使用 TLS 加密连接 (TLS to encrypt connections)”框框。然后将 LDAP 搜索基 DN 设置为 `dc=ldap,dc=corp,dc=cm`，并将 LDAP 服务器名称设置为 `linserver1.corp`。

4. 点击“确定”按钮返回“认证配置 (Authentication Configuration)”对话框。

5. 选择“认证 (Authentication)”选项卡并勾选“启用 LDAP 支持 (Enable LDAP Support)”。然后点击出现的“配置 LDAP (Configure LDAP)”对话框，如图 2.11 所示。再次勾选“使用 TLS 加密连接 (TLS to encrypt connections)”框框，并将 LDAP 搜索基 DN 设置为 `dc=ldap,dc=corp,dc=cm`，并将 LDAP 服务器名称设置为 `linserver1.corp`。

6. 点击“确定”按钮返回“认证配置 (Authentication Configuration)”对话框。

### 认证到 OpenLDAP
