
- 树状窗口 - 在这里你可以看到由 ServeRAID 控制器管理的所有系统
- 信息窗口 - 在此地你可以看到有关阵列和逻辑驱动器的信息
- 事件日志 - 所有事件都显示在此处。

> 注意
> 有关如何使用 ServeRAID Manager 的说明可以在在线帮助中找到。

# 第 2 章. 安装 SuSE Linux 97

## 2.5.8 ServeRAID 适配器的远程管理

安装了 ServeRAID 控制器的服务器也可以进行远程管理。为此，你需要执行以下操作：

- 1. 在安装了 ServeRAID 适配器的服务器上安装 ServeRAID Manager，具体方法见第 94 页第 2.5.7 节“使用 ServeRAID Manager 工具”。不要忘记启用启动时作为服务运行的 ServeRAID Manager Agent。
- 2. 在与要管理的服务器建立 TCP/IP 连接的 Linux 工作站上安装 ServeRAID Manager。

在开始使用 Linux ServeRAID Manager 的远程管理功能之前，你需要更改要管理的服务器上的安全设置。如果服务器配置了适当的 X Windows 环境，你可以在本地启动 ServeRAID Manager 并更新安全信息。如果你在服务器上没有使用 X Windows，则需要按照以下步骤以便访问服务器。默认情况下，在安装 ServeRAID Manager 后安全性开启。

- 1. 在安装了 ServeRAID Manager 的 Linux 工作站上，使用命令启动管理器：

```
/usr/RaidMan/RaidMan.sh
```

### ServeRAID Manager

![](img/85b06e2bfb0156a5e744cfac214d4788_112_0.png)

图 99. 启动安全配置

- 2. 从 Actions 菜单（图 99）选择 ServeRAID agent->Security。你会看到一个类似于图 100 的窗口。

第 2 章. 安装 SuSE Linux 99

![](img/85b06e2bfb0156a5e744cfac214d4788_113_0.png)

- 3. 双击 `Admin`（这是一个内置用户，无法删除），你会看到一个类似于图 101 的窗口。

![](img/85b06e2bfb0156a5e744cfac214d4788_113_1.png)

图 101. 更改用户

- 4. 输入所需的密码并点击 `OK`。
- 5. 关闭 ServeRAID Manager。

100 xServers 和 Netinity SuSE Linux 集成指南

- 6. 在被管理的服务器上安装 ServeRAID Manager。将文件 `/usr/RaidMan/RaidSLst.ser` 从工作站复制到服务器。

> 注意
> 服务器上的目录必须与工作站上的相同。

- 7. 执行命令：

```
ps ax | grep jre*
```

找到所有 jre 进程并删除它们。你还需要删除 ServeRAID Manager agent。你可以通过命令找到进程 ID：

```
ps ax | grep RaidAgnt*
```

- 8. 在命令行提示符中使用此命令，可以重启 ServeRAID agent：

```
/usr/RaidMan/RaidMan.sh &
```

恭喜！你的服务器现在准备好进行远程 ServeRAID 管理了。

你可以通过在工作站上选择 Remote -> Add remote system（如图 102 所示）连接到远程服务器。

xServers 和 Netinity SuSE Linux 集成指南

![](img/85b06e2bfb0156a5e744cfac214d4788_115_0.png)

图 102. 访问远程系统

你会看到一个类似于图 103 的窗口。

![](img/85b06e2bfb0156a5e744cfac214d4788_115_1.png)

图 103. 远程系统

输入必要的数据并点击 Connect。系统连接后，你会看到一个类似于图 104 的窗口。

![](img/85b06e2bfb0156a5e744cfac214d4788_116_0.png)

现在你可以管理远程 ServeRAID 适配器。

## 2.6 XFree86 配置

初始安装后，系统仅在文本终端启动。如果你想将 Linux 作为操作系统，这也可以，但许多人更倾向于基于 Windows 的界面。如果你想使用像 KDE 或 GNU Network Model (GNOME) 这样的图形桌面环境，首先需要配置 X。

