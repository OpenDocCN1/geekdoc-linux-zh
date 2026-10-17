
18. 在 `Firefox` 中输入 `localhost` 测试你的 Web 页面。
19. 退出浏览器，关闭终端。

## 本章总结

- `Apache` Web 服务器是可以下载的软件。
- `Apache` 安装后需要少量配置。
- 你可以使用命令检查 `Apache` 的状态。
- `HTTP-Server` 是用于配置 `Apache` 的应用程序。
- 手动配置 `Apache` 包括修改指令。
- 通过虚拟主机你可以在一台物理机器上运行多个域名。
- `Apache` 支持两种类型的虚拟主机：基于名称的虚拟主机和基于 `IP` 的虚拟主机。

## 复习问题

- `Apache` 可以配置，包括 `DocumentRoot`、`Directory` 和 `ServerName`。`DocumentRoot` 指定提供文件的目录，`Directory` 包含适用于特定目录的指令组，`ServerName` 设置服务器名称。

## 关键术语

**默认主机** `Apache` 配置文件中第一个声明的虚拟主机。参见虚拟主机。

**指令** 嵌入在 `Apache` 配置文件中的，告诉 `Apache` 如何运行。

**`DocumentRoot` 指令** 指定 `Apache` 用于提供主机文本文件的目录路径。

**标记语言** 由指令标签组成，定义了文本的显示方式。

**基于名称的虚拟主机** 共享相同 `IP` 地址的多个站点。

**`NameHost` 指令** 指定用于基于名称的虚拟机的 `IP` 地址的指令。

**`Order`、`Allow` 和 `Deny` 指令** 定义哪些主机可以访问特定目录的 `Apache` 指令。

**端口** 连接硬件设备的接口，例如磁盘驱动器或打印机；在网络中，主机之间的数据连接。

**`ServerAdmin` 指令** 指定 `Apache` 管理员邮箱帐户的指令。

**`ServerAlias` 指令** 将多个名称关联到虚拟主机的指令。

**`ServerName` 指令** 定义服务器名称并告诉 `Apache` 虚拟主机要显示内容的指令。

**标签** 用于格式化 `HTML` 文本的指令。它们成对出现，以表示用这些指令格式化文本的开始和结束。

**统一资源定位符 (`URL`)** 互联网上资源的地址。

**虚拟主机** 一种允许在物理机器上运行多个域名的 `Apache` 功能。

## 第 10 章 `Apache` Web 服务器

3. 使用哪个 `YaST` 应用来安装 `Apache`？
   a. `HTTP` 服务器
   b. 软件仓库
   c. 软件管理
   d. 网络服务

4. 哪种软件模式安装 `Apache` 以及其他相关模块？
   a. 文件和 Web 服务器
   b. 杂项服务器
   c. 邮件和新闻服务器
   d. Web 和 `LAMP` 服务器

5. 使用哪个命令安全地重启 `Apache` Web 服务器？
   a. `rcapache2 reload`
   b. `rcapache2 reboot`
   c. `rcapache2 start`
   d. a 和 b 都是

6. 使用哪个命令检查 `Apache` Web 服务器的状态？
   a. `rcapache2 help`
   b. `rcapache2 status`
   c. `rcapache2 reload`
   d. `rcapache2 probe`

7. 你可以使用哪个 `YaST` 应用来配置 `Apache` Web 服务器？
   a. `HTTP` 服务器
   b. 软件仓库
   c. 软件管理
   d. 网络服务

8. 在使用 `HTTP` 服务器 应用配置 `Apache` Web 服务器后，必须使用 `rcapache2` 命令重启服务器。对或错？

9. 在物理机上运行多个域名是不可能的。对或错？

10. 哪个指令定义了 `Apache` 用于提供文件服务的目录路径？
    a. `ServerName`
    b. `DocumentRoot`
    c. `Alias`
    d. `NameVirtualHost`

11. 哪个指令指定了基于名称的虚拟主机 `IP` 地址？
    a. `ServerName`
    b. `DocumentRoot`
    c. `Alias`
    d. `NameVirtualHost`

12. 哪个指令定义了用户可以访问 Web 页面的 `URL`？
    a. `ServerName`
    b. `DocumentRoot`
    c. `Alias`
    d. `NameVirtualHost`

