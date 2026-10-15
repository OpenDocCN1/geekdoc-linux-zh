
`-A` 选项允许在控制台上显示告报，而 `-K` 选项控制告报如何记录到日志目录中。你应该尝试不同的显示格式，找到一个在对 Snort 主机负担最小的情况下提供足够信息的格式。对于日常操作，你可能希望在日志文件中中使用 `fast` 告报，它们看起来就像使用 `console` 选项发送到控制台的那些一样。这里列出了可用的告报模式和日志格式以供参考。

### 告报模式和日志格式

- `-a` Console 以以下格式记录到控制台：

```
10/12-21:29:35.91189 [**: [1:0:0] TEST rule [**] [Priority: 0] {ICMP}
192.168.1.99 -> 192.168.1.103
```

- `-A fast` 在控制台中记录日志，但将告报写入 `/snort/alert` 文件，不输出到控制台。

- `-A full` 以以下格式记录到 `/snort/alert` 文件：

```
[**] [1:0:0] TEST rule [**] [Priority: 0] {ICMP}
192.168.1.99 -> 192.168.1.103
```

## 安装和配置 Snort 及其插件 • 第 5 章

> 如果你安装的包没有包含 `/snort/schemas/` 目录，你可以下载源码包并从那里提取该目录。在 Fedora Core 5 中，由于某些原因，带有 MySQL 支持的 Snort 并没有包含 schemas 目录。

- 9. 输入以下命令验证 Snort 数据库中是否创建了 MySQL 表。你应该能看到与示例所示类似的输出：

```
mysql -u root -
show databases;
```

+----------------------+
| Database             |
+----------------------+
| mysql                |
| snort                |
| test                 |
+----------------------+

```
use snort;
show tables;
```

+----------------------+
| Tables_in_snort      |
+----------------------+
| data                 |
| detail               |
| encoding             |
| event                |
| icmphdr              |
| iphdr                |
| opt                  |
| reference           |
| reference_system    |
| schema               |
| sensor               |
| sig_Class           |
| sig_reference        |
| signature            |
| tcphdr             |
+----------------------+
udphdr

exit

数据库列表本身并不重要，只要 Snort 数据库存在即可（当然）。表列表必须准确。如果缺少任何一个表，Snort 在运行时将会生成错误。

- 10. 安装 `php-gd`，它用于在 BASE 中生成图表。在 Fedora Core 5 上，你只需输入 `yum install php-gd`。

- 11. 安装 ADODB，这是一个用于 PHP 的数据库抽象库。在 Fedora 上，你只需输入 `yum install php-adodb`。

- 12. 现在是配置 BASE 本身了。编辑 `/usr/share/base-php4/base_conf.conf` 文件，确保以下行配置了适用于你配置的路径和设置。

```
$BASE_path = '/base';
$DBlib_path = '/usr/share/odbc/';
$DBtype = 'mysql';
$alert_dbname = 'snort';
$alert_host = 'localhost';
$alert_port = '';
$alert_user = 'snort';
$alert_password = 'snortpass'
```

你不应该能够通过以下 URL 访问 BASE 页面：

http://localhost/base/.

![](img/33fc180c04c8f96c022bce6e62ae12fd_184_0.png)

![](img/33fc180c04c8f96c022bce6e62ae12fd_185_0.png)

第一次启动 BASE 时，没有任何数据库表被创建。你会看到类似于图 5.3 所示的页面。

### 图 5.3 BASE 设置

![](img/33fc180c04c8f96c022bce6e62ae12fd_185_1.png)

- 13. 点击 Setup（设置）页面链接。

- 14. 点击右侧的 Create BASE AG 按钮。你会看到如图 5.4 所示的多个成功消息。

### 图 5.4 BASE 成功

| 分析与安全引擎 (BASE) | | |
| Home（首页） | Search（搜索） | [ Back（返回） ] |
| 成功创建 acid_ag |
| 成功创建 acid_ag_alert |
| 成功创建 acid_cache |
| 成功创建 acid_error |
| 成功创建 base_roles |
| 成功插入了身份验证用户角色 |
| 成功插入了匿名用户角色 |
| 成功插入了告警组编辑器角色 |
| 成功创建 base_users |
| 操作 | 描述 | 状态 |
| BASE 表 | 添加表以扩展 Snort 数据库以支持 BASE 功能 | DONE（完成） |
| 底层 Alert DB 已配置 BASE。 | |
| 可选数据库权限 | | |
| 为了支持 Alert（选择性清理）永久删除告警（从数据库中）以及 DNS/who 查找缓存，数据库用户 "snort" 必须对数据库 "snort@localhost" 拥有 DELETE 和 UPDATE 权限 |
| 转到主页使用应用程序。 | |
| 告警组维护 | 缓存与状态 | 管理 |
| BASE 1.2.6 (iteration) 由 Kevin Johnson 和 BASE 项目团队开发 | | |
| 基于 ACID 由 Datslyn 构建 | | |
| 1 秒内加载完成 | | |

- 15. 点击 **Main Page**（主页）链接。这应该带你进入图 5.5 所示的 BASE 主界面。

尽管此窗口可能看起来不太华丽，但你可以发现其中丰富的信息。例如，通过点击 **Today's**（今日）告警右侧，你可以获得唯一告警的排序列表、所有告警的列表，或者按源 IP 地址或目的 IP 地址排序的列表。这些功能可以让你快速查看特定的告警，而无需通过菜单。左侧标题提供了大部分告警信息。图 5.5 所示的窗口打开后，你可以看到图 5.6 所示的**15 告警**。

### 图 5.5 BASE 主页

| 操作 | 描述 | 状态 |
|---|---|---|
| BASE 表 | 添加表以扩展 Snort 数据库以支持 BASE 功能 | DONE |
| 底层 Alert DB 已配置 BASE。 | | |
| 可选数据库权限 | | |
| 为了支持 Alert（选择性清理）永久删除告警（从数据库中）以及 DNS/who 查找缓存，数据库用户 "snort" 必须对数据库 "snort@localhost" 拥有 DELETE 和 UPDATE 权限 | | |
| 转到主页使用应用程序。 | | |
| 告警组维护 | 缓存与状态 | 管理 |
| BASE 1.2.6 (iteration) 由 Kevin Johnson 和 BASE 项目团队开发 | | |
| 基于 ACID 由 Datslyn 构建 | | |
| 1 秒内加载完成 | | |

*纠正：原文中表格内容较为混乱，以下是第 14 步后续内容的逻辑翻译：*

- 14. Click the Create BASE AG button on the right-hand side. You will see several success messages as shown in Figure 5.4.

### Figure 5.4 BASE Success

| 分析与安全引擎 (BASE) | | |
| Home（首页） | Search（搜索） | [ Back（返回） ] |
| 成功创建 acid_ag |
| 成功创建 acid_ag_alert |
