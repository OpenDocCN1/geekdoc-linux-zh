
<用一行给出程序名称及其功能的简要说明。>

版权 (C) 19yy <作者姓名>

本程序是自由软件；您可以根据自由软件基金发布的 GNU 许可分发它/或修改它，可以是该许可的 2 版，或（根据您的选择）任何稍后版本。

本程序的分发是希望它是实用的，但没有任何保证；甚至没有对商品性或特定用途适用性的隐含保证。更多信息请参阅 GNU 许可。

您应该随本程序收到一份 GNU 通用许可副本；如果没有，请写信自由软件基金会：675 Mass Ave, Cambridge, MA 02139, USA。

以及如何通过电子邮件和纸质邮件与您联系的信息。

如果程序是交互式的，让它在交互模式启动时输出如下简短通知：

Gnomision 版本 69, 版权所有 ©19yy 姓名
Gnomision 绝对没有任何保证；详情请输入 `show w`
这是自由软件，您可以根据这些条款对其进行分发；输入 `show c` 查看详情。

条件结束

# Samba 常见问题解答

假设命令 `show w` 和 `show c` 应该显示通用公共许可协议（General Public License）的相关部分。当然，你使用的命令名称可能不是 `show w` 和 `show c`；它们甚至可能是鼠标点击或菜单项——任何适合你程序的即可。

如有必要，你应该让你的雇主（如果你以程序员身份工作）或你的学校（如果有）为该程序提供一份“版权免责声明”。以下是一个示例；请修改名称：

Yoyodoy, Inc. 此处声明对程序

<Gnomovision> (该程序对编译器进行了讽刺) 的所有权益由 James Hacker 编写。
<Ty Coon 的签名>, 1989年4月1日

Ty Coon，Vice 公司行长

本通用公共许可协议不允许将你的程序整合到专有程序中。如果你的程序是一个子程序库，你可能认为允许专有应用程序链接到该库更有用。如果你想这样做，请使用 GNU 库通用公共许可协议代替本许可协议。

## 作者注释

以下常见问题解答复制自 http://www.samba.com 的在线文档 SAMBA。它是根据上述列出的 GNU 许可证复制的。

此常见问题解答由 Samba 错误跟踪系统自动生成。因此，它包含了我们经常发送向 `samba-bugs@samba.org` 报告问题的用户的答案。请报告不准确或过时的信息，以便进行修复。

### 索引

- CRLF-LF 转换
- 已停止的 1.9.18
- 无法打开状态文件 STATUS..LCK
- 域控制器 (Domain Controller)
- 获取 NTDOM 代码
- IP 地址更改
- Linux & mmap()
- NT 事件查看器中的登录错误
- Macintosh 客户端
- NT 客客访问
- NT SP3 与加密
- NTDOMAIN 代码

### 附录 B：Samba 文档

- NetWkstaUserLogon
- 未监听调用名称
- 操作中断错误 (Op Break Errors)
- 请先阅读文档！
- PWL 文件
- 密码破解
- 披萨代券
- SMBFS 不是 Samba 的部分
- Red Hat Linux 上的 SWAT
- Samba 2.x 和 PAM (特别是 FreeBSD)
- 系统错误 1240
- 这不是帮助台
- 时间偏差 1 小时
- 陷门 UID
- Unix 权限控制访问
- 用户访问控制
- 使用 NT 浏览 Samba 共享
- Win95 或 98 与加密
- 用户访问模式下的 Win9X
- Windows98 密码
- XXX 不在用户级安全模式下
- YEK
- 大小敏感
- Comp.protocols.smb
- 不进入与安全 (Dont descend & security)
- 文件缓存
- 显示的通用图标
- Linux 2.0.x 和 smbmount
- Linux 编译问题
- 非所有者时设置时间
- Setup.exe 和 16 位程序
- Smbclient -N
- 用于其他 Unix 系统的 Smbfs
- Smbpasswd: 拒绝话请求
- Smsh 和 glibc-2.1
- Smbtar 块大小
- 取消
- Win98 运行缓慢
- 你的服务器软件不友好

## CRLF-LF 转换

我们收到许多关于由 Samba 处理 CRLF/LF 格式转换的请求。问题在于，没有简单的方法来确定哪些文件应该/可以转换，哪些绝对不能转换。

由于 Unix 和 DOS/Windows 的用法都使用 `.txt` 表示包含 ASCII 文本的文件，我们无法可靠地使用文件扩展名。`.doc` 扩展名也是如此。

Samba 的运行前提是我们应该保持所有文件不变。通过不实现 CRLF/LF 转换，我们不会对损坏任何人的文件负责。

当有人提供能够保证文件完整性的良好实现方案时，我们将抓住机会实现此功能。在此之前，该主题没有行动的预期。

## 已停止的 1.9.18

感谢你报告在使用 `samba-1.9.18` 系列代码时遇到的困难。我们遗憾的是，随着 `samba-1.9.18p10` 的发布，对 1.9.18 代码树的所有工作均已停止。

现在所有的开发工作都集中在稳定 `samba-2.0.0` 上，使其能够尽快进入稳定代码发布。

如果你能下载最新的 beta 版本并反馈你可能遇到的任何困难，我们将尽力在稳定发布之前解决它们。

我们仍然会修复 1.98p10 中的主要错误和安全漏洞，但如果问题在 2.0 tree中仍然存在，我们将修复可能会错误。

有关访问最新 CVS 源代码的信息，请参阅 http://samba.org/cvs.html

## 无法打开状态文件 STATUS..LCK

如果你在任何人连接到你的新 Samba 安装之前运行 `smstatus`，你可能会得到错误：

```
Couldn't open status file /var/lock/samba/STATUS..LCK
```

或者可能的错误：

```
ERROR smb_shm_open : open failed with code No such file or directory

ERROR: Failed to initialize share modes!

Can't initialize shared memory - exiting
```
