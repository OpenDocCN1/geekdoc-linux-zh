
### 3.5.2 Linuxconf 启动

![](img/4e6a76e57a4105be55d8a1cc0750b023_83_0.png)

图 78. Linuxconf 启动

第一次运行`Linuxconf`时，你会看到一个欢迎窗口，其中提供了使用`Linuxconf`的提示。

点击``Quit``进入`Linuxconf`界面。

### 3.5.3 我可以用 Linuxconf 做什么？

`Linuxconf`最大的优势在于其控制下极其丰富的配置选项范围。以下是选项的简要但并非完全的列表：

- 网络选项：
  - 基础主机信息：设置主机名和域名。你可以设置多个网络接口，分配`IP`地址并指定驱动程序。
  - `DNS`使用：设置默认域、多个名称服务器和搜索域。
- 路由和网关：设置默认网关和通往其他网络的路由。
- 设置`NIS`、`N`、`DHCP`服务器、`Apache`Web服务器、`SMB`、`FTP`、`IP`接口和`PPP`选项。
- 用户账户管理（图 79）：

![](img/4e6a76e57a4105be55d8a1cc0750b023_84_0.png)

图 79. 用户账户选项

你可以进行基础和一些高级管理，包括添加、删除或修改用户账户。你可以设置密码管理、计划任务定义、配置邮件设置并定义组定义。

- 文件系统：

  你可以控制挂载点、交换文件、分区、`NFS`卷、配额以及某些文件权限。
- 其他服务：

  你可以指定初始系统服务和调制解器端口。
- 启动模式：

  基础`LILO`配置，包括启动新内核的选项以及设置你的启动级别（3代表文本模式，5代表图形模式）。
- 控制选项（图 80）：

| test1: Linuconf 119 (subrev 2) | | | |
| Config | Control | Status |
| --- | --- | --- |
| Control panel | List of configuration files | 这是由 linuconf 管理的所有文件列表。对于每个文件，你可以直接访问描述它的帮助。文件名名前缀的字母表示其如何由 Linuconf 管理。更多信息请见 |
| - Activation | | |
| - Shutdown/reboot | | |
| - Control activity | | |
| Mount/Unmount file systems | | |
| - Configure scheduled tasks | | |
| - Archive configurations | | |
| - Switch system | | |
| - Control and files | | |
| - Activate configuration files | | |
| - Configure all commands and daemons | | |
| - Configure permissions and ownership | | |
| - Configure Linuconf modules | | |
| - Configure system profiles | | |
| - Override Linuconf options | | |
| - Create Linuconf additions | | |
| Features | | |
| Path | Status | Subways |
| /etc/X11/F8MC | A OP base | | |
| /etc/X11/F8MC | A OP base | | |
| /etc/F86Config | A OP base | | |
| /etc/ace-in.map | A OP fluent | | |
| /etc/linuconf | MO | | |
| /etc/contracts | MO OP nfserver | | |
| /etc/exports | M | | |
| /etc/fstab-local | A MV hardware | | |
| Quit | AdpcChanges | Help |

图 80. 控制选项

`Control`允许你激活当前的`Linuconf`配置、关闭、重启、控制已安装的基础服务、卸载文件系统、调度超级用户任务以及许多配置选项。

### 3.5.4 启用服务自启动

启用服务在启动时启动是一个常用程序。在这个示例中，我们安装了`Samba`并希望服务自动启动。为了实现这一点，我们将使用`Linuconf`实用程序。

`Linuxconf`的`X-Windows`版本；但所有版本的`Linuxconf`本质上都是相同的。要从`X-Windows`终端启动`Linuxconf`，输入：

```
linuxconf
```

![](img/4e6a76e57a4105be55d8a1cc0750b023_86_0.png)

图 81. 启动实用程序（见图 81）。在服务窗口中，我们安装的服务是可见的。在本示例中使用`Samba`。向下滚动并选择`samba`服务。

点击``Startup Automatic``框。我们还有启动、停止或重启服务的选项。

点击``Accept``按钮。当`Linux`重启时，`Samba`服务将自动启动。

## 3.6 总结

我们结束了基础服务管理。关于运行`Linux`的更多信息，请查看`Linux`文档网站：

或阅读`Matt Welsh`出版的《Running Linux》。

## 第 4 章 SuSE Linux 基础系统管理

本章将为你提供如何在`SuSE`系统上执行常见管理任务的概述。大多数这些任务可以通过`YaST`，`SuSE`的管理工具完成。然而，你仍然可以手动编辑不同的配置文件。`YaST`会检测这些更改并不会覆盖它们。

### 4.1 使用 YaST 添加和删除软件包

`SuSE Linux`使用`RPM`包管理器管理发行版的软件包。`RPM`使用数据库存储属于特定软件包的文件信息，以及有关软件包的附加信息。`RPM`本身是一个命令行程序。你可以从命令行使用它添加、删除或获取软件包和系统文件的信息。更多详情请参见第 85 页的使用`RPM`进行包管理。`YaST`的管理和配置工具可以作为`RPM`的用户友好界面。

要安装或删除软件包，请插入`CD-ROM`并以`root`用户身份在命令行输入``yast``启动`SuSE`的安装和配置工具。`YaST`将启动，你会看到`YaST`的菜单。

