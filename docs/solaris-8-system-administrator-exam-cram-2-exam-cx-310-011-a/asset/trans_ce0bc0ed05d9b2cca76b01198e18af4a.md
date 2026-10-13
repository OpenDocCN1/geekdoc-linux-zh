

## 练习题

### 问题 1

以下哪条命令用于设置安装服务器？

- a. `setup_install_server`
- b. `setup_install_server -b`
- c. `install_server setup`
- d. `server_setup -i`

答案 a 正确。`setup_install_server` 命令用于设置安装服务器。`-b` 命令行参数用于安装引导服务器。因此，答案 b 不正确。答案 c 和 d 中的命令不存在。

### 问题 2

以下哪项是在与安装服务器分离的系统上设置引导服务器的原因？

- a. 引导服务器不能驻留在安装服务器上。
- b. 一个或多个安装客户端与安装服务器不在同一子网上。
- c. 并非所有安装客户端都在同一子网上。
- d. NIS 或 NIS+ 无法定位驻留在安装服务器上的引导服务器。

答案 b 正确。如果一个或多个安装客户端与安装服务器不在同一子网上，则应在与安装服务器分离的系统上设置引导服务器。引导服务器可以驻留在安装服务器上。因此，答案 a 不正确。客户端相对于其他客户端的位置不决定是否需要引导服务器；客户端相对于安装服务器的位置决定是否需要单独的引导服务器。因此，答案 c 不正确。NIS 和 NIS+ 不定位任何内容；它们仅用作信息数据库。因此，答案 d 不正确。

### 问题 3

输入用于将安装客户端信息添加到安装服务器或引导服务器的命令名称（不带命令行参数）。

正确答案是 `add_install_client`。

### 问题 4

以下哪些安装方法可以使用网络安装资源？（选择所有适用项。）

- [ ] a. 自定义 JumpStart
- [ ] b. Web Start
- [ ] c. JumpStart
- [ ] d. 交互式安装

答案 a、b、c 和 d 均正确。所有四种安装方法都可以使用网络安装资源。

### 问题 5

以下哪些是自动安装方法？（选择所有适用项。）

- [ ] a. SunInstall
- [ ] b. 自定义 JumpStart
- [ ] c. Web Start
- [ ] d. JumpStart

答案 b 和 d 正确。自定义 JumpStart 和 JumpStart 是自动安装方法。SunInstall 和 Web Start 是交互式安装方法。因此，答案 a 和 c 不正确。

### 问题 6

输入用于将 Solaris 8 软件（第 2 张，共 2 张）CD 或 Solaris 8 语言分发 CD 的内容添加到安装服务器的命令名称。

正确答案是 `add_to_install`。

### 问题 7

以下哪些文件应位于 JumpStart 配置目录中？（选择所有适用项。）

- [ ] a. 一个或多个 JumpStart 配置文件
- [ ] b. `check`
- [ ] c. `rules` 文件
- [ ] d. `rules.ok` 文件

答案 a、c 和 d 正确。配置文件和 rules 文件是必须在 JumpStart 配置目录中创建的两种文件。如果它们设置正确，则会在 JumpStart 配置目录中创建 rules.ok 文件。必须执行位于 Solaris 8 分发 CD 上的 check 命令来验证 rules 和配置文件。因此，答案 b 不正确。

### 问题 8

将每个 `add_install_client` 命令行参数与其用途匹配。

| 参数 | 用途 |
| --- | --- |
| a. `-c` | 1. 指定安装服务器和路径 |
| b. `-d` | 2. 指定配置服务器和 JumpStart 配置目录路径 |
| c. `-p` | 3. 指定客户端为 DHCP 客户端 |
| d. `-s` | 4. 指定 sysidcfg 文件的服务器和路径 |

答案 a-2、b-3、c-4 和 d-1 正确。`-c server:path` 命令行参数指定配置服务器以及 rules 和 profile（类）文件所在的 JumpStart 配置目录。`-d` 命令行参数指定客户端将使用 DHCP 来确定 IP 地址、网络掩码等。`-p server:path` 命令行参数指定服务器和 sysidcfg 文件的完整路径名。`-s server:path` 命令行参数指定安装服务器和安装映像的路径。

