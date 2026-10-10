
您的 Linux 系统应该自动在 Fleet Manager 控制板中显示为新卡片。

## 网络安全监控快速课程

现在您已经安装了必要的硬件和软件，用于监控网络中的可疑活动和恶意活动。您需要能够识别问题、在事件发生时做出响应，并保持您的网络、用户和数据安全。在本节中，我们将涵盖如何配置和使用 `osquery`、`Wazuh` 以及 Security Onion Alerts Dashboard 的基础知识。

## 使用 osquery

如果您熟悉关系型数据库和结构化查询语言 `SQL`，使用 `osquery` 对您来说将非常容易。如果不熟悉，这里是基础知识。您可以在 Fleet Manager 控制板中查看 `osquery` 管理的网络中所有设备的数据。要进入控制板，请登录 `https://<security_onion_IP>/` 上的您的 Security Onion 控制台，并在管理员菜单中点击“Fleet”。

数据存储在系列数据表中，每个表包含两个或多个列，也称为元组，其中每个表包含每个设备的信息，例如主机名、IP 地址、MAC 地址、运行时间、最后关机时间等。表中的每行都对应一个特定的实体，例如计算机或笔记本电脑，或者更原子的东西，例如设备上的特定用户账户。例如，`users` 表看起来类似于表 10-1。

表 10-1：osquery 用户表

| UID | GID | UID_Signed | GID_Signed | Username | Description |
|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | testuser | 一个测试用户账户 |

`Username` 列的第一行数据属于设备上的 `testuser` 账户。这些表中的每一个都与数据库中的其他一个或多个表，共 200 多个相关。这些表及其关系允许您对每个受管理设备的详情和状态执行强大的查询。

我们可以使用名为 `SQL` 的查询语言对这些数据提问，`SQL` 是一种用于访问和操作数据库的高级语言。`SQL` 查询如下所示：

```
SELECT c1, c2 FROM tablename
```

在此查询中，大写的命令 `SELECT` 和 `FROM` 表示您想要执行的操作——在这种情况下，是从表 `tablename` 中请求列第 1 列和第 2 列的数据，由 `c1` 和 `c2` 参数表示。

在实践中，该查询看起来如下：

```
SELECT username FROM users

SELECT * FROM users
```

第一条命令返回显示给运行查询的用户 `users` 表中存在的所有用户名，而不包含其他列。第二条命令返回 `users` 表中所有 `*` 的列和行。

> **注意** 有多种 `SQL` 命令可以不同的方式检索数据；详情请参阅 `https://www.sqtutorial.org/sql-cheheet/` 上的 `SQL` 速查表。另见 `https://osquery.io/` 上的 `osquery` 文档获取所有可用表及其数据。

Fleet 在您的 Fleet 控制板中存储了许多查询。点击页面左侧的 **Query** 菜单，见图 10-6。

![](img/8fad00e2c75135eb78018c62b7973377_246_0.png)

**图 10-6：** Fleet Manager 中存储的 SQL 查询

从此菜单，您可以浏览可用查询，或使用页面顶部的搜索栏搜索特定查询。一旦确定了想要运行的查询，点击选择它，然后点击右侧的 **RUN** 按钮。在执行查询之前，您需要从下拉菜单中选择设备。查询完成后，Fleet 将底部向您展示结果。

这些是一些很好的开始点：

- **users**：有助于识别不应存在的用户账户
- **browser**：显示所有浏览器插件
- **chrome_extension**：专门查找 Chrome 插件
- **crontab**：识别 Linux 上的计划任务
- **disk_free_pct**：识别磁盘空间低的设备
- **installed_applications**：识别潜在的恶意应用程序

Hosts 控制板一目了然显示每个设备的详情，见图 10-7。

![](img/8fad00e2c75135eb78018c62b797337_248_0.png)

10-7：Fleet 视图

您可以查看主机名、操作系统、`osquery` 版本、处理器详情、内存量、运行时间、MAC 地址以及此主机的 IP 地址。点击顶部的蓝色按钮可以轻松查询此设备。花时间熟悉可用查询，并在网上研究其他查询。尝试查看某些保存的查询并进行编辑以获取您需要的查询。

## 使用 Wazuh

我们在项目 35 中安装了 Wazuh 代理，本节将对其进行配置。`Wazuh` 允许我们查看 Security Onion 中的日志和告警，我们下一节探讨。

主要的 Wazuh 配置文件位于 Security Onion 系统上的 `/opt/so/conf/wazuh/ossec.conf`。此配置文件的每个部分都是独立的，并用如下行进行标识：

```
<!-- 忽略的文件/目录 -->
```

您可以通过查看此文件中的设置来更改 `Wazuh` 的行为，如果 `Wazuh` 对误报做出响应并阻止了您的某些良操作，这将非常有用。查看此文件以了解 `Wazuh` 监控的类型。

以下片段指定了根据已知攻击者行为已知或预期恶意的文件列表，随后是预期包含木马的一种病毒的文件，然后是要审计各种漏洞的文件和文件夹：

```
--snip--

<rootkit_files>//var/ossec/etc/shared/rootkit_files.txt</rootkit_files>

<rootkit_trojans>//var/ossec/etc/shared/rootkit_trojans.txt</rootkit_trojans>

<system_audit>//var/ossec/etc/shared/system_audit_rcl.txt</system_audit>

<system_audit>//var/ossec/etc/shared/system_audit_ssh.txt</system_audit>

<system_audit>//var/ossec/etc/shared/cis_rhel7_linux.txt</system_audit>

--snip--
```

这些文件中的每一个都包含 `Wazuh` 将监控的项列表。如果代理在设备上发现与 `rootkit_files.txt` 文件中的行为或设置匹配的文件或配置，它将采取行动修复该威胁。

如果你不想让执行该操作，请在配置文件中使用 `#` 注释或删除该行。

当你为了持续更新和补丁 Security Onion 或其他系统而更新 `Wazuh` 时，如 `rootkit_files.txt` 等配置文件也可能会收到更新。这确保了当新威胁被识别并公开失陷指标 `IOC` 时，你的网络能够保持保护。为了避免丢失对这些文件所做的任何更改，请考虑创建新的自定义配置文件，例如 `my_custom_trojans.txt`，并在 `ossec.conf` 文件中添加对此文件的引用，如下所示：

```
--snip--

<rootkit_files>//var/ossec/etc/shared/rootkit_files.txt</rootkit_files>

<rootkit_trojans>//var/ossec/etc/shared/rootkit_trojans.txt</rootkit_trojans>

<rootkit_trojans>//var/ossec/etc/shared/my_custom_trojans.txt</rootkit_trojans>

--snip--
```