13. `httpd.conf` `Apache` Web 服务器配置文件包含以下哪些指令？（选择所有适用）
    a. `DocumentRoot`
    b. `Alias`
    c. `Hosts`
    d. `Include`

14. 哪一个 `Apache` 配置文件是适用于所有虚拟机的全局配置文件？
    a. `default-server.conf`
    b. `listen.conf`
    c. `httpd.conf`
    d. `vhosts.d`

15. 你使用哪个 `Apache` 配置文件将 `Apache` Web 服务器与特定的 `IP` 地址和端口关联？
    a. `default-server.conf`
    b. `listen.conf`
    c. `httpd.conf`
    d. `vhosts.d`

16. 使用什么命令来验证配置文件没有语法错误？

17. 解释基于名称的虚拟主机和基于 `IP` 的虚拟主机之间的区别。

18. `HTML` 是什么种类型的语言？
    a. 脚本
    b. 标记
    c. 解释型
    d. 编译型

![](img/b8a4c65ba2acb99909d8842055c0bdd7_248_0.png)

19. 下列是 `HTML` 文件中常见的标签？（选择所有适用）
    a. `<HTML>`
    b. `<BODY>`
    c. `<HEAD>`
    d. `<URL>`

20. 定义文本在 Web 浏览器中显示方式的指令是什么？
    a. 标签
    b. `XML`
    c. `HTML`
    d. 超文本

## 案例项目

### 案例项目 10-1：创建 `Apache` Web 服务器别名

`Joey Grizzle` 是一个负责公司网络和 `Apache` Web 服务器的 `IT` 主管。公司总部位于佐治亚州的托科阿（`Toccoa`）。在查看帮助台的日志文件和报告后，他发现一些员工无法访问 Web 服务器，因为他们输入的 `URL`。这是一个本地局域网站点，网络上唯一解析的服务器名称是 `Toccoasales`。`Joey` 与负责 `DNS` 服务器的 `IT` 技术人员交谈，让她创建一个条目，允许将名称 `www.tocoales.com` 解析为 `Apache` Web 服务器的 `IP` 地址。他随后询问是否可以确保 `www.tocoales.com` 和 `Toccoasales` 使用相同的 Web 页面。写一份简要报告说明如何配置。

### 案例项目 10-2：创建虚拟主机

你是一个分配到公司网络的帮助台技术人员。你早早上班并决定查看所有工单，看看是否可以快速关闭任务。你发现来自主管 `Ivan Smith` 的工单，请求一个可以托管 Web 站点的服务器。另一位帮助台技术人员在工单上写道：“等待购买新服务器”。你知道公司站点托管在 `Apache` Web 服务器上。解释 `Ivan Smith` 如何在不购买新服务器的情况下获取 Web 站点。

![](img/b8a4c65ba2acb99909d8842055c0bdd7_249_0.png)

# 第 11 章 域名系统

阅读本章并完成练习后，你将能够：

- 描述域名系统及其与互联网的关系
- 安装并配置 `Berkeley Name Daemon (BIND)`
- 通过命令行检查 `DNS` 服务器的状态
- 识别区域并描述区域文件中的元素

在本章中，你将学习如何将 `openSUSE Linux` 变为 `DNS` 服务器。首先，你看到网络如何将主机解析为 `IP` 地址。引入了域名系统。你还学习了 `DNS` 基本概念，如名称服务器、转发器、缓存以及顶级域名。接下来，你使用 `YaST` 模块安装并配置 `DNS` 软件。你还看到如何使用命令行检查 `DNS` 服务器的状态。

## 域名系统简介

过去，互联网上的计算机依赖于地址簿。这些文本文件存储了所有主机的名称和 `IP` 地址。当互联网上添加新计算机时，必须更新主机文件。因此，创建了名称服务器。名称服务器是翻译 `IP` 地址（或名称）的中央数据库。这种方法对于本地网络是有效的，但在处理资源时出现了新问题。例如，如果互联网上的每台计算机都拥有信息（也称为资源记录），你可以想象筛选这些记录以找到你寻找的资源有多困难。管理也变成了一个问题。为了管理互联网，知道哪个实体负责什么非常重要。域名系统建立了。

