
## 19 设置备份

点击“添加”（`Add`）创建一个新任务并按你的意愿进行配置。将密钥类型选择为“备份源在目标内部”（`Backup Source inside Destination`），选择你的源，最后将目标设置为 `Google Drive` 文件夹。点击确定保存，然后点击任务旁的复选框激活它。

![](img/a17757b82ff78d9c8d36ac46319604f3_32_1.png)

## 18 更好的备份

这不是备份此类文件最高效的方法，尽管 `Linux` 带有许多备份数据的工具，其中包含通过 `cron` 实现的备份计划。我们将使用 `luckyBackup`：在包管理器中找到并安装它。

![](img/a17757b82ff78d9c8d36ac46319604f3_32_2.png)

## 21 定时备份

点击“完成”（`Done`）返回主菜单。点击“按计划配置”（`Profile by Schedule`）来绑定每日调度。计划是按配置的，你可以在其中运行多个不同的任务。点击“添加”开始为你的 `Drive` 创建计划。

## 22 计划

![](img/a17757b82ff78d9c8d36ac46319604f3_32_3.png)

计划会创建一个 `cron` 任务，因此你可以设定在每周的特定日期或月份、每天的时间以及任务应该发生的时间。如果你需要频繁备份，可以设置为每小时过一分钟执行一次。

## 23 反向备份

`Google Drive` 在其服务器上保留文件的历史版本；但并非永久保留。如果你正在备份或保存到云端，你可能也想为你的 `PC` 创建一份数据的反向备份。

## 24 驱动

虽然 `Linux` 还没有官方工具，但 `Grive` 和 `G Tools` 至少可以让你实现应该的功能。关注 `Drive` 和 `Tools` 的更新以查看任何新功能是否适合你。

# 教程：Zentymal Free 服务器

通过 `DynDNS` 进行某些远程访问，以及通过浏览器的 `Zentymal` 模块（服务器）可以在本地网络或任何地方进行配置。

![](img/a17757b82ff78d9c8d36ac46319604f3_33_0.png)

`Zentymal` 运行在 `Ubuntu` 之上——你可以从 `Zentymal` 仓库安装它。

# Zentymal 顾问

`Richard Smyth` 在 `Linux` 出现很久以前就开始从事计算，并仍然认为 `Linux` 是最高效的工作环境。`Zentymal` 提供了易于安装的服务器集合，用于如网关和统一管理器等任务。对于那些想要无缝获取 `FOSS` 的人，这也是特别好的选择。

`MS` 几年前放弃了这些业务工具，但许多客户现在正在寻找替代品。`Simon` 告诉我们 `Zentymal` 在他们的客户群中非常受欢迎。

`Zentymal 3.5`（代号）将帮助你在 `Ubuntu 14.04` 上运行服务器。但凭借其高可用性、去重和跨服务改进，通过 `ISO` 或在现有 `Ubuntu 13.10` 之上安装同样简单，因此我们将带你完成这一并展示 `Zentymal` 的功能。规格指定的 `PC Zentymal ISO www.zentymal.org/server`

# 教程：资源

为你的办公室网络提供一个 `Windows` 兼容服务器。

![](img/a17757b82ff78d9c8d36ac46319604f3_34_0.png)

![](img/a17757b82ff78d9c8d36ac46319604f3_34_1.png)

![](img/a17757b82ff78d9c8d36ac46319604f3_34_2.png)

| 特性 | `Ubuntu` | `CentOS` |
| --- | --- | --- |
| 基础设施 | 免费 | 付费 |
| 成本 | 低 | 高 |
| 社区 | 高 | 中 |
| 支持 | 社区 | 付费 |

![](img/a17757b82ff78d9c8d36ac46319604f3_34_3.png)

![](img/a17757b82ff78d9c8d36ac46319604f3_34_4.png)

# Zentymal 基础设施特性

### 01 硬件需求

在我们开始之前，你需要实际安装——但 `Zentymal` 的需求很小，即使是笔记本电脑也能满足许多需求（带有方便的 `UPS`）。

