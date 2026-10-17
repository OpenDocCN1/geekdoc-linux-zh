
`tar -cjf mybackup.tbz /etc /var /home /opt /usr/local`

## 保持更新

你维护列表中的最后一项是保持发行版软件更新。开源软件的真正伟大之处之一是，漏洞或安全缺陷在发现后很快就会看到。Red Hat 和其他发行版的作者会迅速发现补丁已在他们的软件中。

Red Hat 在 `redhat.com/errata/` 发布其所有更新，请此处检查最新软件包。每个修复包中还附有安装说明，所以你不需要猜测如何操作。如果你购买了 Red Hat 发行版的盒装版，可以利用更新程序，它可以自动处理整个过程。它连接到 Red Hat 网站，并将那里可用的修复包列表与你系统中安装的列表进行比较，使你的系统与 Red Hat 保持同步。

## 章节总结

本章检查了系统管理员面临的一些任务，例如监控日志、执行系统备份和执行系统恢复。虽然 Linux 管理曾是一门深奥的艺术，但 `Webmin` 等程序让它变得轻松且简单。

## 章节结束复习

## 关键术语

- 备份 文件系统检查 (`fsck`) `linuxconf` 工具
- `tar` UPS 虚拟桌面 虚拟网络计算 (Virtual Network Computing)
- `webmin` X server X Window System
- 回环地址 (Loopback address)

## 复习题

1. 列出 X Window 系统的三个组件。
2. 描述拥有虚拟桌面的好处。
3. 列出三种可能损坏甚至破坏你的 Linux 文件的情况。在这些中，作者认为哪种是有害的？
4. 如果你的服务器意外关闭或停止接受来自浏览器的连接，你应该检查什么？如何检查这些（列出两种方法）？
5. 下述命令实现了什么：

```
tar -cjf backup.tbz /var/www /home /opt /usr/local
```

## 编程作业

### 练习 1：使用 Webmin

1. 从 `www.webmin.com/webmin` 下载并安装 Webmin 的 RPM。
2. 从 Netscape 调用 Webmin 管理面板：

```
http://127.0.0.1:10000/
```

3. 当显示登录面板时，以 root 身份登录。
4. 检查 Apache 配置：
   a) 点击 Webmin 选项卡
   b) 点击 Apache server 链接。
   c) 在 Global Configuration（全局配置）部分下检查设置。
5. 从 Hardware（硬件）选项卡检查磁盘使用情况。列出可用空间。

### 练习 2：研究 UPS

1. 寻找三个 UPS 供应商。
2. 列出网站地址、价格和若干功能。

### 练习 3：监控设施

1. 使用 Webmin，点击 System 选项卡。
2. 查看以下日志：
   * `/var/log/messages`
   * `/var/log/secure`

### 练习 4：执行例行维护

1. 使用 Webmin，点击 System 选项卡，然后点击 Scheduled Cron。
2. 点击 Logrotate 链接确定 `logrotate` 命令何时执行。
3. 使用 `tar` 工具备份：

```
tar -cjf mybackup.tbz /etc /var /home /opt /usr/local
```