## 互联网上的 `DNS`

互联网的域名系统（`DNS`）遵循更大规模的名称服务器概念。`DNS` 将 `IP` 地址与实际名称关联，这样可以通过易记忆的名称而不是数字字符串访问网络资源。在 `Linux` 中，名为 `Berkeley Name Daemon (BIND)` 的名称服务器执行此转换。`BIND` 是包含解析主机名到 `IP` 地址的协议的开源软件。`DNS` 的目标是去中心化管理，因此 `DNS` 是一个允许管理的去中心化数据库。本地 `DNS` 服务器可以处理请求，但会将主机名请求转发给转发器，转发器的工作是处理站点资源。例如，如果你第一次访问 `google.com`，`DNS` 服务器不知道 `google.com` 的 `IP` 地址，因此无法从该服务器请求 Web 页面。你的本地 `DNS` 服务器查询转发器，并在本地缓存（`google.com` 的 `IP` 地址）一段时间，这称为生存时间 (`TTL`)，稍后将在“`DNS` 区域”中讨论。`TTL` 各不相同，默认值为 86400 秒（即一天）。缓存是一种在本地站点存储 `DNS` 查询以进行主机到 `IP` 地址解析的功能。其理念是在经常访问特定站点时缓存 `IP` 位置以节省查询时间。

![](img/b8a4c65ba2acb99909d8842055c0bdd7_252_0.png)

互联网工程任务组 (`IETF`) 发布了关于 `DNS` 的 `RFC 1034`。可以在 `www.ietf.org/rfc/rfc1034.txt` 获取。

虽然本地管理员可以管理 `DNS` 服务器，但仍在使用由中央控制的根 `DNS` 服务器。根 `DNS` 服务器控制互联网的顶级域名 (`TLD`)。这种 `DNS` 部分的分布式权限使得巨大的 `DNS` 数据库成为可能。表 11-1 描述了一些最为人知的顶级域名。

## 表 11-1 常见顶级域名

| 顶级域名 | 描述 |
|---|---|
| `.com` | 商业组织，例如 `Google.com` 和 `Apple.com`。 |
| `.edu` | 教育机构，例如弗吉尼亚学院 (`vc.edu`) 或贝尔维大学 (`bellevue.edu`)。 |
| `.gov` | 政府机构，例如 `FBI` (`fbi.gov`) 或 `CIA` (`cia.gov`)。 |
| `.mil` | 军事组织，例如空军 (`af.mil`) 和陆军 (`army.mil`)。 |
| `.net` | 网络组织，例如互联网提供商（例如 `AT&T` 和 `at.net`）。没有政府机构控制此域的使用，因此你会在 `net` 域名下看到一个本应为 `.com` 的站点列表。 |
| `.org` | 非商业或非营利组织，例如加利福尼亚共和党 (`capog.org`) 或民主党 (`democrats.org`)。 |

![](img/b8a4c65ba2acb99909d8842055c0bdd7_252_1.png)

除了表 11-1 中的顶级域名外，国际组织 (`ISO`) 还定义了另一组顶级域名，由国家两位代码组成——例如美国的 `.us` 和法国的 `.fr`。

`DNS` 数据库（如图 11-1 所示）结构化为倒树（也称为命名空间），根位于树的顶部，顶级域名位于下方。树的节点被称为域名，并带有标签，例如用于政府的 `.gov`。虽然你可以管理或控制整个 `DNS` 数据库，但你拥有（管理）你自己的域名。个人或组织管理域名树中的每个节点。互联网名称与分配机构 (`ICANN`, `www.icann.org`) 控制树顶部的根域名。

## 域名结构

域名源自节点标签，层次结构中的每一层都由域名分隔。例如，某个学校主机计算机的域名可能是 `computer1.university.edu`。主机名是 `computer1`，它属于大学域名。大学域名是 `edu` 的子域名，而 `edu` 是一个顶级域名（`TLD`）。

![](img/b8a4c65ba2acb99909d8842055c0bdd7_253_0.png)

图 11-1 `DNS` 结构

© Cengage 2013

## 安装 `BIND`

