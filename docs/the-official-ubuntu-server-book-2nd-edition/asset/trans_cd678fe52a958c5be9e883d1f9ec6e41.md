

二进制文件包含图形和基于文本的安装程序，因此如果你的机器上安装了 X 服务器，你就可以使用图形安装程序。我假设在这台特定服务器上你没有安装，所以当你运行程序时，安装程序会提示你继续使用文本模式。安装程序首先检查系统的规格，以确保你有足够的内存和存储空间。如果不满足最低要求，安装程序将退出；但如果你高于最低要求但低于推荐规格，它只会给出警告并允许你继续。

此时安装程序基本上是非交互式的，除了初始提示输入 MySQL root 密码以及是否获取 GroundWork 软件更新通知的选项。设置完这些选项后，你只需看到进度条，软件正在解包。

## GroundWork 文件约定

了解 GroundWork 如何组织其所有文件是很有用的，因为它与大多数其他原生 Ubuntu 软件有所不同。下面我讨论平均管理员会感兴趣的核心文件和目录位置。

- **/usr/local/groundwork**  
  这是核心 GroundWork 目录。在这里你会找到所有包含的脚本和集成程序，如 Nagios、Apache 和 MySQL。
- **/usr/local/groundwork/apache2**  
  在这里你可以找到完整的 GroundWork Apache 安装，包括所有二进制文件和 Apache 配置。
- **/usr/local/groundwork/nagios**  
  所有 Nagios 配置和支持文件都位于此目录。当你提交新的 GroundWork 配置时，它会将其数据库中的设置转换为此目录内的原始 Nagios 文件。在此目录中，你还可以在 var 目录下找到 Nagios 日志文件，以及 libexec 目录中的所有包含的 Nagios 检查。

## /etc/init.d/groundwork

这是启动时启动 GroundWork 的初始化脚本，也是你可以手动启动、停止和重启服务的脚本。此脚本随后会在幕后启动或停止各个守护进程，如 Web 界面、MySQL 和 Nagios。

## 初始配置

GroundWork 安装完成后，打开 Web 浏览器并输入你的 GroundWork 主机的主机名。在我的示例中是 groundwork.example.org。在登录屏幕，<|message|>以 admin 用户名和密码 admin 登录，你将看到默认的 GroundWork 页面。GroundWork 将不同的配置和监控页面分为屏幕顶部的标签。在图 8-2 中可以看到默认的仪表板页面。首先，选择 Administration 标签。此屏幕允许你配置此机器上的用户、组和角色。通过角色你可以选择特定用户可以看到哪些菜单选项，因此如果你不希望用户能够配置 GroundWork，你可以将该用户限制为菜单中的显示选项。现在我们唯一想做的是更改 admin 密码。点击屏幕右上角的 My Preferences 链接，选择 Edit Profile，最后点击 Change Password。

![](img/304f637afcecc491b152ee8ac5afadee_337_0.png)

图 8-2 GroundWork 默认仪表板

> 注意 如果你处于 Administration 窗口中，你也可以添加自己的用户。点击 User Management 标签，然后在右窗格中点击 Create new user account 链接。填写你的用户信息，并在 Assign Roles 屏幕时务必选择 Administrators 角色。现在当你以你的用户登录时，你将拥有与管理员相同的访问级别。

## 初始主机扫描

监控系统的初始配置每个主机都令人烦恼。如果有大量主机需要监控，一次一个地将它们添加到系统中会很痛苦。GroundWork 提供了一个向导，使初始配置变得简单得多。从主标签行中选择 Auto Discovery。有几种不同的扫描模式可供选择：Interactive、Auto 和 Auto Commit。Interactive 模式会在流程的每个阶段提示你。Auto 模式会自动将检测到的每个主机添加到 GroundWork 配置中，但不会提交更改。Auto Commit 选项与 Auto 类似，但也会自动将更改提交到 Nagios。先从 Interactive 模式开始，直到你很好地掌握了其工作原理，然后如果发现你总是倾向于添加 GroundWork 检测到的主机，再尝试其他模式。

在屏幕底部你会看到定义要扫描的 IP 范围的选项。你可以在这里不仅定义要包含的 IP，还定义不希望扫描的 IP。一般来说，你至少要扫描监控服务器所在的同一子网，因此在此处添加该子网。添加子网后，取消选中 localhost 子网（127.0.1.*），以免为你的 localhost 接口添加大量条目，然后点击屏幕顶部的 Go 按钮继续。在下一屏幕确认你想继续后，GroundWork 将扫描你定义的子网中的每个 IP。当它找到特定主机时，它会扫描该主机的开放端口并尝试检测该机器上的服务。对于每个检测到的具有可用 Nagios 检查的服务，GroundWork 会自动将该服务检查添加到该主机。

扫描完成后，如果你选择了 Interactive 模式，点击屏幕底部的 Next，你将看到 GroundWork 检测到的主机的完整列表，如图 8-3 所示。如果你选择了 Auto 或 Auto Commit 模式，

