
<用一行字说明程序的名称及其功能概述的简要构想。>

```
```

Copyright (C) 19yy <作者姓名>

```

本程序是自由软件；你可以根据自由软件基金发布的 GNU 通用公共许可对其进行重新分发或修改；可以是许可的第 2 版本，或（根据你的选择）任何后续版本。

本程序的分发是希望它是有用的，但不提供任何保证；甚至没有对可销卖性或特定用途适用性的暗示保证。更多细节请参见 GNU 通用公共许可。

你应该在收到此程序的同时获得一份 GNU 通用公共许可的副本；如果没有，请致信 Free Software Foundation, Inc., 675 Mas Ave, Cambridge, MA 02139, USA。

另外添加如何通过电子邮件和纸质邮件联系你的信息。

如果程序是交互式的，请让它在交互模式下启动时输出如下短通知：

```
Gnomision version 69, Copyright ©19yy 作者姓名

Gnomision 绝对不提供任何保证；详情请输入 show w'.
```

这是一个自由软件，你可以在某些条件下对其进行重新分发；详情请输入 'show c'。假设的命令 'show w' 和 'show c' 可以被命名为 `show w` 和 `show c` 以外的其他——取决于你的程序。

你还应该让你的雇主（如果你是程序员）或你的学校（如果有）为程序签署一份“版权免责声明”。这是一个示例，请修改名称：

Yoyodyne 此处放弃对程序的版权权益

‘Gnomision’（对编译器进行处理）由 James Hacker 编写

Ty Coon 签名，1989年4月1日

Ty Coon，Vice 公司总裁

此通用公共许可不允许将你的程序整合到专有程序中。如果你的程序是一个子程序库，你可能认为允许专有应用程序与该库链接会更有处。如果你想这样做，请使用 GNU 通用公共许可代替本许可。

## 附录 D：Samba 文档

### 244

- NT 事件查看器中的登录错误
- Macintosh 客户端
- NT 来访问
- NT SP3 与加密
- NTDOMAIN 错误
- NetWkstaUserLogon
- 未监听调用名称
- OpLock 断开错误
- 请务必先阅读文档！
- PWL 文件
- 密码破解
- 披萨优惠券
- SMBFS 属于 Samba 的
- 红帽 Linux 上的 SWAT
- Samba 2.x 和 PAM（尤其是 FreeBSD）
- 系统错误 1240
- 这不是帮助台
- 时间偏差 1 小时
- 陷门 UID
- Unix 权限控制访问
- 用户访问控制
- 使用 NT 浏览 Samba 共享
- Win95 或 98 与加密
- 用户级访问模式下的 Win9X
- Windows98 密码
- XXX 不在用户级安全模式下
- Y2K
- 大写敏感
- Comp.protocols.smb
- 不要进入 & 安全
- 文件缓存
- 显示通用图标
- Linux 2.0.x 和 smbmount
- Linux 编译问题
- 非所有者设置时间
- Setup.exe 和 16 位程序
- Smbclient -N
- 其他 Unix 的 Smbfs
- Smpasswd: 拒绝会话请求
- Smbsh 和 glibc-2.1
- Smbtar 块大小
- 取消订阅
- Win98 运行缓慢
- 您的服务器软件不够友好

### 245

## CRLF-LF 转换

我们收到许多关于 Samba 处理 CRLF/LF 格式转换的。问题在于，没有一种简单的方法确定哪些文件应该转换，哪些绝对不能转换。

由于 Unix 和 DOS/Windows 都使用类似 `.txt` 的扩展名来表示包含 ASCII 文本的文件，我们无法可靠地使用文件扩展名。`.doc` 扩展名也是如此。

Samba 的运行前提是我们应该保持所有文件不变。通过不实现 CRLF/LF 转换，我们就不必承担损坏任何人文件的责任。

当有人提供了一种能够保证文件完整性的良好实现方案时，我们将抓住机会实现这一功能。在此之前，该主题没有行动前景。

我们仍然会修复 1.9.18p10 中的主要错误和安全漏洞，但如果小错误在 2.0Tree 中仍然存在，则会被修复。

有关访问最新 CVS 源码的信息，请参阅 `http://samba.org/cvs.html`。

## 已关闭 1.9.18

感谢您反馈在使用 `samba-1.9.18` 系列代码时遇到的困难。我们遗憾地通知，随着 `samba-1.9.18p10` 的发布，对 1.9.18 代码树的所有工作已关闭。

现在所有的开发工作都集中在稳定 `samba-2.0.0` 上，以便其尽快进入稳定代码发布。

如果您能下载最新的 beta 版本并反馈您可能遇到的任何困难，我们将尽力在稳定版之前解决它们。

我们仍然会在 `1.9.18p10` 中修复主要错误和安全漏洞，但如果小错误在 2.0Tree 中仍然存在，则会被修复。

有关访问最新 CVS 源码的信息，请参阅 `http://samba.org/cvs.html`。

## 无法打开状态文件 STATUS..LCK

如果在任何人都连接到您的新 Samba 安装之前运行 `smbstatus`，您可能会得到错误：

```
Couldn't open status file

/var/lock/samba/STATUS..LCK
```

或者可能的错误：

```
ERROR smb_shm_open : open failed with code in
file or directory
ERROR: Failed to initialize share modes!
Can't initialize shared memory - exiting
```

这两个错误都是无害的。在第一次连接到 Samba 时，适当的文件和内存段会自动创建。通过 `smbclient` 连接后，您会发现从第一次连接后 `smstatus` 就恢复正常了。

## 域控制器

- 遇到未知参数："domain controller"
- 忽略未知参数 "domain controller"

从 1.9.18 起，“domain controller”参数已经发生了变化。您可能不再需要它，但在其对应位置，可能需要“networkstation logon = yes”。在使用此选项**之前**，请检查 `smb.conf` 手册页，以了解其重要性。

## 获取 NTDOM 代码

域控制器代码现在已集成到 Samba 主源码中。

有关如何下载最新版本的信息，请参阅 `http://samba.org/cvs.html`。您可能也加入 `samba-ntdom` 邮件列表。详情请参阅 `http://lists.samba.org/`。

Samba 网站的文档（`http://samba.org/samba/`）中也有独立的 Samba NTDOM 常见。

## IP 地址更改

以下是我们偶尔看到的一个问题示例：

“Samba 之前一直运行良好。我们必须更改 Samba 服务器的 IP 地址。更改后 Samba 就不工作了。我们尝试了一切方法——它仍然不起用！”

要检查的项目：

### 247

1) 遵循 `samba` 文档目录下 `DIAGNOSIS.txt` 中的所有指令。

2) 找到您的 `browse.dat` 和 `wins.dat` 文件。它们可能位于以下典型位置：

- `/usr/local/samba/var/locks`
- `/var/locks/samba`
- `/opt/samba/var/locks`

如果您能找到 `samba` 存储这些文件的位置，可以随时运行：

```
testparm | grep lock
```