安装 `BIND` 与安装 `Apache` Web 服务器类似。使用 `YaST` 管理安装 `DHCP` 和 `DNS Server` 模式，这会安装所有必要的 `DNS` 模块，例如 `BIND`、`BIND` 文档文件和 `DNS` 配置实用。

> `DHCP` 和 `DNS Server` 模式还安装了重要的动态主机配置协议 (`DHCP`) 模块，这些模块用于自动分配网络设置，而不是在每台机器上手动配置。

![](img/b8a4c65ba2acb99909d8842055c0bdd7_253_1.png)

`BIND` 文档文件位于 `/usr/share/doc/packages/bind/arm/` 目录下，包含八个章节。为 `DNS` 管理员文档提供了有关 `BIND 9` 版本的基本信息，该版本是 `openSUSE 11.2` 包含的。在活动 11-1 中，你将安装 `BIND` 并访问文档文件。

### 活动 11-1：安装 `BIND`

![](img/b8a4c65ba2acb99909d8842055c0bdd7_253_2.png)

所需时间：15 分钟
目标：安装 `BIND` 和其他 `DNS` 相关的包。

描述：在本次活动中，你使用 `YaST` 管理在 `DHCP` 和 `DNS Server` 模式中安装 `DNS` 包。安装 `BIND` 后，你使用 `Firefox` 显示 `BIND 9` 管理员参考手册。

1. 启动 `VMware Player` 并启动一个 `openSUSE` 虚拟机。
2. 打开终端窗口。通过输入 `su` 并按回车切换到 `root` 用户，然后输入正确的 `root` 密码。
3. 输入 `yast --gtk` 并按回车打开 `YaST` 控制中心。
4. 点击左侧“组”（`Groups`）下的“软件”（`Software`），然后点击“软件管理”（`Software Management`）。
5. 要显示按模式分类的所有可用包，点击筛选列表数组，然后点击“模式”（`Patterns`）。确保已选了“可用”（`Available`）选项。
6. 点击“功能”（`Functions`）下的 `DHCP` 和 `DNS Server`，点击“全部安装”（`Install All`）以安装 `BIND` 以及其他包，例如 `DNS` 服务器配置实用程序和 `BIND` 文档文件。最后点击“应用”（`Apply`）。
7. 安装完成后，关闭 `YaST` 控制中心。
8. 输入 `rpm -q bind` 并按回车查询 `RPM` 数据库中的 `BIND`。
9. 更改 `/usr/share/doc/packages/bind/arm` 目录，输入 `firefox By9ARM.html` 并按回车在 `Firefox` 中打开 `BIND 9` 管理员参考手册。阅读“引言”（`Introduction`）和“文档范围”（`Scope of Document`）部分以概述此手册的内容。
10. 关闭网络浏览器。保持 `root` 登录状态，让终端窗口打开并运行虚拟机，以便进行下一个活动。

## 配置 `BIND`

在 `openSUSE` 中，安装 `BIND` 后无需进一步配置。它作为一个名为 `named` 的守护进程运行（发音为 "name-dee"，而不是 "named"）。主 `BIND` 配置文件 `named.conf` 位于 `/etc` 目录。要启动 `named` 守护进程（`BIND`），使用 `named start` 命令。表 11-2 描述了确定守护进程状态的常用命令。

| 命令 | 说明 |
| --- | --- |
| `named start` | 启动 `named` 守护进程 |
| `named stop` | 停止 `named` 守护进程 |
| `named restart` | 重启 `named` 守护进程 |
| `named status` | 检查 `named` 守护进程的状态 |

你可以使用 `named.conf` 文件进行配置，使用如 `vim` 的编辑器，或者使用 `YaST` 模块，在安装 `BIND` 后即可可用。这需要 `root` 权限。当你启动该模块时，会看到图 11-2 所示的向导。

![](img/b8a4c65ba2acb99909d8842055c0bdd7_255_0.png)

图 11-2 `DNS` 服务器安装
源：域名系统

## 转发器

你可以在 `named.conf` 文件中配置转发器，将未解析的查询转发到站点 `DNS` 服务器并缓存结果。示例是 `named.conf` 文件中的内容：

```
// 此处应包含 named.conf 的示例代码，但原文在代码块结束后截断
```
