

![](img/e11fcbd2818a3495ac70085e5d8d1c26_601_0.png)

**图 20-1：许可协议**

- 2. 将出现一个类似图 20-2 的屏幕。该屏幕显示最新信息（README）。浏览这些信息，准备好后，点击**下一步**继续。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_601_1.png)

**图 20-2：请先阅读通知**

- 3. 下一个屏幕类似图 20-3，要求您输入网络域名、服务器名称和管理员电子邮件地址。默认情况下，安装程序会根据当前的 Windows 设置确定这些名称。如果合适，请更改默认值。除非主机实际上具有适当的 DNS 和网络配置，否则请勿更改服务器名称或域名。换句话说，不能任意选择域名或服务器主机名。此信息对于正在安装 Apache 的主机必须是有效的。点击**下一步**继续。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_602_0.png)

**图 20-3：输入您的服务器信息**

- 4. 选择是通过“完整”安装（安装所有程序功能，占用最多磁盘空间）还是“自定义”安装（仅安装选定的程序和文件）来安装 Apache，如图 20-4 所示。我建议您选择自定义安装选项，因为它可以让您更了解正在安装的内容。在自定义安装中，您可以始终选择所有项目以获得完整安装。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_602_1.png)

**图 20-4：选择安装方法**

- 5. 如果您选择进行自定义安装，您将看到类似图 20-5 所示的屏幕。显示了一个选项树。您可以点击每个项目来决定是否要安装它。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_603_0.png)

**图 20-5：为您的站点定制 Apache**

例如，点击 Apache httpd Server 项目会弹出如图 20-6 所示的选项菜单。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_603_1.png)

**图 20-6：安装选项菜单**

选择将功能（即 Apache 服务器）安装到本地硬盘或网络驱动器。如果磁盘空间是个问题，且您不想安装在线文档，可以通过点击该选项来取消选中此功能，从而选择不安装文档。

默认情况下，Apache 安装在 `C:\Program Files\Apache Group` 目录中。若要更改此设置，请点击 `Change` 按钮，在下一个对话框窗口中输入不同的目录，然后点击 OK 返回此屏幕。点击 Next 继续。

- 6. 安装程序显示一个屏幕，提示已准备好安装 Apache。点击 **Next**，并在安装 Apache 时等待。安装完成后，点击 **Finish** 结束安装程序。

默认情况下，安装程序会启动 Apache，因此您应该能够通过使用 Web 浏览器查看系统上的默认 Web 站点。将浏览器指向 http://localhost 或 http://127.0.0.1，您应该能看到类似图 20-7 所示的 Web 站点。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_604_0.png)

## 运行 Apache

您可以在 Windows 下通过控制台窗口中的命令行，或在 Windows 2000 或 Windows NT 系统下作为服务来运行 Apache。在 Windows 2000 或 NT 系统上，您应该将 Apache 作为自动服务运行。事实上，默认安装程序会检测您的 Windows 版本，并针对这两个平台选择将其作为服务安装。

> **注意** 在 Windows 9x 系统上，没有很好的方法将 Apache 作为服务运行。对于 9x 平台，最佳方法是在控制台窗口中运行 Apache。

### 将 Apache 自动作为 Windows 服务运行

安装程序会自动检测您的 Windows 平台，并在 Windows 2000 和 NT 系统上将 Apache 作为服务安装。在 Windows 2000（或 NT 系统）上，若要在服务器重启时自动（或不自动）运行 Apache，请执行以下操作：

- 1. 选择 开始 → 设置 → 控制面板 → 管理工具 → 服务，以显示类似图 20-8 所示的屏幕。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_605_0.png)

- 2. 双击服务名称“Apache”，将出现一个对话框，如图 20-9 所示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_605_1.png)

- 3. 在“常规”选项卡下，您将看到一个标记为“启动类型”的下拉菜单。选择 **Automatic**（重启时自动启动）、**Manual**（重启时手动启动）或 **Disabled**（重启时禁用）选项。

- 4. 如果您希望启动或停止 Apache 服务，请点击相应的按钮。

