
![](img/1dc9ba96bb55315f8828b75f085ce4b4_191_0.png)

5. 填充自定义平台的简单方法是复制与您的自定义系统相似的默认平台，然后编辑内容。点击下拉菜单列表并选择现有目标平台来选择相似平台。点击确定。

6. 接下来您将看到“添加平台”对话框，字段已设为您复制的平台默认值（见图 14.2）。根据需要编辑字段。

图 14.2

“添加平台”对话框。

![](img/1dc9ba96bb55315f8828b75f085ce4b4_192_0.png)

- 名称（Name）——输入名称。
- 厂商（Vendor）——输入厂商。
- 产品名称（Product Name）——输入产品名称。
- 版本（Version）——输入版本。
- 包管理器（Package Manager）——输入包管理器。
- 架构（Architecture）——输入架构。
- 设备类型（Device Type）——选择设备类型。
- 操作系统检测（OS Detection）——选择操作系统检测。
- 启用此平台（Enable This Platform）——勾选此框以启用该平台。

7. 点击确定。

现在该平台已出现在您的自定义平台列表中。此操作是在系统中注册您的设备对象。

### 创建自定义平台

有时，您的公司可能根据 ZENworks Linux Management 支持的平台之一，创建创建了某些特殊的自定义发行版。ZENworks 可以识别这些自定义发行版，随后程序包中的 RPM 可以这些新的自定义发行版作为目标，从而允许您识别该 RPM 仅适用于此类设备类型。

要创建一个新的自定义平台，请完成以下操作：

1. 启动 ZENworks 控制中心。
2. 选择浏览器顶部的“配置”（Configuration）选项卡。
3. 从“管理区域设置”（Management Zone Settings）选择“平台”（Platforms）。
4. 滚动到屏幕底部，从“自定义平台”（Custom Platforms）快照选择“添加”（Add）。您将看到如图 14.1 所示的对话框。

图 14.1

用于创建自定义目标的“添加平台”对话框。

![](img/1dc9ba96bb55315f8828b75f085ce4b4_191_0.png)

5. 填充自定义平台的简单方法是复制与您的自定义系统相似的默认平台，然后编辑内容。点击下拉菜单列表并选择现有目标平台来选择相似平台。点击确定。

6. 接下来您将看到“添加平台”对话框，字段已设为您复制的平台默认值（见图 14.2）。根据需要编辑字段。

图 14.2

“添加平台”对话框。

![](img/1dc9ba96bb55315f8828b75f085ce4b4_192_0.png)

- 名称（Name）——输入名称。
- 厂商（Vendor）——输入厂商。
- 产品名称（Product Name）——输入产品名称。
- 版本（Version）——输入版本。
- 包管理器（Package Manager）——输入包管理器。
- 架构（Architecture）——输入架构。
- 设备类型（Device Type）——选择设备类型。
- 操作系统检测（OS Detection）——选择操作系统检测。
- 启用此平台（Enable This Platform）——勾选此框以启用该平台。

7. 点击确定。

现在该平台已出现在您的自定义平台列表中。此操作是在系统中注册您的设备对象。

### 配置静默安装

您可以以静默模式安装 Agent 并记录其响应。当您使用配置文件安装 Agent 时，安装是静默的。

通过运行 `zlm-install -a -r <配置文件路径>` 来记录响应。

要在静默模式运行安装，请运行 `zlm-install -s <配置文件路径>`。这将使用指定的配置安装 Agent。

### 更新 Agent

有时，您需要确保 Agent 更新到最新代码。这可以通过运行 `rug` 命令来实现。

### 加密 VNC 会话

ZENworks 自带的 VNC 版本目前不加密查看器和客户端之间的通信。如果您需要运行 GUI 仍想加密会话，请执行以下步骤：

1. 在管理员设备（查看器）上启动终端会。您需要在 ZCC 和托管设备之间建立隧道。执行此操作需要三项信息：
- 空闲端口（示例为 1234）
- 目标设备上运行的 VNC 服务器端口（为 5950）
- 目标设备的 IP 地址（已获取）

