
- 23). 修复 Samba 崩溃错误。
- 24). 修复 Samba 崩溃错误。
- 25). 修复 Samba 崩溃错误。
- 26). 修复 Samba 崩溃错误。
- 27). 修复 Samba 崩溃错误。
- 28). 修复 Samba 崩溃错误。
- 29). 修复 Samba 崩溃错误。
- 30). 修复 Samba 崩溃错误。
- 31). 修复 Samba 崩溃错误。
- 32). 修复 Samba 崩溃错误。
- 33). 修复 Samba 崩溃错误。
- 34). 修复 Samba 崩溃错误。
- 35). 修复 Samba 崩溃错误。
- 36). 修复 Samba 崩溃错误。
- 37). 修复 Samba 崩溃错误。
- 38). 修复 Samba 崩溃错误。
- 39). 修复 Samba 崩溃错误。
- 40). 修复 Samba 崩溃错误。
- 41). 修复 Samba 崩溃错误。
- 42). 修复 Samba 崩溃错误。
- 43). 修复 Samba 崩溃错误。
- 44). 修复 Samba 崩溃错误。
- 45). 修复 Samba 崩溃错误。
- 46). 修复 Samba 崩溃错误。
- 47). 修复 Samba 崩溃错误。
- 48). 修复 Samba 崩溃错误。
- 49). 修复 Samba 崩溃错误。
- 50). 修复 Samba 崩溃错误。
- 51). 修复 Samba 崩溃错误。
- 52). 修复 Samba 崩溃错误。
- 53). 修复 Samba 崩溃错误。
- 54). 修复 Samba 崩溃错误。
- 55). 修复 Samba 崩溃错误。
- 56). 修复 Samba 崩溃错误。
- 57). 修复 Samba 崩溃错误。
- 58). 修复 Samba 崩溃错误。
- 59). 修复 Samba 崩溃错误。
- 60). 修复 Samba 崩溃错误。

# Samba 2.0 的重大更改

这是一个 Samba 的重大版本，针对 Windows 系统的 SMB。自上一个主要版本 1.9 以来有许多变化。

### 1). 速度

Samba 在高端硬件上进行了基准测试。为了优化性能，进行了许多重大更改。

### 2). 正确性

Samba 现在支持 Windows 请求。这意味着对于能够处理大文件的 Windows 。

![](img/166cd29830b01a9e3eceb33240be1bcf_547.png)

### 3). 可移植性

Samba 现在使用 GNU autoconf 进行自动配置，消除了以前安装 Samba 需要手动配置 Makefile 的需求。现在通过运行 `./configure` 然后 `make` 来配置 Samba。详情请查看 `/docs/textdocs/UNIX_INSTALL.txt`。

### 4). 基于 Web 的 GUI 配置

Samba 现在带有 SWAT，一个基于 Web 的 GUI 系统。

### 5). 跨协议数据完整性

定义了一个开放接口，允许 Samba 授予的机会性锁被其他 UNIX 进程可见。这允许支持此功能的 Samba 平台实现跨协议（NFS 和 SMB）数据完整性。

### 6). 域能力

Samba 现在能够像 Windows NT 工作站一样使用 Windows NT PDC 进行用户认证，即它可以成为域成员。详情请查看 `/docs/textdocs/DOMAIN_MEMBER.txt`。

### 7). 文档更新

Samba 文档的所有引用（手册）都已更新并转换为允许自动生成 HTML、SGML 和文本格式的格式。这些文档现在以标准的 HTML 和手册格式分发。

# 第13章 未来

******结束重要说明******

此外，Samba 现在默认的大写敏感性选项与 Windows NT 服务器精确匹配，即：不区分大小写但保留大小写。

此发行版本的 `smpasswd` 文件的默认格式也发生了更改，尽管为了向后兼容性，新工具将能够读取和写入旧格式。

注意 - 主域控制器（Primary Domain Controller）功能

此版本的 Samba 包含了正确实现未文档的主域控制器认证协议的代码。然而，作为主域控制器，其功能远比仅仅服务 Windows NT 登录请求要复杂得多。

