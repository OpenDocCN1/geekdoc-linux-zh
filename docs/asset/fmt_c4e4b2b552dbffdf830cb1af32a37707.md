
### 3. 滚动到“MySQL 4.1”或任何标记为“Generally Available (GA) Release (recommended)”的发行，并点击“MySQL 4.1”链接。将出现“MySQL 4.1 Downloads”。

### 4. 滚动到“Windows downloads”并找到“Windows (x86)”包。点击“Pick a mirror”开始下载过程。会出现一个用户信息表。

### 5. 填写用户信息表，或者点击“No thanks, just take me to the downloads!”。

### 6. 选择离你最近的镜像站点。一个 ZIP 文件将开始下载。在提示时，将 ZIP 文件保存到桌面上。

我们已经下载了 ZIP 压缩包形式的安装程序。现在我们准备好解压并安装 MySQL 了。安装程序有许多界面，但对于大多数界面，我们将接受默认设置。出于空间原因，我们不会提到与我们目的无关的默认设置。

安装程序实际上两个程序：一个安装向导和一个配置向导。配置向导会提示一个值得注意的信息，即根密码（`root password`）。MySQL 根密码不需要与你的 Windows 管理员密码相同。在生产环境中，你绝不应使用管理员密码作为 MySQL 根密码。

MySQL 根密码仅供需要创建和删除数据库的程序和脚本使用。此类程序还可以创建权限较低的账户，这些账户可以访问某些数据库而无法创建新数据库。出于测试目的，我们将使用密码 `ppassword`，但在生产环境中你应该选择一个安全的密码。

在 `exchange2003.ad.corp.com` 上按照以下步骤解包、安装并配置 Windows 版 MySQL：

- 1. 在桌面上，双击我们在上一步中下载的 ZIP 文件。`Setup.exe` 程序将作为 ZIP 压缩包内的唯一文件出现。
- 2. 双击 `Setup.exe` 启动安装程序。
- 3. 出现“Welcome to the Setup Wizard for MySQL Server 4.1”界面。点击“Next”继续。
- 4. 出现“Setup Type”界面。选择“Complete”进行完整安装并点击“Next”继续。
- 5. 出现“Ready to Install the Program”界面，简要回顾将要的操作。点击“Install”开始实际安装。
- 6. 出现“MySQL.com Sign-Up”界面。注册账户，或直接选择“Skip Sign-Up”。然后点击“Next”。
- 7. 出现“Wizard Completed”界面，有一个标记为“Configure the MySQL Server Now”的复选框。确保勾选并点击“Finish”。
- 8. 出现“Welcome to the MySQL Server Instance Configuration Wizard”界面。点击“Next”。
- 9. 显示“MySQL Server Instance Configuration”界面。选择“Standard Configuration”并点击“Next”。
- 10. 出现“Please set the Windows options”界面。确保勾选了“Install As Service”，并点击“Next”。
- 11. 出现“Modify Security”界面。勾选“Modify Security”框。在密码字段中输入 `ppassword` 并点击“Next”。
- 12. 出现“Ready to Execute”界面。点击“Execute”完成配置。
- 13. 点击“Finish”关闭向导。

MySQL 已成功安装在 `exchange2003.ad.corp.com` 上。但我们需要解决一个小小问题。MySQL 提供了一个动态链接库（DLL），让其他应用程序（如 PHP）可以与之通信。此 DLL 未自动安装在 PHP 期望的位置。我们可以通过将此 DLL 复制到 `SYSTEM2` 来验证这一点。

为了让 PHP 使用此 DLL，请执行以下步骤：

- 1. 使用 Windows 文件管理器在 `C:\Files\MySQL Server 4.1\opt` 找到 `libmysql.dll`。
- 2. 拷贝到 `C:\WINDOWS\SYSTEM2`。

# MySQL 初始化

现在我们将验证 MySQL 是否运行正常，并完成运行 phpBB 的一个必要步骤。我们可以通过创建一个数据库来完成这些操作。我们可以使用简单的命令行客户端完成这些。