### 问题 9

输入自定义 JumpStart 安装用于定义系统安装方式的文件。

正确答案是 profile。

### 问题 10

以下哪些是 Solaris 8 软件组？（选择所有适用项。）

- [ ] a. 完整发行版
- [ ] b. 基本
- [ ] c. 最终用户支持
- [ ] d. Java 开发环境

答案 a 和 c 正确。完整发行版和最终用户支持是 Solaris 8 软件组。答案 b 和 d 中的组不存在。

### 问题 11

输入包含引导参数并由 `add_install_client` 命令更新的文件名。

正确答案是 `/etc/bootparams`。

## 需要了解更多信息？

![](img/b957f979417d9f16274c2eb52c8f2c9f_464_0.png)

Becker, George, Mary E. S. Morris 和 Kathy Slattery，*Solaris Implementation*（Prentice Hall, Englewood Cliffs, NJ, 1995），ISBN 0-13-353350-6。

![](img/b957f979417d9f16274c2eb52c8f2c9f_464_1.png)

Sun Microsystems，*Solaris 高级安装指南*。提供印刷版（部件编号 806-0957-10），可通过 **http://docs.sun.com** 获取，也可从 Solaris 8 操作系统随附的在线文档 AnswerBook2 中获取。

![](img/b957f979417d9f16274c2eb52c8f2c9f_464_2.png)

Sun Microsystems，*系统参考手册，第 1 节——用户命令*。提供印刷版（部件编号 806-0624-10），可通过 **http://docs.sun.com** 获取，也可从 Solaris 8 操作系统随附的在线文档 AnswerBook2 中获取。

![](img/b957f979417d9f16274c2eb52c8f2c9f_464_3.png)

Sun Microsystems，*系统参考手册，第 1M 节——管理命令*。提供印刷版（部件编号 806-0625-10），可通过 **http://docs.sun.com** 获取，也可从 Solaris 8 操作系统随附的在线文档 AnswerBook2 中获取。

![](img/b957f979417d9f16274c2eb52c8f2c9f_464_4.png)

Sun Microsystems，*系统参考手册，第 4 节——文件格式*。提供印刷版（部件编号 806-0633-10），可通过 **http://docs.sun.com** 获取，也可从 Solaris 8 操作系统随附的在线文档 AnswerBook2 中获取。

## 模拟测试 II

![](img/b957f979417d9f16274c2eb52c8f2c9f_465_0.png)

本章提供 61 道与考试 CX-310-012（“Solaris 8 操作环境认证 Solaris 管理员考试，第二部分”）相关的题目。本次考试必须在 90 分钟内完成。

请记住，要通过认证，您必须同时通过 CX-310-011 考试和本次考试。CX-310-011 考试的模拟测试见第 11 章。应试技巧也可参阅该章。

## 模拟测试

### 问题 1

输入用于将 Solaris 8 软件（第 2 张，共 2 张）分发 CD 的内容添加到安装服务器的命令名称。

### 问题 2

DiskSuite 支持以下哪些虚拟设备或 RAID 级别？（选择所有适用项。）

- [ ] a. 串联虚拟设备
- [ ] b. RAID 级别 0
- [ ] c. RAID 级别 1
- [ ] d. RAID 级别 5
- [ ] e. RAID 级别 10

### 问题 3

以下哪条命令用于设置系统以通过网络进行安装？

- ( ) a. `setup_network_client`
- ( ) b. `network_install`
- ( ) c. `add_install_client`
- ( ) d. `install_network_client`

### 问题 4

在尝试解析主机名时，以下哪个 /etc/nsswitch.conf 文件条目会导致依次搜索 DNS、NIS+，然后是 /etc 文件？

- ( ) a. `hosts: dns nisplus files`
- ( ) b. `hosts: files nisplus dns`
- ( ) c. `ipaddress: files nisplus dns`
- ( ) d. `ipaddress: dns nisplus files`

