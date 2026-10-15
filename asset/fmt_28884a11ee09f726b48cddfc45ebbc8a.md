
# Kali Linux 2 基础安全测试：使用攻击者使用的策略测试你的计算机系统安全

## 使用 Kali Linux

使用与攻击者相同的战术来测试你的计算机系统安全。

感谢我的家人对我无尽的支持和祈祷，你们真是上帝赐予的礼物！

感谢信息安全与网络安全社区的朋友们与我分享知识和时间。还要感谢我们当地书写协会的朋友们（特别是你，Bill！），如果没有你们的投入、陪伴和建议，这一切绝不会发生。

> “古人云：知彼知己，百战不殆。” —— 孙子

> “看，我把你们像羊送入狼群，所以要像蛇一样聪明，像鸽子一样。”。” 马太福音 10:16 (和定钦译本)

## 关于作者

Daniel W. Dieterle 在 IT 领域工作了超过20 年。在此期间，他在一家计算机支持公司工作，为纽约州北部和整个宾夕法尼亚北部的数百家公司提供计算机和网络支持。

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_3_0.png)

他还在一家财富500 强企业的数据中心工作过，曾在一家常春藤学院的计算机支持部门短暂工作，并在一家电气工程公司担任过主管。

在过去的 5 年里，Daniel 完全专注于安全领域。他创建并编写了“CyberArms 计算机安全博客”，他的文章发表在国际安全杂志上，并被技术实体和媒体引用。

Daniel 协助过许多安全培训课程和技术书籍，主要基于 Backtrack 和 Kali Linux。

### Daniel W. Dieterle

`Cyberarms@live.com`

`Cyberarms.wordpress.com`

## 基础 Metasploit 命令

核心命令

文件系统命令

网络命令

系统命令

捕获摄像头视频、截图和声音

运行脚本

玩转模块 - 从远程系统恢复已删除的文件

## 引言

## 社会工程防御

## 第14章 – 社会工程工具包 (SET)

## 启动 SET

## 批量邮件发送器

# SET 的 Java PYInsector 攻击

## 社会工程工具包：PowerShell 攻击向量

## 使用 SET 进行更高级的攻击

## 第15章 - Subterfuge (欺骗)

## 使用 Subterfuge 进行自动浏览器攻击

## 浏览器自动利用

## 第五部分 - 密码攻击

## 第16章 – 破解简单的 LM 哈希

## 在线破解 LM 密码

## 在 Kali 中查询哈希

## 第17章 – 哈希传递攻击 (Pass the Hash)

## 使用 Psexec 传递哈希值

## 哈希传递工具包

## 防御哈希传递攻击

## 第18章 – Mimikatz 明文密码

## 加载模块

## 恢复哈希和明文密码

## 第19章 – Mimikatz 与 Utilman

## Utilman 登录绕过

## 从锁定的工作站恢复密码

## 第20章 - Keyscan 与锁定键盘记录器

# 使用 Metereter 记录键盘

## 使用 Lockout 键盘记录器自动化记录

## 第21章 - HashCat

## 破解 NTLM 密码

## 破解 NTLM 密码

## 破解密码

## 第22章 - 字典文件

## 破解字典

## 第23章 - 哈希传递

## 破解 Linux

## 第24章 - 路由器

## 破解路由器

## 第25章 - Fern

## 使用 Fern

# 26 - Fern

## 使用 Fern 进行攻击

技术，使用公司管理层设定的参数和准则来寻找安全问题。

随后，他们向管理层报告他们的发现并协助纠正这些问题。

> 我们不会涵盖过程中的每一个步骤，但将向你展示所使用的许多技术，以及如何防御这些技术。

我认为 Kali 优于商业安全解决方案最大的驱动因素是价格。安全测试工具可能极其昂贵，而 Kali 是免费的！其次，Kali 包含了许多商业安全产品的开源版本，因此你理论上可以仅通过使用 Kali 来替代昂贵的程序。

尽管 Kali 确实包含了几个流行软件运行的免费版本，这些版本可以升级为全功能的付费版本，并通过 Kali 直接使用。

Backtrack 和 Kali 之间在工具使用上没有主要区别。Kali 基本上是 Backtrack 版本 6，或者是 Backtrack 的最新版本。但它已经从底层开始完全重新工具化，使得软件更新和添加变得简单得多。

在 Backtrack 中，更新某些程序似乎会导致其他程序崩溃；而在 Kali 中，你使用 `Kali update` 命令更新所有内容，可以很好地保持系统完整性。

只需更新 Kali，它就会下载其中包含工具的最新版本。只需注意一点，单独更新工具可能会破坏 Kali，因此运行 `Kali update` 始终是获取操作系统最新包的最佳方式。

由于我们要处理的是有漏洞的操作系统，请确保在宿主机系统和公共互联网之间有一个防火墙路由器（最好是硬件设备）。

## 安装 VMware Player & Kali

在 VMware 上安装 Kali 极其简单，因为 Offensive Security（攻防安全）提供了一个可以直接下载的 Kali VMware 镜像，所以我们不会在这一步花费太多时间。

下载并安装适用于您操作系统版本的 VMware Player。

