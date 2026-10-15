
## 安装软件包 RPM 和 YUM

Linux 提供了多种工具，允许用户安装、管理和更新软件包。Fedora 有两个主要的工具，即 `rpm` 和 `yum`；在 `rpm` 中，用户可能需要搜索感兴趣的包，下载它并安装它，并且知道如果该包需要其他额外的包，必须单独进行搜索、下载和安装。`yum` 命令提供了相同的功能，但它会自动执行大部分工作，包括在互联网上搜索该包，然后下载并安装它，同时自动安装所有所需的其他包。

测试了 `rpm` 和 `yum`；对安装 `xlockmore` 软件包进行了尝试。在 `rpmfind.net` 网站上找到了该包，如图 2.16 所示。然后获取了链接并使用 `wget` 命令将其下载到 `Downloads` 目录，如图 2.17 所示。

### RPM 为 xlock 找到 10 个结果

| 软件包 | 摘要 | 发行版 |
| --- | --- | --- |
| `xlock-5.3-9.1.1506.i686` | X Window 的屏幕保护程序和锁定 | OpenSUSE 12.3 for x86 |
| `xlock-5.3-9.1.1506.i686` | X Window 的屏幕保护程序和锁定 | OpenSUSE 12.3 for x86 |
| `xlock-5.3-9.1.1506.i664` | X Window 的屏幕保护程序和锁定 | OpenSUSE 12.3 for x86_64 |
| `xlock-5.3-9.1.1506.i664` | X Window 的屏幕保护程序和锁定 | OpenSUSE 12.2 for x86_64 |
| `xlock-5.3-7.2.1586.i686` | X Window 的屏幕保护程序和锁定 | OpenSUSE 12.1 for x86 |
| `xlock-5.3-7.2.1586.i664` | X Window 的屏幕保护程序和锁定 | OpenSUSE 12.1 for x86_64 |
| `xlock-5.3-4.2.1506.i686` | X Window 的屏幕保护程序和锁定 | OpenSUSE 11.4 for x86 |
| `xlock-5.3-4.2.1506.i664` | X Window 的屏幕保护程序和锁定 | OpenSUSE 11.4 for x86_64 |
| `xlock-5.32-4.1.1506.i686` | X Window 的屏幕保护程序和锁定 | OpenSUSE 11.4 for x86 |
| `xlock-5.32-4.1.1506.i664` | X Window 的屏幕保护程序和锁定 | OpenSUSE 11.4 for x86_64 |

图 2.16：在 `rpmfind.net` 中启动了 `xlock` 的搜索并下载了 `rpm` 文件。

![](img/7be05572b414927ff78ba38f31a7ecfc_67_0.png)

下载过程完成后，使用 `rpm -iv` 命令启动软件包的安装，但显示了错误，表明在安装 `xlock` 包之前必须先下载并安装其他包，如图 2.18 所示。

![](img/7be05572b414927ff78ba38f31a7ecfc_68_0.png)

根据图 2.18，软件包未被安装，因为需要在系统上预先安装其他包。可以使用 `rpm -q` 命令验证软件包是否已安装，如图 2.19 所示。

![](img/7be05572b414927ff78ba38f31a7ecfc_68_1.png)

图 2.19：如 `rpm -q` 命令所示，`xlockmore` 软件包未安装。

`yum` 命令为安装软件包提供了一种方便的方法，因为在 `yum install` 命令后除了输入包名外，不需要其他操作，如图 2.20 所示。在最近的 Linux 中使用 `yum` 命令会显示警告，指出它将在较新版本中不再被使用，因为它将由 `dnf` 命令取代。如图 2.21 所示，使用 `dnf` 命令仅需一条命令即可安装 `xlockmore`。

# 控制台与登录安全

## 锁定控制台

未锁定的运行机器提供了一个易于破解的系统，因为它允许攻击者从系统中获取多个文件。消除这种风险的良好做法是在离开运行机器时锁定屏幕。此操作可以使用 Linux 中的 `xlock` 工具完成，因为它会锁定屏幕并要求输入 `root` 密码来解锁。

![](img/7be05572b414927ff78ba38f31a7ecfc_69_0.png)

![](img/7be05572b414927ff78ba38f31a7ecfc_69_1.png)

在终端中输入 `xlock` 命令，如图 2.22 所示显示屏幕保护程序，当按下任意键时，会显示另一个屏幕请求 `root` 密码，如图 2.23 所示。

![](img/7be05572b414927ff78ba38f31a7ecfc_70_0.png)

图 2.22：屏幕保护程序显示请求 `root` 密码。

![](img/7be05572b414927ff78ba38f31a7ecfc_70_1.png)

图 2.23：显示请求 `root` 密码。

## 禁用控制台