| YaST - Yet another Setup Tool | |
| YaST 版本 1.07 -- (c) 1994-2000 SuSE GmbH |
| 语言: English |
| 媒体: CD-ROM ATAPI EIDE /dev/sdc [OK] |
| 根设备: /dev/sda6 |
| 安装的通用帮助 |
| 安装的调整 |
| 选择/安装软件包 -> |
| 更新系统 -> |
| 系统管理 |
| 显示。安装介质的 README 文件。 |
| 版权 |
| 退出 YaST |

高亮菜单项``选择/安装软件包``并按回车。或者，你可以通过以下参数调用`YaST`：

```
yast --mask install --autoexit
```

这将自动打开安装主菜单，并在退出时返回命令行界面。

| 安装 | YaST 版本 1.07 -- (c) 1994-2000 SuSE GmbH |
|---|---|
| 日志文件: | 加载配置 |
| 保存配置 | |
| 修改/创建配置 | |
| 检查软件包依赖 | |
| 如果…… | |
| 开始安装 | |
| 所有系列和软件包索引 | |
| 软件包信息 | |
| 安装软件包 | |
| 删除软件包 | |
| 主菜单 | |

图 85. YaST：软件包主菜单

`SuSE Linux`提供了软件配置选择。这些包含一组选定的软件包，以满足特定的需求。选择“加载配置”来加载预定义的配置。

`80 IBM @server xSeries`和`Netfinity`的`Linux`系统管理与备份

### 安装 YaST 版本 1.07 -- (c) 1994-2000 SuSE GmbH

| | | | |
|---|---|---|---|
| [ ] SuSE 几乎所有 (Almost everything) | 1859 - 7.25 G |
| [ ] SuSE 开发系统 (Development system) | 452 - 1.98 G |
| [ ] SuSE D2 基础系统 (base system) | 93 - 202.7 M |
| [ ] SuSE 游戏 (Games) | 519 - 1.82 G |
| [ ] SuSE Gnome 系统 | 425 - 1.61 G |
| [ ] SuSE KDE 系统 | 683 - 1.61 G |
| [ ] SuSE 最小系统 (Minimum system) | 359 - 1.47 G |
| [ ] * SuSE 多媒体系统 (Multimedia system) | 87 - 158.7 M |
| [ ] SuSE 网络导向系统 (Network oriented system) | 464 - 1.6 G |

| F1=帮助 | | F2=描述 | | F9=软盘 |
|---|---|---|---|
| < 添加 | | 替换 | | 中止 |

![](img/4e6a76e57a4105be55d8a1cc0750b023_92_0.png)

现在您可以从当前配置中添加文件，也可以用这些配置之一来替换它。如果您替换了配置，所有不属于所选配置的已安装软件包将被标记为删除！按`Esc`返回主菜单。

要向您的当前配置中添加或删除软件包，请选择“修改/创建配置”。这将打开图 87 中的系列窗口。

### 系列选择 YaST 版本 1.07 -- (c) 1994-2000 SuSE GmbH

| 系列 | | |
|---|---|---|
| 文档 (Documentation) | [ 144.7 M ] |
| Emacs | [ 31.7 M ] |
| 模拟器 (Emulators) | [ 0 B ] |
| 游戏等 (Games and more) | [ 1.9 M ] |
| GNOME - GNU 对象模型环境 | [ 0 B ] |
| 所有图形 (All Graphics) | [ 59.9 M ] |
| 业余无线 (AX.25, CW, Logs, 等) | [ 0 B ] |
| KDE - K 桌面环境 (版本 2) | [ 0 B ] |
| K 桌面环境 | [ 76.8 M ] |
| KWP 应用 | [ 6.5 M ] |
| 网络支持 (TCP/IP, UUCP, 邮件, 新闻) | [ 355.3 M ] |

| 设备名称分区 | 总计 | 已用 | 空闲 | 空闲百分比 | 挂载点 |
|---|---|---|---|---|---|
| /dev/sda6 | Linux | 1.85 G | 1.12 G | 753.3 M | 39% | / |
| /dev/sda5 | Linux | 5.5 M | 325.0 K | 5.2 M | 94% | /boot |

| F1:帮助 | F4:排序 | F5:依赖 | F10=Esc-退出 |

所有软件包都被分为不同的系列。选择您的类别并按回车键查看属于该系列的所有软件包。

### 软件包选择 - 系列 n YaST 版本 1.07 -- (c) 1994-2000 SuSE GmbH

| | | | |
|---|---|---|---|
| [ ] acmnrp | Java 版 NNTP 代理 | <F3>=200 |
| [ ] amanda | 网络磁盘归档器 | 挂载点 |
| [ ] apache | Apache Web 服务器 | Free |
| [ ] archive | 我在哪里可以找到什么？ | 812.0 M |
| [ ] authd | Apache auth_ldap 模块 | /boot |
| [ ] autofs | 基于内核的自动挂载器 | 3.4 M |
| [ ] backend | Apache Web 服务器的负载均衡 | .../adm |
| [ ] bind | 命名服务器工具（旧版本） | 0 B |
| [ ] bind9 | BIND9（新版本） | | |
| [ ] bindutil | 用于查询和测试 DNS 的工具 | | |
| [ ] bing | 点对点带宽测量工具 | | |
| [ ] bitchx | 一个 IRC 客户端 | | |
| [ ] bookmail | Bukmail | | |

版本: 8.2.3
软件包大小：已安装 2.9 M（压缩后 998.0 K）
新的命名作者示例。支持工具`nslookup`、`dig`、`dnsquery`和`host`位于`bindutils`软件包中。关于设置命名服务器的文档可以在`/usr/share/doc/SuSE/packages/bind`找到。
