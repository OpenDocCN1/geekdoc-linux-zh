
# 配置和管理网络打印服务 537

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 538

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 539

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 540

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 541

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 542

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 543

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 544

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 545

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 546

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 547

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 548

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 549

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 550

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 551

## 第10 节 管理网络服务：DNS 和文件打印服务

通常，CUPS 服务器上可用以下资源：

+   - `/root/`。该资源的访问限制适用于所有后续资源，前提是这些资源处没有指定其他限制。
+   - `printers`。所有打印机或队列。
+   - `classes`。可用的打印机类，例如所有彩色打印机。
+   - `jobs`。CUPS 服务器上的打印作业。
+   - `admin`。这些设置涉及对服务器配置的访问。
+   - `http://localhost:631/printers`
+   - 或
`http://localhost:631/admin`

以下主题描述了如何：

+   - 使用 YaST 配置访问限制
-   为用户和组配置访问限制
-   配置

### 使用 YaST 配置访问限制

在 `YaST > 硬件 > 打印机 > 更改 > 高级 CUPS 服务器设置 > 修改权限`，你可以定义访问指令应用的顺序（先应用 `Allow` 规则再应用 `Deny` 规则，还是反之）以及默认指令。

在“权限”下，根据之前指定的顺序定义访问规则所需的实体。

访问设置存储在 `/etc/cups/cupsd.conf` 配置文件中。

这是一个示例：

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 529

...（后续文本遵循逻辑）

所有用户都可以通过输入显示选项：

```
loptions -p queue -l
```

以下是可能显示的某些示例：

`PageSize/Page Size: A3 *A4 A5 Legal Letter`

`Resolution/Resolution: 150 *300 600`

选项前的星号 `*` 表示当前设置。在上面的示例中，纸张格式为 `A4`，分辨率为 `300 dpi`。

你可以使用以下命令更改队列的选项：

```
loptions -p queue -o option=value
```

例如，将 `lp` 队列的纸张格式更改 letter，输入：

```
loptions -p lp -o PageSize=Letter
```

这些新设置的影响取决于以下因素：

+   * 如果普通用户（例如 `geeko`）输入命令，则更改将仅影响该用户。设置保存在用户目录下的 `.lpoptions` 文件中。
*   如果 `root` 输入命令，则设置将成为本地计算机上每个用户的偏好，并保存在 `/etc/cups/lpoptions` 文件中。相应的 PPD 文件将保持不变。

关于打印类型硬件无关标准选项的信息，请阅读文件 `/usr/share/doc/packages/cups/sum.html#USING_SYSTEM`。

注意

关于保存选项的信息，请阅读文件 `/usr/share/doc/packages/cups/sum.html#SAVING_OPTIONS`。

## 限制打印机访问

可以对各种 CUPS 资源的访问进行限制。

资源显示为目录（`/printers` 或 `/jobs`）。

# 528 第10 节 管理网络服务：DNS 和文件打印服务

通常，CUPS 服务器上可用以下资源：

+   - `/root/`。该资源的访问限制适用于所有后续资源，前提是这些资源处没有指定其他限制。
+   - `printers`。所有打印机或队列。
+   - `classes`。可用的打印机类，例如所有彩色打印机。
+   - `jobs`。CUPS 服务器上的打印作业。
+   - `admin`。这些设置涉及对服务器配置的访问。
+   - `http://localhost:631/printers`
+   - 或
`http://localhost:631/admin`

以下主题描述了如何：

+   - 使用 YaST 配置访问限制
-   为用户和组配置访问限制
-   配置

### 使用 YaST 配置访问限制

在 `YaST > 硬件 > 打印机 > 更改 > 高级 CUPS 服务器设置 > 修改权限`，你可以定义访问指令应用的顺序（先应用 `Allow` 规则再应用 `Deny` 规则，还是反之）以及默认指令。

在“权限”下，根据之前指定的顺序定义访问规则所需的实体。

访问设置存储在 `/etc/cups/cupsd.conf` 配置文件中。

这是一个示例：

```
<Location />
Order Deny,Allow
Allow From 127.0.0.1
</Location>
```

```
...
<Location /admin>
...
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
```

# 配置和管理网络打印服务 530

...（后续文本遵循逻辑）

## 第 10 管理网络服务：DNS 和文件打印服务

显示图 10-25 所示的网页。

![](img/39399c9366aee7ad257a7d2d6505f1a1_553_0.png)

图 10-25

通过此网页，你可以执行如管理打印机类、作业和打印机等任务。

要使用此网页上的管理选项（或 DE 中的打印机管理工具），必须将 `root` 设置为 CUPS 管理员，并加入 CUPS 管理组 `sys`，同时设置 CUPS 密码。

你可以以 `root` 用户身份通过输入以下命令来实现：

```
lpasswd -g sys -a root
```

> 有关如何将另一个用户设置为 CUPS 管理员的信息，请参阅《SLES 9 安装与管理》手册第 13.6.2 节。

## 排除 CUPS 打印系统

以下是排除 CUPS 打印系统的基本任务：

- 将日志级别设置为记录错误
- 检查访问日志 `Access Log`
- 执行基础故障排除

### 将日志级别设置为记录错误

来自 `cupsd` 的消息被写入 `/var/log/cups/error_log` 文件。默认情况下，只有查询和状态更改会被记录在文件中。

