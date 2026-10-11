
```
Chain FORWARD (DROP)
target prot opt scope destination
ACCEPT all all anywhere state RELATED, ESTABLISHED
RULE_0 tcp all anywhere 192.168.1.12 tcp multiport dports,https state NEW
RULE_1 tcp all anywhere 192.168.1.0/24 tcp multiport dports,https state NEW

Chain RULE_0 (2 references)
target prot opt scope destination
LOG all all anywhere
ACCEPT all all anywhere LOG level info prefix 'RULE 0 - ACCEPT '

Chain RULE_1 (3 references)
target prot opt scope destination
LOG all all anywhere
ACCEPT all all anywhere LOG level info prefix 'RULE 1 - ACCEPT '
```

注意，默认链与你在 `FWBuilder` 中配置的规则匹配，目标为 `RULE_<RULE NUMBER>`。这些额外的链用于配置日志。所有链的开头还有一条规则用于接受与已建立会话相关的流量。这通常是理想的，但仍然配置。要删除此自动生成的规则，请在树视图中选择防火墙并在对话框区域点击“防火墙设置”。DMZ、远程访问和 VPN • 第9章“在第一条规则之前接受 ESTABLISHED 和 RELATED 数据包”。虽然你配置的 `FWBuilder` 策略涵盖了你可能需要的任何基础规则，但还有几种情况需要处理。如果你在 Linux 防火墙上进行 NAT，使用 `FWBuilder` 配置它是很容易的。按照以下步骤操作，使你的防火墙将来自内部网络的所有流量 NAT 到外部接口使用的 DHCP 地址。这种配置也称为源 NAT（`source nat`），因为更改的是源地址。

- 1. 在对话框区域选择 `NAT` 选项卡。
- 2. 右键点击并选择“插入规则”。这将添加编号为 0 的 NAT 规则。
- 3. 从对象树将你的 `INTERNAL` 网络对象拖到 NAT 策略中的原始源（`Original Src`）列。
- 4. 将防火墙树上的外部接口拖到 NAT 策略中的“翻译后的源”（`Translated Source`）。

就是这样。保存、编译并安装。

擦除文件系统并在磁盘上安装一个经过加的 Linux 版本，并带有 SmoothWall 软件。SmoothWall 防火墙在系统中没有 GUI，只有命令行界面以及通过 Web 管理界面进行管理。SmoothWall 的设计目的仅作为一个防火墙，不再作他用。

考虑到这一点，这种方法有几个优点。首先，你不需要学习如何加固你的 Linux 发行版使其达到足够的安全水平。此外，与安装 Linux 并学习 `iptables` 语法不同，使用 SmoothWall 你不需要了解 Linux。安装菜单会引导你完成防火墙功能的配置。你不需要了解任何关于 Linux 的知识就能让 SmoothWall 运行起来（尽管了解一下总没有坏处）。SmoothWall 防火墙已经经过了精简，并移除了不需要的软件和服务，这意味着你可以最大限度地利用旧电脑的性能，而无需花费大量时间来调优几个（普通的）Linux 发行版。

# 安装 Smoothwall

安装 SmoothWall Express 最简单的方法是从 `http://smoothwall.org/` 下载 `.iso` 镜像。建议阅读位于 `http://smoothwall.org/docs/` 上的手册。SmoothWall Express 提供的文档在免费产品中是出色的，而且所有的安装界面都显示在 PDF 安装指南中。这种安装方法与手动安装 SmoothWall Express 一样。

- 1. 将此文件刻录到 CD-ROM 后，在驱动器中插入 CD-ROM 并启动目标防火墙。
- 2. 启动界面看起来与许多 Linux 发行版典型。它会警告你安装 SmoothWall Express 将删除硬盘上的所有数据。如要继续安装，请按 `ENTER`。
- 3. 安装将切换到类似 DOS 的 GUI 界面。使用 `TAB`、方向键和 `ENTER` 键进行导航。系统会提示插入安装 CD 并点击 `OK`。如果你的系统无法从 CD-ROM 启动且你使用了启动软盘开始安装，则执行此操作。无论如何，请确保 CD-ROM（仍）在驱动器中，高亮 `OK` 并按 `ENTER`。
- 4. 在硬盘重新分区并丢失所有数据之前，你必须选择两次 `OK`。
- 5. 在提示时，选择 `Probe`（探测）以允许安装程序查看它能检测到哪些网卡。