如果运行机器未锁定，它提供了一个易于破解的系统，因为它允许攻击者从系统中获取多个文件。消除这种风险的良好做法是在离开运行机器时锁定屏幕。此操作可以使用 Linux 中的 `xlock` 工具完成，因为它会锁定屏幕并要求输入 `root` 密码来解锁。在终端中输入 `xlock` 命令，如图 2.22 所示显示屏幕保护程序，当按下任意键时，会显示另一个屏幕请求 `root` 密码，如图 2.23 所示。

## 控制台安全

未锁定的运行机器提供了一个易于破解的系统，因为它允许攻击者从系统中获取多个文件。消除这种风险的良好做法是在离开运行机器时锁定屏幕。此操作可以使用 Linux 中的 `xlock` 工具完成，因为它会锁定屏幕并要求输入 `root` 密码来解锁。在终端中输入 `xlock` 命令，如图 2.22 所示显示屏幕保护程序，当按下任意键时，会显示另一个屏幕请求 `root` 密码，如图 2.23 所示。

## 登录界面

大多数时候，登录界面为攻击者提供了有关系统的有用信息。当攻击者知道系统的类型和版本时，他们能够发起攻击。良好的做法是从登录界面隐藏所有系统信息，同时显示警告信息，警告攻击者他们即将访问未经允许的系统。

# 横幅配置

`group1@M80006988~`

文件 编辑 视图 搜索 终端 帮助
`GNU nano 2.5.3` 文件:`/etc/issue.net` 已修改

```
\S
内核位于 \m (\l)

这是一个横幅警告，旨在警告你尝试未经授权访问该系统，Group1 成员有权起诉你并将你的行为提交法庭审判。
```

^ 获取帮助 ^ 写出 所在位置 ^ 剪切文本 对齐 ^ 当前位置
^ 退出 读取文件 替换 未剪切文本 拼写 ^ 跳转行

图 2.29：`/etc/issue.net` 文件已修改了新的横幅消息，以便在启动未经授权访问时显示。

`banner` 参数和 `/etc/issue.net` 文件的位置必须在 `/etc/ssh/sshd_config` 文件中指定，如图 2.30 所示。

| 活动 终端 | 设置 2101 |
| :--- | :--- |
| `group1@M80006988~` | 文件 编辑 视图 搜索 终端 帮助 |
| 文件: `/etc/ssh/sshd_config` 已修改 | 配置模式 2 |
| `# 打印最后一行` | |
| `PasswordAuthentication yes` | |
| `PubkeyAuthentication yes` | |
| `UsePAMSeparation sandbox` | |
| `PermitRootEnvironment no` | |
| `ClientAliveCountMax` | |
| `ClientAliveInterval no` | |
| `ShowPasslevel no` | |
| `# 文件 /etc/ssh/sshd_config` | |
| `Match Group sftp` | |
| `PermitTunnel no` | |
| `VersionAddendum none` | |
| `# 允许使用 /etc/issue.net 转发` | |
| `# 接受本地区域环境变量` | |
| `acceptenv LC_TYPE NAME LC_COLLATE LC MESSAGES` | |
| `acceptenv LC_PAPER NAME LC TELEPHONE MEASUREMENT` | |
| `acceptenv LC_SIZE LC ALL LANGUAGE` | |
| `acceptenv XMODIFIERS` | |
| `# 覆盖默认子系统` | |
| `# 按用户覆盖设置的示例` | |
| `Match group users Shell=/usr/bin/sftp-server` | |
| `AllowForwarding no` | |

^ 获取帮助 ^ 写出 所在位置 ^ 剪切文本 对齐 ^ 当前位置 上一页
^ 退出 读取文件 替换 未剪切文本 拼写 ^ 跳转行 下一页

图 2.30：通过向 `/etc/ssh/sshd_config` 文件添加 `banner /etc/issue.net` 行，启用了横幅消息。

通过 `/etc/ssh/sshd_config` 启用横幅后，对 `ssh` 系统进行了测试，输入的消息显示如图 2.31 所示。

![](img/7be05572b414927ff78ba38f31a7ecfc_75_0.png)

图 2.31：当启动 `ssh` 会话时，显示预定义的横幅。

# Wireshark

使用非加密服务（如 `telnet` 和 `http`）会导致凭据和通信信息面临被攻击者嗅探的风险，因为它们都是以明文形式发送和接收的。嗅探网络包最常用的工具之一是 `Wireshark` 软件。

在该 `Wireshark` 软件包中已安装并启动了软件，如图 2.32、33、34 所示。图 2.36 显示已开始捕获，并访问了一个测试 `http` 网站，并在表单中输入了用户名和密码，如图 2.37 所示。`Wireshark` 成功嗅探到了输入的用户名和密码，如图 2.38 所示。

![](img/7be05572b414927ff78ba38f31a7ecfc_75_1.png)

图 2.32：使用 `dnf install` 命令成功安装了 `Wireshark` 软件包。

# Wireshark

六 23:56