命令行工具对于典型的 MySQL 用户来说听起来更友好。MySQL 的管理命令只是结构化查询语言（SQL）的扩展，数据库丰富的开发人员通常熟悉它。但不用担心，我们不需要精通 SQL 就可以执行几个简单的命令来创建数据库、创建一个名为 `phpbb` 的新 MySQL 用户，并授予该用户对该数据库的权限。

为了这些，我们将使用 `database` 命令创建一个数据库，并使用 `grant all` 将数据库控制权授予特定用户。`grant all` 会在此过程中顺便创建该用户。

此外，我们将使用 `set password` 命令调整密码以与 PHP 兼容。PHP 标准的 MySQL 支持函数（在最新的 5.x 版本中，我们在本书中坚持使用 4.3 服务器，因为它在 Windows 上安装顺畅得多）不理解这种协议。PHP 5.x 的另一种 MySQL 扩展确实存在，但 PHP 应用程序不知道如何使用它……而且目前没有包含在 Windows 版 PHP 中。唉！幸运的是我们可以通过告诉 MySQL 使用“旧式”密码来解决这个问题。由于我们允许的所有数据库连接都来自本地（Web 和数据库服务器本身），这些密码不可能在网络上被监听。

要在 `exchange2003.ad.corp.com` 上为 `phpbb` 创建数据库和 MySQL 用户，请按照以下步骤操作：

- 1. 通过以下菜单选择启动命令行客户端：

`Start -> All Programs -> MySQL Server 4.1 -> MySQL Command Line Client`

2. 出现“Enter password:(输入密码:”提示。输入 MySQL 根密码，我们在测试实验室中将其设置为 `p@password`。随后出现 `mysql>` 提示符。

3. 在 `mysql>` 提示符下，输入以下 MySQL 命令以为 phpBB 的运行创建一个数据库：

```
create database phpBBB;
```

你将收到类似下所示的响应：

Query OK, 1 row affected (0.02 sec)

4. 输入以下 MySQL 命令将新数据库的控制权授予用户 `phpbb`：

```
grant all privileges on phpBBB.* to phpbb@localhost identified by 'p@ssword';
```

这将产生类似下所示的响应：

Query OK, 0 rows affected (0.02 sec)

> “0 rows affected”并不是错误。权限已正确设置。

5. 调整密码以兼容 PHP 使用的旧版 MySQL 客户端库：

```
set password for phpbb@localhost = OLD_PASSWORD('p@ssword');
```

这应该产生类似下所示的响应：

Query OK, 0 rows affected (0.02 sec)

> “0 rows affected”并不是错误。密码已正确调整。

6. 输入 `quit` 命令并按回车退出客户端。

# 在 Windows 上安装和测试 PHP

我们已经验证了 MySQL 引擎运行正常。并且我们创建了 phpBB 使用的数据库。现在我们准备好为 Windows 安装 PHP，为我们的 IIS 网站服务器引入 PHP 编程能力。在演示安装 phpBB 软件这一大收获之前，我们将安装 PHP 并使用 IIS 对其进行简单测试。

在大多数情况下，安装过程是非常直观的。同样，有很多提示，但大多数情况下我们都可以接受默认设置。这里有一个陷阱：PHP 安装程序使用用 VBScript 语言编写的脚本完成某些任务。在我们的 Windows 2003 / SP 1 服务器上，我们发现这些脚本生成了警告对话框，指示它们无法通过脚本（微软的脚本解释器之一）运行。幸运的是，Windows 为我们提供了另一种替代方案，即在微软的脚本解释器下运行脚本。由于提示信息有些晦涩，因此我们为你列出了正确的步骤。

另一个问题是：PHP 的当前“稳定”版本是 5.0 系列。我们发现在 Windows 平台上将此版本与 MySQL 集成非常困难。所以，和现在的许多 PHP 用户一样，在情况稍显稳定之前，我们将坚持使用 PHP 4.3 系列。

![](img/1bd448c8019d74f469e5d7e3f033d752_509_0.png)

# 为 Windows 安装的 PHP 4.3

按照以下步骤在 `exchange2003.ad.corp.com` 上安装 PHP 支持：

- 1. 访问 PHP 首页页 `www.php.net`。