- 1. 下载并安装 VMware Player (`https://my.vmware.com/web/vmware/downloads`)

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_17_1.png)

- 2. 同意许可协议并选择您想要安装的位置，通常默认设置即可。

- 3. 完成后点击“完成（Finish）”。

下载 Kali VMware 镜像（`http://www.kali.org/downloads/`）并将其保存到您想要运行的地方。

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_18_0.png)

（注：通过下载的镜像验证 SHAISUM 是一个好习惯，以确保您拥有的是合法的镜像副本。有很多 MD5/SHA1 免费软件可用。）

- 5. 解压下载的镜像（使用 7-Zip 即可）。

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_18_1.png)

- 6. 启动 VMware Player。

- 7. 点击菜单中的“播放（Player）”。

- 8. 然后点击“文件（File）”。

- 9. 然后点击“打开（Open）”。

- 10. 浏览到提取出的 `.vmx` 文件，选中它并点击“打开（Open）”。

- 11. 它现在会出现在 VMware 主屏幕上。

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_18_2.png)

- 12. 选中 Kali 虚拟机，点击“编辑虚拟机（Edit Virtual Machine）”。

- 13. 在这里您可以查看并更改虚拟机的任何设置：

- 14. 点击“网络适配器（Network Adapter）”：

- 15. 默认设置为 NAT。这对于我们的工作已经足够了。NAT 意味着虚拟机将在一个与宿主机共享的小型 NAT 网络中创建；如果需要，它们也可以访问互联网。每台机器将获得一个 DHCP 地址，这意味着重启它们时 IP 地址可能会发生。如果您需要知道 Kali 或 Metasploitable 的 IP 地址，只需在终端窗口中输入 `ifconfig`。在基于 Windows 的虚拟机上，在提示符处输入 `ipconfig` 即可。

- 16. 点击“取消（cancel）”返回 VMware 主界面。

- 17. 现在只需点击“播放虚拟机（Play Virtual Machine）”来启动 Kali。您可能会收到消息询问虚拟机是被移动还是复制的，只需点击“我已复制它（I copied it）”。

- 18. 当提示安装 VMware Tools 时，选择稍后安装。

- 19. Kali 启动后，您将进入登录界面：

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_20_0.png)

- 20. 点击“其他（Other）”，然后用用户名“root”和密码“root”登录。

- 21. 随后您将登录 Kali 并看到主桌面：

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_20_1.png)

恭喜你，你做到了！

## 更新 Kali

我们稍后会介绍如何操作 Kali，但首先我们需要将 Kali 更新到最新版本。虚拟机镜像有点旧了，因此有很多更新可能需要一些时间下载。

- 1. 打开终端窗口：

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_21_0.png)

- 2. 输入 `apt-get update` 并按回车键：

```
root@kali:~# apt-get update
Get:1 http://http.kali.org/kali/InRelease [22.0 kB]
Get:2 http://http.kali.org/kali/updates/InRelease [11.8 kB]
Get:3 http://http.kali.org/kali/main [7,535 kB]
Ign http://http.kali.org/kali/contrib-en-US
Ign http://http.kali.org/kali/contrib-en-en
Ign http://http.kali.org/kali/main-en-US
Ign http://http.kali.org/kali/main-en-en
```

- 3. 输入 `apt-get dist-upgrade` 并按回车键：

```
root@kali:~# apt-get dist-upgrade
```

- 4. 当提示时输入 `y` 并按回车。

## 欢迎使用新虚拟机向导

虚拟机就像物理计算机；它需要操作系统。你将如何安装客体操作系统？

从以下位置安装：

- DVD RW 驱动器 (D):

请将安装光盘插入此驱动器以继续。

然后像往常一样安装 Windows 7。。

完成后，你将拥有一个 Windows 7 虚拟机：

![](img/3ef0f51cacb0127e8ad0ea42f248a9fe_25_0.png)

检查它的网络设置，确保它也使用 NAT 进行网络连接：

| 设备 | 摘要 | 设备状态 |
| --- | --- | --- |
| 内存 | 1 GB |  {机时连接 |
| 处理器 | | 网络连接 |
| 硬盘 (SCSI) | 40 GB | 桥接模式：直接连接到物理网络 |
| CD/DVD (IDE) | 自动检测 | 复制物理网络连接状态 |
| 软盘 | 自动检测 | |
| 网络适配器 | 自动检测 | 配置适配器 |
| USB 控制器 | 已存在 | NAT：用于共享主机的 IP 地址 |
| 声卡 | 自动检测 | 主机模式：与主机的专用网络连接 |
| 打印机 | 已存在 | 自定义：特定的虚拟网络 |
| 显示器 | 自动检测 | |

运行虚拟机并在 Windows 7 命令行提示符中运行“ipconfig”以查看其 IP 地址：

```
Microsoft Windows [Version 6.1.7601]

C:\Users\Fred>ipconfig

Windows IP 配置

以太网适配器局域连接:

IPv4 地址. . . . . . . . . . . . : 192.168.198.130
```

最后，如果你愿意，在提示时安装适用于 Windows 的 VMware Tools：