SmoothWall 使用接口颜色概念来表示它们的信任级别，在安装过程中你将开始看到这些术语。例如，

![](img/33fc180c04c8f96c022bce6e62ae12fd_333_0.png)

你的内部接口被认为是信任流量，并指定为 `GREEN`（绿色）接口。虚拟拨号或间接数字数字网络（ISDN）被指定为 `ORANGE`（橙色）接口。你也可以拥有颜色组合来指示你的接口配置。如果你使用额外的以太网接口作为不信任（外部）接口，在 Smoothwall 的术语中那就是 `GREEN + RED`（红色）。

文件安装成功后，你将有机会从软磁盘恢复配置。这在你升级或迁移到新硬件时非常有用。在这种情况下，我们选择 `OK`。

- 1. 选择你的键盘布局（在我的案例中是“`US`”），并选择 `OK`。
- 2. 为防火墙选择主机名（例如 `smoothwall`）并选择 `OK`。
- 3. 下一个屏幕允许你输入代理服务器信息，以防防火墙需要通过代理获取 Web 更新。如果你正在使用代理，请在此处输入相应信息；如果没有，请选择 `OK`。
- 4. 接下来的几个屏幕允许你为 ISDN 或 ADSL 连接输入配置信息。安装过程的假设是你的 INSIDE（信任）接口是以太网接口，而 OUTSIDE（不信任）接口将是以太网、ISDN 或 ADSL。如果你使用其中之一，请输入相应信息。如果你的 OUTSIDE 接口是普通的以太网接口（例如来自电缆调制解调器），请在 ISDN 和不对称数字用户线（ADSL）配置屏幕上选择 `DISABLE`。
- 5. 下一个屏幕允许你查看并编辑网络配置。如果两个都使用以太网接口，你需要在网络配置类型中选择 `GREEN + RED`。检查每个菜单选项，确保两个接口都被识别、安装了驱动程序并设置了 IP 地址。通常，`RED` 接口使用 `DHCP`，而 `GREEN` 使用静态 IP 地址，这样内部主机可以将防火墙配置为访问 Internet 的默认网关。

当你对所有设置满意时，选择 `DONE`。

系统会询问你是否启用 SmoothWall 防火墙作为 `DHCP` 服务器。这与大多数家用防火墙的配置相同，作为防火墙、网关和 `DHCP` 服务器。如果你的网络中还没有 `DHCP` 服务器，请启用它。在各个字段中输入所需的值。大多数设置不是关键的，但一个需要注意的设置是租期时间。租期过长会导致你缓慢失去那些在离线前未收到释放地址更改系统（例如崩溃或断电）IP 地址。如果租期太长，这种 IP 地址耗尽可能会耗尽 `DHCP` 范围，为其他用户留出可用地址。24 小时的租期并不常见，且通常网络越大，需要的租期就越短。如果你不确定 `DHCP`，可以保持禁用。`DHCP` 设置在稍后可以通过 Web 界面进行配置。

![](img/33fc180c04c8f96c022bce6e62ae12fd_334_0.png)

- 接下来的几个屏幕允许你在 Web 界面设置各种账户的密码。以下是这些账户的摘要：
- `Administrator` 用于通过 Web 界面管理防火墙。该账户仅用于 Web 界面，不能直接登录防火墙 Linux 系统。
- `root` 是用于直接访问防火墙 Linux 的本地账户。
- `setup` 用于运行设置程序的本地账户，登录 `setup` 时会自动启动。
- 在配置完最终密码后，CD-ROM 将弹出，系统将重启。当系统恢复后，你可以通过控制台使用 `root` 账户登录，或者首选方法是登录 Web 界面。默认 Web 界面位于 `http://smoothwall:81`，安全 HTTP 位于 `https://smoothwall:441`。`root` 和 `setup` 账户都可以通过端口 222 连接 `SSH`。

# 配置 Smoothwall

当你首次登录 `smoothwall` Web 界面时，界面如图 9.26 所示。

# 图 9.26 SmoothWall Web 界面

![](img/33fc180c04c8f96c022bce6e62ae12fd_336_0.png)
