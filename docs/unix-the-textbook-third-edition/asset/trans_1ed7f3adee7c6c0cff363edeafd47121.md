

*正在关闭（Shutting down）和已关闭（Down）：* 这些是在区域（zone）被停止过程中可见的过渡状态。但是，如果区域因任何原因无法完全关闭，它将停留在其中一个状态。

## 25.3.2 影响区域状态的命令

下表列出了 Solaris 中影响前一小节所述区域状态的相关命令及子命令。您还可以查看系统上的 zonecfg 和 zoneadm 手册页，以了解更多描述和解释。手册页中包含多个示例。zoneadm 命令的一般语法如下：

```
语法（SYNTAX）
zoneadm -z 区域名称 [-u uuid匹配] 子命令 [子命令选项]
zoneadm [-R 根目录] -z 区域名称 [-u uuid匹配] list [列表选项]
zoneadm [-R 根目录] -z 区域名称 [-u uuid匹配] mark incomplete
```

用途：zoneadm 实用程序用于管理系统区域。区域是一种由操作系统维护的应用程序容器。

常用选项/功能：
- zoneadm list -cv 列出区域并显示详细信息（verbose）。
- zoneadm -z firstzone install 使用 ZFS 安装名为 firstzone 的区域。

通过 zonecfg 更改的参数不会影响正在运行的区域。必须重新启动该区域才能使更改生效。

## 25.3.3 创建 Solaris 区域

### 示例 25.4：第一个区域

目标：使用 zonecfg 和 zoneadm 命令创建一个 Solaris 区域，并使用 ping 命令检查其与主机的连接。

简介：区域是一个“容器”，它运行与主机相同的内核，但在与主机完全隔离的、自主且安全的独立环境中运行。图 25.1 展示了区域在任意时刻可能处于的允许状态，表 25.1 列出了影响这些状态的命令。示例中的许多步骤将使区域经历这些状态。当您逐步执行示例时，建议回看该图，以确认您正在创建的区域在任一步骤中所处的当前状态。

前提条件：
- 1. 您必须拥有 Solaris 系统的超级用户权限。
- 2. 您的计算机必须连接到互联网，并且您必须能够访问 Oracle IPS 软件包仓库。

## 表 25.1 zonecfg 和 zoneadm 子命令及参数

| 命令、参数和子命令 | 简要说明 |
|---|---|
| **已配置（Configured）** | |
| zonecfg -z 区域名称 verify | |
| zonecfg -z 区域名称 set 旧值=新值 | 将旧区域名称重命名为新名称。 |
| zonecfg -z 区域名称 commit | |
| zonecfg -z 区域名称 delete | |
| zoneadm -z 区域名称 attach | |
| zoneadm -z 区域名称 verify | |
| zoneadm -z 区域名称 install | |
| zoneadm -z 区域名称 clone | |
| zoneadm -z 区域名称 mark incomplete | |
| zoneadm -z 区域名称 mark unavailable | |
| **不完整（Incomplete）** | |
| zoneadm -z 区域名称 uninstall | |
| **不可用（Unavailable）** | |
| zoneadm -z 区域名称 uninstall | 从指定系统卸载该区域。 |
| zoneadm -z 区域名称 attach | |
| zonecfg -z 区域名称 | 可用于更改 zonepath 以及在已安装状态下可更改的任何其他属性或资源。 |
| **已安装（Installed）** | |
| zoneadm -z 区域名称 ready（可选） | |
| zoneadm -z 区域名称 boot | |
| zoneadm -z 区域名称 uninstall | 从系统中卸载指定区域的配置。 |
| zoneadm -z 区域名称 move 路径 | |
| zoneadm -z 区域名称 detach | |
| zonecfg -z 区域名称 | 添加或移除 attr、bootargs、capped-cpu、capped-memory、dataset、dedicated-cpu、device、fs、ip-type、limitpriv、net、rctl 或 scheduling-class 属性。 |
| zoneadm -z 区域名称 mark incomplete | |
| zoneadm -z 区域名称 mark unavailable | |
| **就绪（Ready）** | |
| zoneadm -z 区域名称 boot | |
| zoneadm halt | 将处于就绪状态的区域返回到已安装状态。 |
| zonecfg -z 区域名称 | 添加或移除 attr、bootargs、capped-cpu、capped-memory、dataset、dedicated-cpu、device、fs、ip-type、limitpriv、net、rctl 或 scheduling-class 属性。 |
| **运行中（Running）** | |
| zlogin 选项 区域名称 | |
| zoneadm -z 区域名称 reboot | |
| zoneadm -z 区域名称 halt | 将处于就绪状态的区域返回到已安装状态。 |

