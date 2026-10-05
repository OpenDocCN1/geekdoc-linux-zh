

3.3. 使用密码 `student` 以学生用户身份登录。

你现在已以普通用户身份登录，具有最小权限。

- 4. 在 Web 控制台界面内验证你的当前权限。

- 4.1. 点击左侧导航栏中的“Terminal”（终端）进入终端。将打开一个已以 student 用户身份登录的终端会话。使用 `id` 命令确认嵌入式终端中的命令执行是否正常。

```
[student@servera ~]$ id
uid=1000(student) groups=1000(student), 10(wheel)
context=unconfined_u:unconfined_r:unconfined_t:s0
```

- 4.2. 点击左侧导航栏中的“Accounts”（账户）来管理用户。将鼠标指针悬停在左角的“New Account”（新账户）按钮上。注意学生用户不允许创建新账户。

- 4.3. 点击“Student User”（学生用户）链接。在用户账户详情页上，注意该用户仅允许设置新密码或授权 SSH 公钥。

- 4.4. 点击右上角的“Student User”下拉菜单。从下拉菜单中选择“Log Out”（注销）。

- 5. 以管理员权限访问 Web 控制台。

- 5.1. 再次以学生用户密码 `student` 登录 Web 控制台界面，但这次勾选“Reuse password for privileged tasks”（特权任务重用密码）复选框。

- 5.2. 要验证管理员访问，确认 Web 控制台右上角的 Student User 账户旁边显示了“Privileged”（特权）标签。

- 6. 要查看系统统计信息，点击左侧导航栏中的“System”（系统）。

此页面显示基本操作系统的统计信息，例如：当前负载、磁盘使用情况、I/O 和网络流量。

- 7. 要检查系统日志，点击左侧导航栏中的“Logs”（日志）。

此页面显示系统日志。使用左上角的按钮根据日期和日志严重性类型修改日志条目的显示方式。

- 7.1. 点击“Severity”（严重性）下拉列表并选择“Everything”（全部）。

- 7.2. 根据当前日期，点击列表中的任何日志条目。日志条目详情页将打开有关该事件的附加信息，例如主机名、SELinux 上下文以及该条目对应的进程 PID 。

- 为现有的网络接口设备添加第二个 IP 地址。

8.1. 点击左侧导航栏中的“Networking”（网络）。
此页面显示 servera 当前网络配置的详情，以及实时网络统计信息、防火墙配置和与网络相关的日志条目。

- 8.2. 滚动到“Interfaces”（接口）部分并点击 `ens3` 网络接口名称行。
详情页显示实时网络统计信息以及该网络接口的当前配置。

- 8.3. 点击“Address 172.25.250.10 via 172.25.250.254”链接。
打开一个 IPv4 Settings 窗口，你可以在其中更改网络接口配置。

- 8.4. 在 IPv4 Settings 窗口中，点击“Manual”（手动）旁的 `+` 号。

- 8.5. 在“Address”文本框中输入 `172.25.90.99` 作为 IP 地址。

- 8.6. 在“Prefix length or Netmask”文本框中输入网络掩码值 `24`。

- 8.7. 点击“Apply”（应用）保存新的网络配置。
注意新配置已立即生效。新的 IP 地址在 IPv4 行中可见。

- 创建一个用户账户。

9.1. 点击左侧导航栏中的“Accounts”（账户）。

- 9.2. 点击“New Account”（新账户）。

- 9.3. 在“Create New Account”窗口中添加以下详细信息：

| FIELD | VALUE |
| --- | --- |
| Full Name | manager1 |
| User Name | manager1 |
| Password | redh@t123 |
| Confirm | redh@t123 |

9.4. 点击“Create”（创建）。

- 10. 在 Web 控制台内访问终端会话，将 manager:1 用户添加到 wheel 组。

10.1. 点击左侧导航栏中的“Terminal”（终端）。

- 10.2. 使用 `id manager1` 命令查看 manager1 用户的组组成情况。

```
[student@servera ~]$ sudo id manager1
```

uid=1001(manager1) gid=1001(manager1) groups=1001(manager1)

- 10.3. 使用 `usermod -ag wheel manager1` 命令将 manager1 添加到 wheel 组。

```
[student@servera ~]$ sudo usermod -ag wheel manager1
(sudo) password for student: student
[student@servera ~]$
```

- 10.4. 使用 `id manager1` 命令验证 manager1 是否为 wheel 组成员。

```
[student@servera ~]$ id manager1
uid=1001(manager1) gid=1001(manager1) groups=1001(manager1),10(wheel)
```

- 11. 启用并启动内核进程计数 (psacct) 服务。
11.1. 点击左侧导航栏中的“Services”（服务）。
- 11.2. 滚动查看“System Services”列表直到找到“Disabled”（已禁用）部分。找到并点击“Kernel process accounting”（内核进程计数）链接。
- 11.3. 点击“Enable”（启用）。
- 11.4. 点击“Start”（启动）。
服务已启用并启动。

- 12. 从 Web 控制台注销。

- 13. 从 servera 注销。

```
[student@servera ~]$ exit
```

## 从红帽支持获取帮助

### 目标
完成本节后，你应该能够：

## 访问客户门户的资源
Products & Services 提供了产品中心，这些页面提供了特定产品的评估、概述、入门指南和其他产品支持信息。你还可以访问 Red Hat 产品的文档、知识库直接链接以及有关如何联系支持的信息。

- 访问官方文档。
- 提交支持案例。
- 管理你的订阅和权限。
- 获取优化系统的下载。

网站部分部分对所有人开放，而其他部分仅限拥有订阅的客户。请注意，如果你属于某个组织，组织管理员可以限制对该页面的访问。

## 熟悉客户门户
导览是一个非常有用的工具，可以帮助发现门户提供的所有功能并充分利用其价值。

## 欢迎来到红帽客户门户
第一个窗口有两个选项：CLOSE（关闭）和 NEXT（下一步）。

## 顶部导航栏
客户门户主页顶部导航栏下方有菜单，你可以通过它们导航到提供的四类资源：

- SUBSCRIPTIONS（订阅）
- DOWNLOADS（下载）
- CONTAINERS（容器）
- SUPPORT（支持）

Subscriptions 打开一个新页面，你可以在其中管理已注册系统和订阅。它列出了相关的错误信息，并允许你创建激活密钥以便在注册系统时获取正确的订阅权限。访问此页面。

Downloads 打开一个新页面，让你访问产品下载并对没有权限的产品申请评估。

Support Cases 打开一个新页面，允许你通过案例管理系统创建、跟踪和管理支持案例，前提是你的组织授权了该访问权限。

