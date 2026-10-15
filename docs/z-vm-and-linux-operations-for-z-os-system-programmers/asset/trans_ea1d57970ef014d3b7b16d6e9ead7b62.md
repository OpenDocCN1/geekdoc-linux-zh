

> **注意：** 在命令中，请确保添加最后一个参数，label。
> 
> z/VM 系统不会在下一次 IPL 之前重新读取磁包标签，因此如果要显示这些磁包，将会显示旧标签。

- 3. 将更新后的 USER DIRECT 文件加载到系统目录空间。
  - `directxa user direct c`

- 4. 在加载新目录后，关闭系统并重新 IPL 系统。

## 关闭系统并重新 IPL

你必须为此步骤运行 HMC 控制台会话，如果你尚未从那里运行。

测试更改涉及关闭并重新启动系统。在这种情况下，你不得使用 SHUTDOWN REIPL，因为你随后必须使用 FORCE 来重新启动它。要关闭系统，请单独使用 SHUTDOWN 命令：

```
==> shutdown
SYSTEM SHUTDOWN STARTED
HCPSH9060I System shutdown may be delayed for up to 210 seconds
```

要将系统恢复运行：

- 1. 从 HMC，点击 CPC Recovery（或仅 Recovery）菜单中的 LOAD 图标。
- 2. 选择 Clear 单选按钮。所有其他参数应与之前的 IPL 相同。点击 OK。
- 3. 在 Load Task Confirmation 面板上点击 Yes。
- 4. 返回到 Integrated 3270 控制台。几分钟后，Standalone Program Loader 面板应打开。使用 TAB 键遍历到 IPL Parameters 部分并输入以下值：
  - `cons=sysg`
- 5. 按 F10 键继续 IPL 你的 z/VM 系统。这大约需要三分钟。
- 6. 在 Start 提示符处，指定 FORCE 启动，因为 spool 卷标签已更改：
  - `==> force drain`
- 7. 不要更改日时钟：
  - `==> no`

8. 当 IPL 完成时，从 OPERATOR 用户 ID 断开连接：
==> disc

9. 登录到 MAINT。

你现在应该能够启动一个 3270 仿真器会话，因为 TCP/IP 服务机器应该已启动。作为 MAINT 获取一个 3270 会话并使用 QUERY CPOWNED 命令验证卷标签是否已更改：

```
==> q cpowned
Slot Vol-ID Rdev Type Status
1 LX6RES 1A20 Own Online and attached
2 LX6PSL 1A21 Own Online and attached
3 LX6PAG 1A22 Own Online and attached
4 LX6W01 1A23 Own Online and attached
5 LX6W02 1A24 Own Online and attached
...
```

如果你 IPL 了一个具有重复系统卷的系统，你可能已经破坏了你的保存段。当你无法 IPL CMS 时，你就知道这种情况发生了，因此你必须 IPL 190。

> 重要：只有在你的保存段已被破坏时才执行此操作！要重建保存段，请尝试以下命令，作为 MAINT：
> ==> vmfsetup zvm cms
> ==> sampnss cms
> ==> i 190 c1 parm savesys cms
> ==> vmfbld ppf segbld esasegs segblist ( all

## 4.4 安装 Linux

本节描述如何配置你的 z/VM 系统以安装 Linux，引导用于安装的 Linux 内核，并登录到 Linux 系统。

### 4.4.1 为安装 Linux 配置你的 z/VM 系统

要在 z/VM 上运行 Linux 虚拟机，需要一个简单但高效的环境，你必须首先配置和自定义你的环境，以便在执行 Linux 内核时，DASD、网络和易于管理和安装的 Linux 客户机等资源都可用。

涉及的配置任务包括：

- 自定义 SYSTEM CONFIG 文件
  - 更改各种参数。
  - 创建虚拟交换机。
- 为 Linux 客户机设置 DASD
  - 格式化 DASD。
  - 为系统和用户使用配置 DASD。
- 创建 Linux 维护用户
  - 创建 minidisk。
  - 设置一个用于在客户机虚拟机中引导 Linux 的通用环境。

请回顾第 4.2.2 节“系统文件”第 126 页，我们在其中提到了 z/VM 的重要配置文件。你现在即将对其进行自定义。

## 自定义 SYSTEM CONFIG 文件

z/VM IPL 时读取的第一个配置文件是 SYSTEM CONFIG 文件。

建议进行以下更改：

- 增加检索键容量。
- 允许创建虚拟磁盘（VDISK）。
- 关闭 Disconnect Timeout。这将防止空闲断开连接的用户被强制退出系统。
- 定义一个将用于 Linux 网络的虚拟交换机（VSWITCH）。

为所有 Linux 客户机系统定义虚拟交换机是良好的做法，因为如果你计划以后增加数量，你可能没有足够的物理 OSA 网络卡供你创建的每个客户机虚拟机使用。虚拟交换机使用单个真实 OSA 设备并在多个虚拟客户机之间共享网络连接。

要自定义 SYSTEM CONFIG 文件：

- 1. 释放 CF1 磁盘。

要编辑 SYSTEM CONFIG 文件，MAINT 的 CF1 minidisk 必须通过 CPRELEASE 命令（或其缩写：CPREL）作为 CP 磁盘释放。CP 磁盘可通过 QUERY CPDISK 命令查询。请注意，由于 CF1 磁盘归 CP 所有，它正以只读模式由 MAINT 作为 CP 磁盘 A 访问。因此，为了以多读模式访问该 CF1 磁盘，我们首先请求 CP 释放它，然后以多读（mr）模式访问它：

```
==> q cpdisk
Label Userid Vdev Mode Stat Vol-ID Rdev Type StartLoc EndLoc
```