一个实用的主域控制器版本包含许多远程过程调用（RPC），用于列出用户、组和安全信息等操作，而 Samba 目前仅实现了其中的一部分。此外，此版本中 Samba 作为 PDC 存在一些待解决的（已知）漏洞，Samba 团队正在积极解决这些问题。由于这些原因，我们选择不在此发行版本中宣传和支持主域控制器功能。

这项工作正在 Samba 的 CVS（开发版）中进行，其开发工作仍在快速推进。如果你有兴趣参与或帮助这项开发，请加入 Samba-NTDOM 邮件列表。加入详情请见：

```
http://samba.org/listproc/
```

获取 Samba CVS（开发版）版本的详情请见：

```
http://samba.org/cvs.html
```

如果你发现了漏洞，请发送邮件报告至：

```
samba-bugs@samba.org
```

一如既往，所有的漏洞都是我们的责任。

此致，

Samba 团队

Samba 团队为自己制定了一系列目标，在任何方向你都能找到一个名为 Roadmap 的文件。这里包含了随 Samba 2.0.5a 发行版附带的文件摘要：

当前的 Samba 版本 2.0.5a 是对 Samba 2.0.4 版本进行一系列增强和漏洞修复的结果，Samba 称之为“NT 安全更新”。此版本实现了 Windows NT 特有的 SMB 调用，允许 Samba 作为 Windows NT 域环境中的客户端正常运行。

# 未来

从 2.0.0 版本开始，发行版还包含了 SWAT，这是基于 Web 的 GUI 管理工具的首次实现。这是 2.0.0 随包的一部分，因此实现了 1.9.18 版本 Roadmap 文档中承诺的某些内容。

已在确保与 Windows NT 5.0（现为 Windows 2000-）兼容性方面完成了一些工作——这是一个（缓慢）移动的目标。

未来发行版本的开发目标如下：

- 2.0.x—“NT 安全更新”——允许 Windows NT 客户端使用原生工具操作文件安全和所有权
- 注意，Roadmap 中的“NT 安全更新”部分已通过 Samba 2.0.4 版本实现
- 2.0.xx—“薄服务器”模式——允许将 Samba 服务器插入到没有 Unix 设置的网络中
- 提供使用原生 NT 工具对 Samba 进行某些管理的能力。
- 2.X—“域控制器”——能够作为 Windows NT PDC。
- X.XX—“全域集成”——允许 PDC 和 BDC 模式。

请注意，Samba 团队将继续跟踪 Windows (NT/ 2000) 的更新发布，确保 Samba 能够与雷德蒙投掷给我们的任何“Beta”版本良好地工作 :-

你可能还会注意到，目标越接近未来，版本号就越模糊。这是刻意的，因为我们还无法承诺确切的时间表。

# Windows 2000 与 Samba

当前的 Windows 2000 测试版是 beta 3，它可以与 Samba 一起安装和使用。至少需要 2.0.5a 版本。Samba 团队不会 Windows 2000 的使用或某些最新功能发表过多评论，特别是因为它被认为是处于开发中的软件。编写此书的系统将成功运行 Windows 2000 并连接到 2.0.5a Samba 服务器。

然而，所使用的密码加密似乎引发了一些问题，目前使用 Windows 2000 客户端的唯一方法是使用与其他 Windows 操作系统类似的明文密码注册表。

涉及的注册表键为 `[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkStation\Parameters]`。参数

![](img/166cd29830b01a9e3eceb33240be1bcf_550_0.png)

`EnablePlainTextPassword` 设置为 dword:00000001。最新的 Samba 发行版也包含此项的 .reg 文件。另一个似乎有效的步骤是将 `smb.conf` 参数 `nt pipe support` 设置为 `no`。

对于 Samba 控制的 NT 域，步骤在概念上没有区别。Samba 目前没有服务器管理器 GUI 界面，因此目前必须手动创建机器账户。我确定基于 Samba 的还原服务器器的 GUI 最终会出现。

# Windows NT 打印机支持

目前，Samba 不支持 Windows NT 打印。尽管已经完成了大量的开发，但这仍处于初步阶段。Windows NT 打印机功能很快出现在 Samba 发行版中。

# 远程过程调用尚未完成

如果你在 Windows 9x 中使用共享，请在资源管理器中选择“属性”。调用将失败，因为远程过程调用尚未完全功能。此功能很快将在 Samba 中完成。
