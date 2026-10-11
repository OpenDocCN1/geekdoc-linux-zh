
你应该得到 IP 地址。如果没有得到，说明 PC 上的客户端软件没有正确安装或启动。

# 测试 6

运行命令 `mblookup -d '*'`

这次我们正在尝试与上一次测试相同的操作，但通过广播进行。

# 测试 7

运行命令 `smclient '\BIGSERVER\TMP'`。你应该会被提示输入密码。你应该使用登录 Unix 机器的账户密码。如果你想用另一个账户进行测试，请在命令末尾添加 `-U <username>` 选项。例如：`smclient //bigserver/tmp -Ujohnndoe`。

# 测试 8

在 PC 上输入命令 `net view \\BIGSERVER`。你需要在 dos 提示符窗口中执行此操作。你应该会获得服务器上可用共享的列表。

如果你收到“network name not found”（找不到网络名称）或类似的错误，说明 netbios 解析未正常。这通常是由 `nmbd` 的问题引起的。要解决这个问题，你可以采取以下操作之一（只需选择其一）：

- 修复 `nmbd` 安装
- 在 PC 的高级 tcp/ip 设置中的 wins server 框中添加 `BIGSERVER` 的 IP 地址。
- 在 tcp/ip 设置的高级部分通过 DNS 启用 wmans 解析。
- 在 PC 的 `lmhosts` 文件中添加 `BIGSERVER`。

如果你收到“invalid network name or password”（无效的网络名称或密码）错误，则采用与上述上述 `smclient -L` 测试中相同的修复方法。特别是，请确保你的 `hosts.allow` 行是正确的（参见 man 手页）。

此外，不要忽视这样一个事实：当工作站请求 samba 服务器时，它将尝试使用你登录 Windows 机器时使用的名称进行连接。你需要确保 Samba 服务器上存在一个具有相同名称和密码的账户。

如果你收到“specified computer is not receiving requests”（指定的计算机未接收请求），则可能意味着主机无法通过 tcp 服务访问。检查主机是否运行了 tcp wrappers，如果是，请在 `hosts.allow` 文件中为你的客户端（或子网）添加条目。

# 测试 9

运行命令 `net use x: \\BIGSERVER\TMP`。系统会提示输入密码，然后你应该收到“command completed successfully”（命令成功完成）的消息。如果没有，说明你的 PC 软件安装错误或 `smb.conf` 错误，请确保 `smb.conf` 中的 `hosts allow` 以及其他配置行是正确的。

也可能是服务器无法确定用于连接的用户名。要检查是否是该问题引起的，请在 `smb.conf` 的 `[tmp]` 部分添加行 `user = USERNAME`，其中 `USERNAME` 是用户名。

# 第 G 节：诊断你的 Samba 服务器

对应你输入的密码。如果你发现这解决了问题，你可能需要用户映射（user mapping）选项。

# 测试 10

从文件管理器尝试浏览服务器。你的 samba 服务器应该出现在你的本地工作组（或你在 `smb.conf` 中指定的的工作组）的浏览列表中。你应该能够双击服务器名称并获得共享列表。如果你执行此操作时收到“invalid password”（无效密码）错误，你可能正在运行 WinNT，它拒绝浏览一个没有加密密码功能且处于用户级安全模式的服务器。在这种情况下，在你的 `smb.conf` 文件中设置 `security = server` 且 `password server = Windows_NT_Machine`，并在编译对加密密码的支持之后启用加密密码（参考 Makefile）。

# 仍然遇到问题？

尝试联系邮件列表或新闻组，或者使用 `tcpdump-smb` 工具来嗅探问题。官方 samba 邮件列表的联系地址为 <samba@samba.org>。要了解更多关于 samba 的信息以及如何订阅邮件列表，请查看 samba 网页：

```
http://samba.org/samba
```

同时查看 Samba 软件包中的其他文档！

# 索引

# 681

# A

高级电源管理 (APM) 支持, 66

AfterStep 桌面, 187

`alias` 命令, 99–100

APM (高级电源管理) 支持, 66

笔记本电脑的 apm 工具程序, 305

Applets, 到 Gnome 桌面面板, 161–162

应用程序启动器 (Application Launcher), 189–190

添加程序到, 190

Internet 项, 添加到, 192

StarOffice, 插入到, 218

通用非设备特定参数, 367–379

内存处理参数, 371–372

杂项参数, 374–379

NFS 根文件系统参数, 372–374

RAM 磁盘管理选项, 369–371

根文件系统选项, 368–399

硬盘, 389–392

IDE 磁盘/CD-ROM 驱动参数, 389–391

标准 ST-506 磁盘驱动选项, 391–392

XT 磁盘驱动选项, 391

MS 总线鼠标驱动程序, 400

概览, 367, 401

内核如何对参数进行排序, 366–367

# B

`bashrc` 文件，用 vi 编辑器, 107–110

Baud 与 bps, 484–485

启动管理程序 (Boot managers), 6–7

BootMagic 程序, 6–7, 47

CalderaLinux, 53–55

TurboLinux 工作站, 66–67

启动提示符 (Boot prompt), 361–401

SCSI 主机适配器的参数, 383–389

SCSI 外围设备的参数, 382–383

视频帧缓冲驱动程序的参数, 380–381

控制 PCI bios 行为的参数, 379–380

总线鼠标驱动程序, 399

CD-ROM (非 SCSI/ATAPI/IDE), 392–395

复制, 400

以太网设备, 397–398

软磁盘驱动程序, 389–399

LILO (Linux 加载器) 程序, 365–366

LoadLin 程序, 365–366

传递给 init 的参数, 367

设置环境变量, 367

打印机驱动程序, 400

串行驱动程序, 395–397

声音驱动程序, 399

ps 与 baud, 484–485

总线鼠标驱动程序, 399–400

# C

CalderaLinux 配置, Windows, 156

CalderaLinux 配置, Windows, 49–53

CalderaLinux 配置, Windows, 55

CalderaLinux 配置, Windows, 52–54

CalderaLinux 配置, Windows, 37–48

CalderaLinux 配置, Windows, 50

CalderaLinux 配置, Windows, 51

CalderaLinux 配置, Windows, 44

CalderaLinux 配置, Windows, 42, 46

CalderaLinux 配置, Windows, 43

CalderaLinux 配置, Windows, 45

CalderaLinux 配置, Windows, 43

CalderaLinux 配置, Windows, 47

CalderaLinux 配置, Windows, 48

CalderaLinux 配置, Windows, 38

CalderaLinux 配置, Windows, 39

CalderaLinux 配置, Windows, 40

CalderaLinux 配置, Windows, 41

CalderaLinux 配置, Windows, 32

CalderaLinux 配置, Windows, 33

CalderaLinux 配置, Windows, 34

CalderaLinux 配置, Windows, 35

CalderaLinux 配置, Windows, 36

CalderaLinux 配置, Windows, 31

CalderaLinux 配置, Windows, 34

CalderaLinux 配置, Windows, 35

CalderaLinux 配置, Windows, 36

CalderaLinux 配置, Windows, 37

CalderaLinux 配置, Windows, 38

CalderaLinux 配置, Windows, 39

CalderaLinux 配置, Windows, 40

CalderaLinux 配置, Windows, 41

CalderaLinux 配置, Windows, 42

CalderaLinux 配置, Windows, 43

CalderaLinux 配置, Windows, 44

CalderaLinux 配置, Windows, 45