如果你想记录错误，需要更改配置文件 `/etc/cups/cupsd.conf` 中的 `LogLevel` 选项。

```
# LogLevel: 控制写入 ErrorLog 文件的消息数量
# 并且可以是以下值之一：
# debug2 记录记录所有内容。
# debug 记录几乎所有内容。
# info 记录所有请求和状态更改。
# warn 记录错误和警告。
# error 仅记录错误。
# none 不记录任何内容。
```

为了调试和故障排除，请将日志级别设置为 `debug2`。更改配置后，输入 `rcups restart` 重启 CUPS。

### 检查访问日志

`/var/log/cups/access_log` 文件记录了浏览器或 CUPS/IPP 客户端对 CUPS 守护程序的每次访问。每行都包含表 10-6 所示的字段。

表 10-6

| 字段 | 描述 |
|--- |--- |
| host | DNS 名称或 IP 地址 |
| group | 组名（CUPS 始终为 "-"） |
| user | 如果用户通过登录名和密码识别身份，则是用户名（否则为 "-"） |
| date | 当前日期 |
| method | HTTP 方法（如 GET 或 POST） |
| resource | 请求的资源 |
| version | HTTP 版本（对于 CUPS，始终为 HTTP/1.1） |
| status | HTTP 结果状态（通常为 200，但也可能是其他代码） |
| bytes | 传输的字节数 |

### 执行基础故障排除

要对 CUPS 进行基础故障排除，请执行以下操作：

- 在 `/etc/cups/cupsd.conf` 文件中将 `LogLevel` 设置为 `debug`。
- 输入 `rcupsd stop` 停止 `cupsd`。
- 通过重命名文件 `/var/log/cups/error_log` 来避免在大型日志文件中搜索（如下所示，在同一行）：

`/var/log/cups/error_log /var/log/cups/error_log-yyyymmd`

- 输入 `rcupsd start` 启动 `cupsd`。
- 重复导致问题的操作。
- 检查 `/var/log/cups/error_log` 中的消息以识别问题原因。

## 练习 10-4 配置 CUPS 网络打印服务

在一个部门内配备一台较大的打印机，比为每个工作站配备一台打印机更具经济效益。这台打印机将通过网络供几个人使用。

有多种协议可以访问此类打印机。CUps 主要使用互联网打印协议 `IPP`。

在此练习中，你将通过以下步骤在你的 SLES 9 服务器上设置并管理 CUPS 打印环境：

- 第一部分：从命令行管理打印机
- 第二部分：使用 YaST 管理打印机
- 第三部分：为 CUPS 管理员提供访问权限
- 第四部分：打印到远程 CUPS 打印机

> 你必须在练习 4.4 中设置一台打印机才能完成此练习。

![](img/39399c9366aee7ad257a7d2d6505f1a1_555_0.png)

### 第一部分：从命令行管理打印机

执行以下操作：

1. 打开终端窗口。
2. 使用 Berkeley 打印机命令向 HP LaserJet 4 打印机发送打印作业：
   a. 输入以下命令打印 `/etc/hosts` 文件：
      ```
lpr -P hplj4 /etc/hosts
```
   b. 输入 `lpq -P hplj4` 查看 `hplj4` 的打印队列。

将列出发送 hosts 文件的作业。请注意作业号。

3. 使用 System V 打印机命令向 HP LaserJet 4 打印机发送打印作业：
   a. 输入以下命令将 `/etc/hosts` 文件发送打印机：
      ```
lp -d hplj4 /etc/hosts
```
   b. 输入 `lpstat -P hplj4` 查看 `hplj4` 的打印队列。
4. 在 Konqueror 浏览器中，输入以下 URL：
`http://localhost:631/admin`
5. 输入以下内容登录：
字体 用户名：`root`
- 密码：`N033`

出现 CUPS 管理员页面。

### 第二部分：使用 YaST 管理打印机

在练习的这部分，你使用 YaST 执行某些打印任务。

执行以下操作：

1. 从 YaST 控制中心选择“硬件 > 打印机”。
出现配置对话框。
2. 选择“配置”添加新的 CUPS 打印机。
3. 选择“通过 CUPS 网络打印”，然后点击“下一步”。
4. 选择“远程 IPP 队列”，然后点击“下一步”。
5. 在“打印服务器主机”旁选择“查找”，然后选择“扫描 IPP 服务器”。
6. 从下拉列表中选择 `da1.digitalairlines.com`。

如果下拉列表中没有 `da1.digitalairlines.com`，请在字段中输入 `da1.digitalairlines.com`。
7. 在“远程队列名称”字段旁选择“查找”，选择 `da1` 上的默认队列。
8. 选择“测试远程 IPP 访问”测试与打印服务器的连接性。

### 第三部分：为 CUPS 管理员提供访问权限

在通过浏览器管理打印机之前，你需要为每个用户创建 CUPS 密码。

执行以下操作：

1. 确保你在终端窗口中切换到 `root` 用户。
2. 输入以下命令为 `root` 用户创建 CUPS 密码：
`lpasswd -r root`
3. 两次输入密码 `N033`。
4. 在 Konqueror 浏览器中，输入以下 URL：
```
http://localhost:631/admin
```
5. 输入以下内容登录：
字体 用户名：`root`
- 密码：`N033`

### 第四部分：打印到远程 CUPS 打印机
