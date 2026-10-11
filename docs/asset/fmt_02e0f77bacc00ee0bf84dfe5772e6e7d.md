
```
cp /usr/src/linux/arch/i386/boot/bzImage /boot
```

> 如果你之前重新编译过内核，请小心不要覆盖现有的 `/boot/bzImage` 文件！在充分测试新内核之前，不要覆盖现有的内核镜像。给新内核镜像一个不同的名称，例如 `/boot/bzImage.new`。

![](img/9102b40bb114da6b158a518630807d57_272_0.png)

要测试新内核，你必须重启。在此之前，你必须告诉 LILO 你构建了一个新内核。

LILO 的选项在 `/etc/lilo.conf` 文件中配置。你现有的 `lilo.conf` 文件应该类似于列表 A-1。

## 附录 A：重新编译 Caldera OpenLinux 2.3 内核

### 列表 A-1 默认的 `/etc/lilo.conf` 文件。

```
#
#etc/lilo.conf - 由 Lizard 生成
#

# target

boot = /dev/hda3
install = /boot/boot.b

# options

prompt
delay = 50
timeout = 50
message = /boot/message

default = linux

other = /dev/hda1
label = win

image = /boot/vmlinuz-pc97-2.2.10-modular
label = linux
root = /dev/hda3
vga = 274
read-only
  append = "debug=2 noapic nosmp"
```

`image =` 之后的内容告诉 LILO 关于你的内核的信息以及如何加载它。复制这些行，使得有组 `image =` 行，后面跟着它们的选项。修改第一行以指向你刚刚生成的新内核路径，并修改第二行使 `label` 变为 `linux.old`。列表 A-2 显示了你的结果应该是的样子。

### 列表 A-2 修改后的 `/etc/lilo.conf` 文件。

```
# /etc/lilo.conf
# /etc/lilo.conf - 由 Lizard 生成
#

# target

boot = /dev/hda3
install = /boot/boot.b

# options

prompt
delay = 50
timeout = 50
message = /boot/message

default = linux

other = /dev/hda1
label = win

image = /boot/vmlinuz-pc97-2.2.10-modular
label = linux
root = /dev/hda3
vga = 274
read-only
  append = "debug=2 noapic nosmp"
```

| URL | 资源名称 |
|---|---|
| http://linuxdoc.org/HOWTO/Kernel-Installation | Linux 内核 |
| http://cheek.com/page.php?kernel | 内核页面 |

## 附录 B：CD 上有什么？

### 运行 CD

#### Prima 许可证

#### Prima 用户界面

随书的 CD 包含了各种网络工具、示例配置文件以及完整的知识库。

![](img/9102b40bb114da6b158a518630807d57_277_0.png)

这张 CD 设计用于 Linux 下运行。然而，你可以在任何图形查看器中浏览 CD。

-1. 将 CD 放入托盘。
2. 以 root 身份输入：`mount /dev/cdrom/tmp`（将 `tmp` 替换为你想挂载的地方）。
3. 启动 X 会话 (`startx`)。
4. 打开 Netscape Navigator。
5. 从文件菜单中选择 Open，然后点击浏览按钮。
6. 浏览到 `start_here.html`。
1. 将 CD 放入 CD-ROM 驱动器，并关闭托盘。
2. 进入控制面板并双击 CD-ROM 驱动器。
3. 启动 `start_here.html`（Netscape 和 Internet Explorer 均可）。

# 索引

## A

- `(Address)` 资源资源，对比 PTR (指针), 79
- 访问 Apache Web 服务器, 95–96
- FTP 服务器，WU-FTPD 配置, 152–154, 158–161
- 远程访问 Linux 系统（参见 Radius (远程认证拨号用户服务)）
- 网络（另另 `ssh` (安全外壳);`telnet`）
- 带有 `smbclient` 实体的 SMB 共享
- OpenLinux 系统, 43–44
- Windows NT 系统, 44–45
- `squid` 服务器, 221–222
- Active Directory (Windows 2000)，Samba 不支持, 7
- `(Address)` 资源资源，对比 PTR (指针), 79
- 模拟分析仪，`squid` 代理服务器, 232
- 用于 Apache Web 服务器的模拟统计分析程序, 116
- 匿名 FTP 账户, 146
- 章节, 147–149
- Apache Web 服务器
    - 基础配置, 93
    - 全局访问, 95–96
    - 服务器请求管理, 95
- Asart Technologies; Powell, Patrick (`LPRng` 开发者), 8
- 认证
    - RADIUS 认证过程, 181
    - `radius`, 11
    - 管理, 183
    - 定义, 181–182
    - 安装二进制文件, 183
    - 安装源码, 182–183
    - 概述, 180
    - 用户配置文件, 184–191
- DNS
    - 配置, 74–76
    - `hosts`，添加和配置, 81
    - 名称解析器, 82
    - 根缓存, 77
    - 文件 (`switch files`), 82
    - 区域权限创建, 78–80
    - 启动/停止, 83
    - 状态检查, 84–85
    - 系统日志检查, 85–86
- `Bind/Active` 指令，Apache Web 服务器安全, 108–111
- 广播名称解析 (`WINS`)，Samba `nmb` 进程, 34

## B

- BDCs (备份域控制器), 36
- `bind` (伯克利互联网域名守护进程), 8–9
- 命令
    - `dig`, 87
    - `host`, 86–87
    - `slookup`, 88–89
- `coastool`, 18
- `finger`, `sendmail` 状态检查, 139–140
- `lsmod | grep smbfs`, 39
- `dc` 程序
    - `dumpdb`, 85
    - `start`, 83
    - 状态, 84–85
    - `stop`, 83–85
- `rmmod smbfs`, 39
- `route`, 22–24
- `rpm`，安装 WU-FTPTP, 150–151
- `samba` 启动/停止, 39
- `submount`, 36, 39
- 输出状态报告, 85
- 启动/停止, 83
- 故障排除, 83–84
- 配置
    - 基础, 73–76
    - `hosts`, 81
    - 名称解析器, 82
    - 根缓存创建, 77
    - 区域权限创建, 78–80
    - 层次结构, 72–73
    - 查询, 71
- 域主主浏览器 (DMBs), 35
- 域名系统。参见 DNS (域名系统)

## C

- 缓存管理器，`squid` 代理服务器, 229–230
- `calamaris` 日志分析器，`squid` 代理服务器, 232
- Caldera Network Desktop，与 LSTM 发发行版合并, 4
- Caldera 开放管理系统。参见 COAS (Caldera 开放管理系统)
- Caldera Systems, Inc. OpenLinux。参见 OpenLinux
- CD-ROM (附加) 内容, 258–259
- CHAP (挑战握手认证协议)，RADIUS, 196
- `checkpc` 程序, 64
- CD-ROM 中的 Check Consulting 知识库, 258
- CIFS (通用互联网文件系统)，与 Samba 的关系, 33
- COAS (Caldera 开放管理系统), 4–5
- 配置打印机共享, 61–64
- 安装网络卡驱动, 18–20
- IP 地址
    - 分配多个 IP, 20–22
    - IP 转发选项, 23
    - 挂载 NFS 目录, 55–56
- 网络管理
    - 网络的启动和关闭, 25–26
