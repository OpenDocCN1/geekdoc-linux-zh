
如果你有网络打印机，可以将其配置为非本地设备。例如，如果你有一个带有 JetDirect 接口的高端 HP LaserJet，请选择“网络 Jet-Direct”而不是“本地连接”。

Linux 并行（打印机）端口对应 Windows 打印机端口。Linux 的 `l1p0` 等于 `LPT1`，`/dev/l1p1` 等于 `LPT2`。

## 配置网络打印机

- 5. 点击本地打印机设备（通常应列为 `/dev/l1p0` 或 `/dev/l1p1`）并点击“下一步 (Forward)”按钮。

弹出“打印机型号”窗口。

- 6. 点击下拉菜单并选择你的打印机制造商。例如，选择 Epson。出现制造商型号列表。滚动型号列表并选择你的打印机型号。

某些打印机带有多个驱动程序。请选择最适合你打印机的驱动程序。如果你不知道哪种驱动程序最好，请使用尝试法。

- 7. 点击“下一步 (Forward)”按钮。

- 8. 在新窗口中点击“完成 (Finish)”按钮，打开“问题”对话框。点击“是 (Yes)”按钮并返回“打印机配置”窗口。

- 9. 点击“应用 (Apply)”按钮，Linux 打印守护进程 `l1pd` 重启并使新配置生效。

![](img/453364505e32ffec24f7d88ac7824962_249_0.png)

配置工具向打印机发送测试页。如果页面打印正常，点击“信息”对话框中的“是 (Yes)”按钮。

- 10. 选择“操作-退出 (Action-Quit)”关闭配置工具。

![](img/453364505e32ffec24f7d88ac7824962_250_0.png)

图 16-4：队列名称窗口。

打印机配置向导允许你返回并编辑或删除打印机配置。

## 配置 Linux 客户端通过打印服务器打印

Samba 让将打印机共享给 Linux、Unix 和 Windows 计算机变得简单，因为所有这些类型都可以会话消息块 (SMB) 协议；SMB 是 Windows 分享财富的一种（呵呵，就得如此）。

Samba 默认配置为自动导出默认 Linux 打印机。这成功了一半！你不需要配置服务器；只需要配置每个客户端。

通过重复……中的步骤来配置 Linux 客户端通过 Linux 打印机打印（等待，OCR 文本此处中断或跳跃，让我们根据提供的文本流进行重新对齐）。

## 配置 Linux 客户端通过打印服务器打印

Samba 让将打印机共享给 Linux、Unix 和 Windows 计算机变得简单，因为所有这些类型都可以会会话消息块 (SMB) 协议；SMB 是 Windows 分享财富的一种（呵呵，就得如此）。

Samba 默认配置为自动导出默认 Linux 打印机。这成功了一半！你不需要配置服务器；只需要配置每个客户端。

通过重复……中的步骤来配置 Linux 客户端通过 Linux 打印机打印（注意：源文本此处跳转到了新章节“构建 DNS”）。我将遵循提供的文本块。

## 构建 DNS

Samba 让将打印机共享给 Linux、Unix 和 Windows 计算机变得简单，因为所有这些类型都可以会会话消息块 (SMB) 协议；SMB 是 Windows 分享财富的一种（呵呵，就得如此）。（等待，提供的文本存在大量重复和混乱，我将按照提供的文本块进行处理）。

## 配置 Linux 客户端通过打印服务器打印

Samba 让将打印机共享给 Linux、Unix 和 Windows 计算机变得简单……

## 构建 DNS

- *权威名称服务器 (Authoritative name servers)*：每个区域必须有一个有一个名称服务器。它持有该区域内所有主机的信息。你可以创建主服务器和从服务器来备份主服务器。

- *非权威名称服务器 (Non-authoritative name servers)*：你可以创建不一定提供最新信息的名称服务器。

- *缓存名称服务器 (Caching name server)*：名称服务器可以配置为查询其他名称服务器并临时保存信息。缓存名称服务器有助于分担大型领域的负载。

- *根名称服务器 (Root name servers)*：控制域名注册的机构提供根名称服务器，持有每个域名的名称服务器地址。DNS 查询到根名称服务器以查找权威名称服务器。