- 5. 默认情况下，Apache 使用本地系统账户在 **Windows 2000** 或 **Windows NT** 下运行。如果您希望将此用户 ID 更改为其他用户，请点击 **Log On** 选项卡并选择 **This account** 选项。然后输入相应的用户名和密码。请确保该用户名和密码是您 Windows 网络上有效的用户凭证。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_606_0.png)

默认情况下，Apache 以 LocalSystem（“System”）账户运行，这是一个非常强大的本地账户，不与任何用户名或密码关联。此账户不能用于登录机器或连接到同一 Windows 网络上的其他机器。如果您选择更改 Apache 服务的用户，请确保创建一个适当的用户账户，该账户可以作为服务（即作为操作系统的一部分）运行，能够登录到服务，能够备份和还原文件和目录，对文档根目录具有读取访问权限，并且对 Apache 日志目录具有读取、写入和删除访问权限。默认的用户名对于大多数系统应该是足够的。

- 6. 在 Windows 2000 Advanced Server 下，若要定义 Apache 服务失败时的操作，请选择“恢复”选项卡并为第一次、第二次及后续故障选择适当的操作。例如，您可以选择在 Apache 服务失败时自动重启服务或重启机器，甚至运行外部程序以执行一些有用的操作，例如呼叫系统管理员。图 20-10 显示，当 Apache 服务第一次运行失败时，它将自动重启；在第二次故障时，服务器将自动重启；对于任何后续故障，一个程序将呼叫系统管理员。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_606_1.png)

**图 20-10：Windows 2000 Advanced Server 上 Apache 服务的恢复选项**

- 7. 服务配置完成后，点击“应用”以完成设置。

- 您也可以随时通过控制台使用 **net start apache** 或 **net stop apache** 命令来启动或停止 Apache 服务。

与许多 Windows 服务不同，Apache 将其错误记录在自带的错误日志文件中。默认情况下是 `logs\error.log`，它位于默认的 `C:\Program Files\Apache Groups\Apache` 目录中。只有 Apache 服务初始启动期间发生的错误才会记录在 Windows 2000 和 NT 下可用的事件日志功能中。

### 通过开始菜单管理 Apache

默认情况下，Apache 安装程序会在 Windows 开始菜单中添加菜单项，您可以使用这些菜单项来启动、重启和停止 Apache，方法如下：

- 若要启动 Apache，选择 开始 程序-Apache httpd Server Control Apache Server Start。
- 若要重启 Apache，选择 开始 程序-Apache httpd Server Control Apache Server Restart。
- 若要停止 Apache，选择 开始 程序-Apache httpd Server Control Apache Server stop。
- 您还可以编辑和测试 `httpd.conf` 配置文件，方法如下：

    - 若要编辑 `httpd.conf` 文件，选择 开始 程序-Apache httpd Server Configure Apache Server Edit Configuration。
    - 若要测试 `httpd.conf` 文件，选择 开始 程序-Apache httpd Server Configure Apache Server Test Configuration。这等同于从 Apache 二进制目录运行 `Apache -t` 命令。将会弹出一个控制台窗口，您将能够查看配置语法。

### 通过命令行管理 Apache

如果您不将 Apache 作为服务运行，您可以使用以下命令从控制台（通常称为 DOS 窗口）启动、停止或重启 Apache。

- 若要启动 Apache，请从 Apache 二进制目录（默认为 `C:\Program Files\Apache Group\Apache`）运行 `Apache -k start`。
- 若要优雅重启 Apache，请从 Apache 二进制目录（默认为 `C:\Program Files\Apache Group\Apache`）运行 `Apache -k restart`。
- 若要停止 Apache，请从 Apache 二进制目录（默认为 `C:\Program Files\Apache Group\Apache`）运行 `Apache -k stop`。您也可以使用 `Apache -shutdown` 命令来达到相同的效果。
- 若要使用非默认配置文件运行 Apache，请使用 `-f` 选项指定文件名。例如，若要使用 `c:\test\new-httpd.conf` 运行 Apache，请从包含 Apache 二进制的目录运行 `Apache -f "c:\test\new-httpd.conf" -k start` 命令。

