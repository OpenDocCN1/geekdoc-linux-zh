

## Nessus 漏洞扫描

上述使用的 nmap 脚本在识别我们未打补丁的 Windows 7 系统中的那个单一漏洞时是有效的。对于那一个漏洞它是有效的，但远非全面。如果我们想要或需要扫描所有已知漏洞该怎么办？这正是像 Nessus 这样的漏洞扫描器所能做到的。尽管市场上有许多有效的漏洞扫描器，但 Nessus 是我最喜欢的，也是 44% 的安全工程师的最爱。Nessus 始于 Renaud Deraison 在 1998 年发起的一个开源项目（就像 Snort、Metasploit 以及许多其他信息安全项目一样）。2005 年，Deraison 的公司 Tenable Network Security 将这款软件转为专有和闭源。幸运的是，它仍然有一个免费的 Essentials 版本（以前称为 Home 版本），可以无限期免费使用，最多支持 16 个 IP 地址。

让我们用它来测试我们的 Windows 7 系统。

前往 [Nessus 页面](https://www.tenable.com/products/nessus/nessus-essentials) 并下载 Nessus 的 Essentials（家庭）版本。

https://www.tenable.com/products/nessus/nessus-essentials

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_233_0.png)

| 名称 | 描述 | 详情 |
| --- | --- | --- |
| Nessus-8.4.0-x64.msi | Windows Server 2008, Server 2008 R2*, Server 2012, Server 2012 R2, 7, 8, 10, Server 2016 (64-bit) | Checksum |
| Nessus-8.4.0-Win32.msi | Windows 7, 8, 10 (32-bit) | Checksum |
| Nessus-8.4.0-debian6_i386.deb | Debian 6, 7, 8, 9 / Kali Linux 1, 2017.3 i386(32-bit) | Checksum |
| Nessus-8.4.0-es5.i386.rpm | Red Hat ES 5 i386(32-bit) / CentOS 5 / Oracle Linux 5 (including Unbreakable Enterprise Kernel) | Checksum |
| Nessus-8.4.0-suse12x86_64.rpm | SUSE 12 Enterprise (64-bit) | Checksum |
| Nessus-8.4.0-ubuntu910_i386.deb | Ubuntu 9.10 / Ubuntu 10.04 i386(32-bit) | Checksum |
| Nessus-8.4.0-debian6_amd64.deb | Debian 6, 7, 8, 9 / Kali Linux 1, 2017.3 AMD64 | Checksum |
| Nessus-8.4.0-es6.i386.rpm | Red Hat ES 6 i386(32-bit) / CentOS 6 / Oracle Linux 6 (including Unbreakable Enterprise Kernel) | Checksum |
| Nessus-8.4.0-fc20.x86_64.rpm | Fedora 20, 21, 25, 26, 27 (64-bit) | Checksum |
| Nessus-8.4.0-ubuntu910_amd64.deb | Ubuntu 9.10 / Ubuntu 10.04 (64-bit) | Checksum |

点击以下载合适的版本。由于我在整本书中都使用 Kali，我下载了 Debian 6,7,8/Kali Linux 的版本（如前所述，Kali 基于 Debian 构建，就像 Ubuntu 一样）。

接下来，同意主许可协议（Master License）。

一旦 Nessus 下载完成，导航到你 Kali 系统上的 Downloads 目录。

```bash
kali > cd /root/Downloads
```

在 Downloads 目录中，你应该能看到你的 Nessus 包。现在，使用 `dpkg` 命令来解压并安装 Nessus。

```bash
kali > dpkg -i Nessus-8.5.1-debian6_amd64.deb
```

请注意，你下载的 Nessus 版本可能不同。请在 dpkg 命令的 -i 后面输入你的版本包名。