### 05 Unix 方式

你会注意到 `Zentymal` 放在你服务器上的许多依赖是胶水代码——执行单一任务的库。这是 `Unix` 方式，从小型、专门的程序构建。

### 08 向导角色

服务器角色被分组为模块。在这里你可以看到列出的基础设施模块，包括：`DHCP`、缓存、授权、`NTP` 和 `FTP` 服务器。

![](img/a17757b82ff78d9c8d36ac46319604f3_34_5.png)

# Zentymal Server 3.4

获取你的免费 `Zentymal Linux`！请注意试用版并非用于商业用途。

![](img/a17757b82ff78d9c8d36ac46319604f3_34_6.png)

![](img/a17757b82ff78d9c8d36ac46319604f3_34_7.png)

### 06 安全引导程序

你可能需要设置 `MySQL` 密码和依赖项，然后你就可以从跨本地网络安装 `Zentymal`。`HTTPS` 的默认端口为 `443`。

### 09 挑选

我们选择了网关（`Gateway`）作为服务器角色，因此涉及的十个模块被高亮。你可以选择任何区域，因为你以后可以添加额外的模块。

### 02 专用服务器

安装 `Zentymal` 有两种方法。如果你已经准备好硬件，可以使用 `Zentymal Server` 版本的镜像，或者在现有服务器上安装。

### 03 虚拟到位

如果这就是虚拟机所设置的——我们设置好了——但 `Ubuntu` 从功能开始的，所以我们带你通过……

### 07 信任

你将被提示使用 `Firefox` 对自签名证书的响应。在跨本地网络安装 `Zentymal` 期间确认证书。通常情况下，它是正确的，但我们正在去正确的地方。现在，这个

![](img/a17757b82ff78d9c8d36ac46319604f3_34_8.png)

# 此连接已受信任

你已添加密码以连接安全。

### 07 添加异常

你正在关于 `Firefox` 如何启动以及其他

### 我该怎么办？

如果你不想使用这个印象深刻的网站，那么你应该

# 证书状态

`https://zentymal.org/`

# 错误站点

证书属于不同的网站，这可能包括

# 技术细节

`127.0.0.1` 使用无效的安全证书。

该证书不受信任，因为它是自签名的。

# 我理解风险

如果这是你想做的，那么你就可以添加

# 添加异常

![](img/a17757b82ff78d9c8d36ac46319604f3_34_9.png)

### 04 添加 Ubuntu

不要只使用 `Ubuntu` 仓库中的 `Zentymal` 包。虽然它们可以使用，但你不会获得最新版本，也没有允许你 `apt get install` 的元包。

```
sudo apt-get update
sudo apt-get install apt-transport-https
wget -O - https://zentymal.org/zentral-key.gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/zentral.gpg
echo 'deb [signed-by=/etc/apt/trusted.gpg.d/zentral.gpg] https://zentymal.org/repo main' | sudo tee /etc/apt/sources.list.d/zentral.list
sudo apt-get update
sudo apt-get install central
```

![](img/a17757b82ff78d9c8d36ac46319604f3_34_10.png)

`35 www.linuxuser.co`

# 教程

# 使用 Zentanyl 从 MS 小型型业务服务器中解放出来

![](img/a17757b82ff78d9c8d36ac46319604f3_35_0.png)

`Zentanyl 社区版 3.4`

# 安装完成

# 12 (域名)

# 恭喜！

您的 `Zentanyl` 安装已成功完成！

现在您可以准备好配置并使用您的新 `Zentanyl` 服务器了。

- `Dashboard` (仪表板)
- `Module Status` (模块状态)
- `System` (系统)
- `Network` (网络)
- `Maintenance` (维护)
- `Registration` (注册)

前往仪表板

![](img/a17757b82ff78d9c8d36ac46319604f3_35_1.png)

# 10 图标朋友

在将邮件过滤器、网页邮箱和 `Web` 服务器添加到网关角色包并安装后，我们发现自己处于一个界面。这些图标和功能包比其他某些 `Linux` 安装程序要友好得多。