在终端中输入：

`ssh -L 1234:localhost:5950 <目标 IP 地址>`

此外，您可以包含 `-l <user>` 来指定用户账户。SSH 连接需要输入目标设备上有效账户的密码。当 shell 连接到远程设备时，会提示输入用户密码。提供密码后，安全连接即完成。

您可以在 http://www.uk.research.att.com/archive/vnc/sshvnc.html 获取更多关于与 SSH 使用 VNC 的额外信息。

4. 返回 ZENworks 控制中心并点击“设备”（Devices）选项卡。

5. 从左侧的任务列表中选择远程控制设备。您将看到以下对话框（见图 14.3）。

图 14.3

远程管理对话框。

![](img/1dc9ba96bb55315f8828b75f085ce4b4_195_0.png)

6. 在“IP 地址”字段中输入 `localhost`。

7. 在“端口”字段中输入 `1234`。

8. 点击确定。这将通过隧道到目标设备启动 VNC 查看器会话。输入远程控制会话的密码并点击确定。这将打开设备的 GUI。

### 不安装 VNC Agent

出于安全或空间考虑，有时您可能不希望 Agent 安装允许您远程控制设备的 VNC 组件。您可以通过向 `zlm-install` 命令传递 `-x` 来实现。

当 `zlm-install` 命令接收到 `-x` 时，不会安装任何 X-Windows 组件（即 VNC）。

# 日志

默认情况下，ZENworks Linux Management 会尝试记录大量信息和事件数据。你可以通过区域设置（zone settings）配置服务器和设备上的日志级别。请参阅第 6 章“系统设置”获取有关区域设置的更多信息。

在 ZENworks Linux Management 中，所有日志都存储在单一位置：`/var/opt/novell/log/zenworks`。进入此目录可以发现所有包含系统上运行进程信息的各种日志。设备上的日志可能位于相同的位置。

# 附录 A

## 命令

本附录讨论了用于 ZENworks Linux Management 的命令行工具。

共有三种不同的命令行工具：
- `zlman`——这是管理 ZENworks Linux Management 的主工具。
- `rug`——受管理设备上的代理（agent）用于执行安装、更新、删除软件等任务的工具。
- `zlmirror`——用于将包（bundles）和目录列表（catalogs）从远程 ZENworks Linux Management、YAST Online Updates 以及 RedHat Network 服务器镜像到你的本地 ZENworks 管理服务器或本地目录。

每个命令在页面的边缘都标有命令名称。如果有快捷方式，它将显示在命令旁边的括号中。语法行之后是简要描述以及任何额外选项列表。

### zlman

以下选项被所有命令理解：

```
-?, --help—获取特定命令的帮助。
-U, --user=<username>—指定用户名。
-P, --password=<password>—指定密码。
-log=<logfile>—指定要记录的文件（默认：/var/opt/nov11/log/zenworks/zlman.log）。
-d, --debug—显示调试输出。
```

--version--打印 `zlman` 版本并退出。

-V, --verbose--启用详细输出。

--quiet--静默输出，仅打印错误信息。

--ignore-rc-file--忽略 `~/.zlmanrc` 文件。

--host=<host>--指定要连接的主机名（默认：local-host）。

--port=<port>--指定服务器监听的端口（默认：443）。

--cleartext--为了调试目的禁用 SSL。端口必须设置为明文端口。

### ZLMAN 命令总结

| 命令 | 用法/选项 | 描述 |
| :--- | :--- | :--- |
| ping | `zlman ping <options>` | 验证服务器正在运行并有响应。 |
| registration-list (rl) | `zlman registration-list <options><filter>` | 列出所有注册。 |
| | -f, --filter=<filter> | 仅显示匹配指定过滤器的选项。（如果过滤器加了引号，可以使用通配符 * 和 ?。） |
| | -r, --recursive | 包含子文件夹中的对象。 |