- A 记录：地址 (A) 记录将 IP 名称映射到数字地址。

- C 记录：规范 (C) 记录定义了 A 记录的别名。

- MX 记录：邮件交换 (MX) 记录指定服务该域名的邮件服务器。

- NS 记录：名称服务器 (NS) 记录指定区域的名称服务器。

- SOA 记录：起始授权 (SOA) 参数创建了一个描述区域通用属性的章节……SOA 配置了设置序列号和各种超时时间的参数，外外加上区域的域名。

## 理解 DNS 请求是如何运作的

- 1. 你打开浏览器并输入 URL www.redhat.com。

- 2. 浏览器向 Linux 请求 Web 页面的数字地址。

- 3. Linux 检查其 `/etc/resolv.conf` 配置文件并找到名称服务器的地址。

# 232 第四部分：书呆虫的复仇

你可以使用互联网上任何一个 DNS 服务器。例如，你可以从互联网的任何地方使用阿尔伯克基最优秀的 ISP——西南west Cyberport DNS 服务器，198.59.115.2。你应该使用自己 ISP 的服务器，因为它们需要经过的路由器（或跳数）较少，这会带来更好的可靠性和速度。

![](img/453364505e32ffec24f7d88ac7824962_253_0.png)

- 4. Linux 向名服务器请求 www.redhat.com 的 IP 地址。

- 5. 如果名服务器不知道 www.redhat.com 的 IP 地址，它会向根服务器请求 redhat.com 域的权威名称服务器的地址。

- 6. 根服务器返回 Red Hat 权威名称服务器的地址，其中第一个是 nsl.redhat.com (66.187.233.210)。

- 7. 名服务器向 nsl.redhat.com 询问 www.. 的地址。

- 8. 名服务器 nsl.redhat.com 返回 www.redhat.com 的地址。

- 9. 使用数字化的 www.redhat.com IP 地址，你的浏览器开始与 Web 服务器通信。

## 构建 DNS 服务器

是时候构建服务器了。本节的步骤描述了如何为你的私有网络构建权威名称服务器。该服务器为第 15 章中描述的不可路由私有网络提供地址。因此，你不需要向任何机构注册地址。DNS 服务器对于你的私有域是权威的，但这些信息在你的网络之外不可用。

本节的步骤展示了如何安装 DNS 软件。你需要创建 `/etc/named.conf`、`/var/named/local.zone`、`/var/named/paunchy.zone` 和 `/var/named/1.168.192.zone` 文件。

## 安装 DNS 软件

首先安装名服务器软件的 bind RPM 包：

- 1. 以 root 身份登录你的电脑并插入此书的配套 DVD-ROM。

- 2. 启动 GNOME Terminal 会话。

- 3. 在终端模拟器窗口输入此命令：

```
rpm -ivh /mnt/cdrom/RedHat/RPMS/bind-9*
```

现在你必须创建 DNS 配置文件 `/etc/named.conf`：

# 第 16 章：创建基础 Linux 网络服务

## 创建 DNS 配置文件

这些步骤描述了如何创建一个基本的 named.conf 文件：

- 点击 GNOME 菜单按钮并选择“应用程序(Accessories)-> 文本编辑器(Text Editor)”。

- 在 Gedit 窗口中输入以下配置：

```options
options ( directory /var/named );
zone "." {
    type hint;
    file "named.ca";
};
zone "localhost" {
    type master;
    file "localhost.zone";
};
zone "paunchy.net" {
    type master;
    file "paunchy.zone";
};
zone "1.168.192.in-addr.arpa" {
    type master;
    file "1.168.192.zone";
};
```

此列表描述了 `/var/named` 文件的各个部分：

- `options` 部分将 `/var/named` 目录定义为数据库文件的位置。你可以配置更多选项。输入命令 `named.conf` 获取更多信息。

- `named.ca` 部分定义了为整个互联网服务的服务器。

- 第一个 `zone` 部分 `localhost` 定义了内部环回接口的器服务器。

- 第二个 `zone` 部分设置了 `paunchy.net` 域或区域的主服务器，该服务器位于 `/var/named/paunchy.zone`。