```bash
root@kali-2019:~# cd Downloads
root@kali-2019:~/Downloads# ls -l
total 75400
-rw-r--r-- 1 root root 77287016 Jul 18 09:08 Nessus-8.5.1-debian6_amd64.deb
root@kali-2019:~/Downloads# dpkg -i Nessus-8.5.1-debian6_amd64.deb
(Reading database ... 375790 files and directories currently installed.)
Preparing to unpack Nessus-8.5.1-debian6_amd64.deb ...
Shutting down Nessus .
Unpacking nessus (8.5.1) over (8.5.1) ...
Setting up nessus (8.5.1) ...
Unpacking Nessus Scanner Core Components...

 - You can start Nessus Scanner by typing /etc/init.d/nessusd start
 - Then go to https://kali-2019:8834/ to configure your scanner
Processing triggers for systemd (240-4) ...
```

```bash
root@kali-2019:~/Downloads# /etc/init.d/nessusd start
Starting Nessus : .
root@kali-2019:~/Downloads#
```

当安装完成后，我们接下来需要启动 Nessus。我们可以输入以下命令来启动它：

```bash
kali > /etc/init.d/nessusd start
```

现在，打开你的浏览器并前往 [https://localhost:8834](https://localhost:8834)。你的浏览器可能会抱怨连接不安全（Nessus 使用自生成证书）。忽略这些警告，为你的 Nessus 服务器创建一个安全例外并继续。

你应该会看到如下所示的 Nessus 界面。在这个界面上，你将创建你的 Nessus 服务器账户。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_237_0.png)

### 创建账户

要使用此扫描器，必须创建一个账户。此账户可以在远程目标上执行命令，并且应当被视为 root 用户。

- 用户名 *
- 密码 *
- 继续

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_239_0.png)

接下来，你需要输入 Nessus 通过电子邮件发送给你的激活代码。请确保将扫描器类型选为“Essentials”。

输入你的激活代码并点击继续。Nessus 现在开始初始化你的扫描器，下载插件和漏洞数据库。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_240_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_241_0.png)

### 初始化中

请在 Nessus 准备扫描资产所需文件时稍等。

正在下载插件...

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_241_1.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_242_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_243_0.png)

这可能需要一段时间。去拿你喜欢的饮料然后等待……然后也许再拿一杯。

当初始化完成后，使用你上面输入的凭据登录。

一旦我们登录 Nessus，就会看到“我的扫描（My Scans）”界面。由于我们还没有执行过漏洞扫描，这里暂时不会显示任何扫描。你可以看到右上角有一个标记为“新建扫描（New Scan）”的按钮。点击它以开始一个新的漏洞扫描。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_244_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_244_1.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_245_0.png)

这应该打开一个界面，询问你想要进行哪种类型的扫描。让我们选择顶部第二行左侧的“高级扫描（Advanced Scan）”。

这将打开一个界面，要求你为扫描命名（这只是一个标签），所以我把我的命名为“NewScan”。很有创意，对吧？你还需要输入描述、文件夹，以及最重要的，你想扫描的 IP 地址。这可以是 IP 地址列表或子网的 CIDR 表示法。

如果有很多 IP 地址，你可以上传一个包含 IP 地址的文件，位于底部附近。这里，我将只扫描我本地网络上的 Windows 7 系统（192.168.0.102）。

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_246_0.png)

### 新建扫描 / 高级扫描

- 返回扫描模板
- + 设置
- + 凭据
- + 插件
- + 基础
    - 常规
    - 计划
    - 通知
- + 发现
- + 评估
- + 报告
- + 高级

- 名称: New Scan
- 描述: 我对 Windows 7 的第一次 Nessus 扫描
- 文件夹: 我的扫描
- 目标: 192.168.0.102
- 上传目标: 添加文件

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_247_0.png)

### 我的扫描

- + 更多
- + 导入
- + 新建文件夹
- + 新建扫描
- 1 个扫描 (已选择 1 个)
- 清除已选项目

| 名称 | 计划 | 最后修改 |
| --- | --- | --- |
| New Scan | 手动 | 无 |

这将加载你的扫描并展示如下所示的界面。在最右侧，你会看到一个 | > 按钮。当你点击它时，你的扫描将开始。

当 Nessus 完成你的漏洞扫描后，打开该扫描，你将看到扫描的图形化表示。在我的情况下，有许多“信息（info）”级别的漏洞，两个中等级别的漏洞，以及两个