配置 XFree86，我们推荐使用 SuSE 的高级工具 SaX。有关 SaX 的详细文档，请参见 SuSE Linux 手册中的第 8.4 节“使用 SaX”。由于某些原因 SaX 失败，你仍然可以使用 XF86setup 或 x86config 作为备选。两者都属于 XFree86，也可用于配置。然而，它们没有 SaX 那么友好，你可能需要一些使用 XFree86 的经验。

第 2. 安装 SuSE Linux 103

有关配置 XFree84 的信息，请参见 SuSE Linux 手册中的第 8.3 节“使用 SaX”。

以 root 身份登录后，在命令行输入 `sax` 启动 SaX。如果你已经知道哪个服务器驱动适用于你的显卡，也可以使用 `sax -s <servername>` 例如 `sax -s svga`。

SaX 完成配置后，你将看到图 105 中的鼠标配置对话框。

![](img/85b06e2bfb0156a5e744cfac214d4788_117_0.png)

由于 SaX 是图形化配置工具，你首先需要配置鼠标以便方便操作 SaX。如果你在初始安装期间配置了鼠标，你应该已经能够移动鼠标了。如果没有，你需要通过按 Tab 键在不同的输入字段之间移动。

如果鼠标移动正常，点击名为 Test 的文件夹来测试鼠标。

104 xServers 和 Netinity SuSE Linux 集成指南

![](img/85b06e2bfb0156a5e744cfac214d4788_118_0.png)

图 106. SaX: 鼠标测试

如果你的鼠标只有两个，可以通过同时按下左键和右键来模拟第三个（中间）鼠标键。要激活此仿真模式，选择 Options 文件夹并勾选 Emulate 3 buttons。

![](img/85b06e2bfb0156a5e744cfac214d4788_119_0.png)

点击 `Apply` 应用更改。如果鼠标正常，点击 `OK` 关闭鼠标对话框。点击右下角的 `Next >>` 继续进入窗口。

106 xServers 和 Netinity SuSE Linux 集成指南

### 键盘

型号

Generic 104-key PC

Japanese 106-key

Keytronic FlexPro

Microsoft Natural

![](img/85b06e2bfb0156a5e744cfac214d4788_120_0.png)

语言

U.S. English

United Kingdom

![](img/85b06e2bfb0156a5e744cfac214d4788_120_1.png)

应用

测试字段

重映射死键

按 F10 进入菜单 Next >>

图 108. SaX: 键盘配置

默认情况下，SaX 采用初始安装期间的键盘配置。如有必要，选择键盘型号和语言。你可以使用测试字段输入一些文本进行测试。如果键盘工作正常，点击 Next >> 继续进入显卡窗口。

![](img/85b06e2bfb0156a5e744cfac214d4788_121_0.png)

图 109. SaX: X 服务器选择

如果 SaX 能够检测到你的显卡，将在 Name 字段中看到 Autodetect（自动检测）。然后你可以直接进入显示器配置窗口。如果未检测到显卡，你可以从 Vendor 列表中选择，或者选择 Generic Server Selection 并选择适用于显卡的 X 服务器。某些显卡需要额外的配置。点击 Expert 打开高级配置对话框。点击 Next >> 选择显示器。

108 xServers 和 Netinity SuSE Linux 集成指南

### 文件设置信息

| 厂商 | 名称 |
| :--- | :--- |
| III LCD | 1024X768@75HZ |
| II VESA | 1280X1024@75HZ |
| I-CT KERN | 1600X1200@75HZ |
| AMAZING | 800X600@75HZ |
| ACER |  |
| ADONICS |  |
| ADEX |  |
| ADI |  |
| ALPHA |  |

Expert Hsync: 31-37.5 kHz Vsync: 50-80 Hz Typ: crt,color

按 F10 进入菜单 Next >>

图 110. SaX: 显示器配置窗口
