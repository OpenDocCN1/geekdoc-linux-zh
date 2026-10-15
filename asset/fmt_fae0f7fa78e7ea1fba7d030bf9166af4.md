
```php
<?php
// 连接到此系统上的 MySQL 服务器
mysql_connect("localhost", "admin", "somepassword")
or die("Unable to connect to SQL server");

// 使用 etcpasswd 数据库
mysql_select_db("etcpasswd")
or die("Unable to select database");

// 获取 users 数据库的列名列表
$result = mysql_list_fields("etcpasswd", "users");

// 获取 login 包含字母 "o" 的所有字段
$query = mysql_query("select * from users where login like '%o%");

// 获取返回行数
$affected = mysql_num_rows($query);

if(!$affected) {
    echo "No users with 'o' in their name returned";
} else {
    // 显示列名
    echo "<table align='center' border=1>";
    echo "<tr><th>" . mysql_field_name($result,0) . "</th></tr>";
    echo "<tr><td>" . mysql_field_name($result,4) . "</td></tr>";
    echo "<tr><td>" . mysql_field_name($result,5) . "</td></tr>";
    // 显示每一行
while($row=mysql_fetch_row($query)) {
echo "<tr><td>$row[0]</td></tr>";
echo "<tr><td>$row[4]</td></tr>";
echo "<tr><td>$row[5]</td></tr>";
}

echo "</table>\n";

// 释放与查询相关的内存
mysql_free_result($query);
?>
```

生成的网页将类似于图 2 所示。

**图 2 通过 PHP 查询 MySQL 的结果**

![](img/36cca419b7fb93321343e40d77521ed5_20_0.png)

13T3-1100A-WWEN

基于 Apache、PHP、MySQL 和 HTTP 的 Linux Web 解决方案

### 3.2.6 验证 HTTP 是否工作

完成第 3.1.5 节描述的 `rundig.sh` 脚本后，打开 URL `http://127.0.0.1/search.html`。该 URL 应显示搜索查询页面，如图 3 所示。

**图 3. HTTP 搜索页面**

![](img/36cca419b7fb93321343e40d77521ed5_21_0.png)

13T3-1100A-WWEN

基于 Apache、PHP、MySQL 和 HTTP 的 Web 解决方案

输入查询并查看结果。`rundig.sh` 脚本应该索引了 Apache 手册的本地副本。尝试搜索“server”。图 4 显示结果示例。

## 图 4. HTTP 搜索结果

![](img/36cca419b7fb93321343e40d77521ed5_22_0.png)

13T3-1100A-WWEN

# 4 管理 Apache 服务器

安装后，Apache Web 服务器应该无人值运行一段时间。然而，监控服务器以确保其运行良好是明智的。

## 4.1 监控日志文件

为了确保系统不会耗尽磁盘空间，请监控持有访问和错误日志的磁盘分区。默认情况下，Apache 服务器将这些日志存储在 `/usr/local/apache/log`。

日志文件的增长速度差异很大，日志大小取决于访问频率以及请求的 URL 类型。虽然你可以假设访问日志约为 150 字节数据，但使用取决于 Web 内容目录的结构和命名规范。

`logrotate` 工具旨在简化生成大量日志系统的管理工作。它允许对日志文件进行自动轮转、压缩、删除和发送。每个日志可以每天、每周或在过大时处理。如果你的 Linux 发行版不包含 `logrotate`，你可以从以下站点获取它：

```
ftp://ftp.redhat.com/pub/linux/RedHat/redhat/code/logrotate/
```

或者许多 RedHat 镜像站之一。

## 4.2 监控网络连接

某些第三方开源 Apache 模块限制了到特定目录的并发连接数，或者对于超过“每秒字节”下载速率的用户限制响应。

ApacheWeek 维护了一个限制 Web 域访问的模块列表。更多信息，请访问他们的网页 `http://www.apacheweek.com/features/modulesoup`。

## 4.3 监控系统性能

有很多开源工具可以监控通用系统特别是 Web 服务器。

### 4.3.1 状态显示

`mod_status` 模块传递有关 Apache Web 服务器总体运行的信息，例如，它的运行时间以及当前请求计数、Apache 子进程、总访问量和发送的字节数

默认情况下，Apache 配置文件 (`httpd.conf`) 禁止从所有地方访问状态报告。

# 基于 Apache、PHP、MySQL 和 http:// 的 Linux Web 解决方案

若要允许访问，请取消 `Allow` 行的注释，并编辑互联网提供商 (`isp.com`) 的位置，以包含一个可以访问该 URL 的系统或域名列表。

```
#允许服务器状态报告，URL 为 http://servername/server-status
# 将 "your.domain.com" 修改为您的域名以启用。
#<Location /server-status>
# SetHandler server-status
# Order deny,allow
# Deny from all
# Allow from your.domain.com
</Location>
```

如需了解更多信息，请参阅 Apache 文档：

`http://www.apache.org/docs/mod/mod_status_status.html`

### 4.3.2 配置信息

`mod_info` 模块返回有关服务器配置的全面信息；这包括配置文件中所有安装的模块和指令。

默认情况下，Apache 配置文件 (`httpd.conf`) 禁止从所有地方对 URL 进行 Web 访问。取消并更改 `Allow` 行，以包含一个允许访问该 URL 的系统或域名列表。

```
# 允许远程服务器配置报告，URL 为
# http://servername/server-info (需要加载 mod_info.c)
# 将 "your.domain.com" 修改为您的域名以启用。

#<Location /server-info>
# SetHandler server-info
# Order deny,allow
# Deny from all
# Allow from your.domain.com
</Location>
```

如需了解更多信息，请参阅 Apache 文档：

`http://www.apache.org/docs/mod/mod_info.html`

### 4.3.3 监控工具

监控工具包括以下内容：

- 大型系统和网络监控器
- `mon`，服务守护进程监控是一个基于 Web 的监控和通知包。

大型系统和网络监控器是一个基于 Web 的监控和通知包。通过这些监控工具，网站运营人员可以集中观察远程 UNIX 和 Microsoft NT 系统。

监控器由几个客户端组成：本地测试系统状况和网络可用性。这些客户端将报告发送到显示和解析网页，通知系统管理员 Web 服务器、DNS、NNTP (USENET 新闻)、SMTP 和 POP3 的可用性。

系统状态报告包括 CPU 使用率、系统日志消息、关键系统进程运行以及磁盘空间等信息。

# 基于 Apache、PHP、MySQL 和 http://Dig 的 Linux Web 解决方案

访问网站 `http://bb4.com` 下载源码、查看演示或获取更多信息。

`mon`，服务监控守护进程是一个通用的资源监控系统，旨在检查网络服务可用性、服务器问题和环境条件等状况。

资源监控可以视为两个独立的任务：状况的测试以及在失败时触发某种操作。`mon` 的设计是将测试和执行操作的任务作为独立程序。`mon` 被实现为一个调度器，它执行监控器（测试状况），并在监控器失败时调用相应的警报。访问网站 `http://www.kernel.org/software/mon` 获取更多信息、示例页面并下载源码。

## 4.4 分析日志文件

### Webalizer
