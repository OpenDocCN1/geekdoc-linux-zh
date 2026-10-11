

## lchains 中匹配的数据包选项

| 选项 | 结果 |
|---|---|
| ACCEPT | 允许数据包通过至其目标位置。 |
| DENY | 拒绝数据包通过；不通知发送方被拒绝的事实。 |
| MASQ | 将出站数据包转换，使其看起来像是来自防火墙；将入站数据包转换，使其指向正确的机器。仅适用于转发链或自定义链，不适用于输入链或输出链。 |
| REDIRECT | 将数据包重路由到本地 IP 地址和端口。仅适用于输入链或自定义链。 |
| REJECT | 拒绝数据包通过，并发送一个 ICMP 数据包，让发送方知道数据被拒绝。 |
| RETURN | 跳转到下一个链以检查其规则；或者默认执行该链的策略动作。 |

## 代理防火墙

代理防火墙隐藏了其背后网络的结构。所有从内部机器发往外部世界的流量，看起来都像是来自代理本身。这意味着，用户想要访问的任何服务，都必须在终端用户机器上有一个客户端，并在防火墙上有一个代理服务器来发送请求并传递结果。

在撰写本书时，我考虑了两种在 Linux 下免费提供的代理防火墙：

- SOCKS——可在 www.socks.nec.com 获取
- 防火墙工具包（FWTK）——可在 www.tis.com/research/software 获取

FWTK 是“即时解决方案”部分末尾“设置代理防火墙”中所涵盖的防火墙。另一种流行的选择是 Gauntlet Firewall，可在 www.pgp.com/asp_set/products/tns/gauntlet.asp 获取。

在设置 FWTK 时，你需要处理的主要配置文件之一是 `/usr/local/etc/netperm-table`。它包含一系列单行对，遵循以下通用格式：

`application: rule value`

你可以用以下两种格式之一来指定多个应用程序。若要明确列出应用程序，请使用这种格式：

`application1, application2, ...:`

若要指定所有应用程序均符合条件，请使用以下格式：

`*`

同一个应用程序可以出现在多条规则中，因此你不必觉得必须把所有内容都塞在一起。如果存在多条针对相同结果类型的规则，则代理程序将使用它遇到的第一条规则。请确保定期检查该文件，特别是在你向其中添加更多内容时，以确保你没有意外让某些项目忽略了它们自己的规则。

## 独立防火墙

防火墙并不总是以在可能也充当路由器及其他设备的盒子上安装软件的形式出现。有几种专门化的防火墙实际上并不与任何生产机器共享设备。其中一些防火墙是你购买时已预装好，然后直接插入你的网络或受保护区域与外部世界之间的“黑盒子”。另一些则是单独安装在盒子上的程序。

该领域的几种可能解决方案如下：

- Phoenix 自适应防火墙——可在 [www.progressive-systems.com/products/](https://www.progressive-systems.com/products/) 获取
- Sinus 防火墙——可在 [www.sinusfirewall.org](https://www.sinusfirewall.org) 获取
- FirePlug EDGE 项目——可在 [http://edge.fireplug.net](http://edge.fireplug.net) 获取

## 即时解决方案

### 激活和停用影子套件

影子套件有两个主要组件：密码和组。虽然在 Red Hat 安装中，影子密码通常默认是激活的，但如果你已将其停用，可以使用命令 `pwconv` 来启用它们。若要移除它们，请使用命令 `pwunconv`。

影子组通常默认未激活。要启用它们，请使用命令 `grpconv`。要移除组影子功能，请使用 `grpunconv`。

### 关闭不必要的守护进程和后台进程

要阻止不必要的守护进程和其他进程在 Red Hat Linux 中自动启动，请执行以下操作：

1. 以 root 身份登录。
2. 输入 `ps aux | more` 以显示所有正在运行的进程列表，防止列表开头从屏幕顶部滚动出去。
3. 查看这些进程。其中一些是你需要的，另一些则是基于“你可能需要它们”的假设而启动的。
   - 提示：*如果你无法确定是否需要某个特定项目，请利用 man 系统。输入 "man 进程名" 以了解其功能。*
4. 输入 `cd /etc/rc.d` 切换到包含所有运行级别启动目录的父目录。Red Hat 的运行级别布局如表 9.9 所示。
5. 输入 `ls rc#.d`，其中 # 代表你想要编辑其启动信息的运行级别。
6. 输入 `ls S*` 并按下 Enter。你在这里看到的所有内容都是进入此运行级别时启动的守护进程。每个 S 后面的数字对应该守护进程的启动时间。数字越小，启动得越早。

| 运行级别 | 描述 |
|---|---|
| 0 | 关闭系统 |
| 1 | 单用户模式 |
| 2 | 多用户模式但不具备 NFS 功能 |
| 3 | 完整多用户模式；启动到命令行的标准运行级别 |
| 5 | 具备 GUI 的完整多用户模式；启动到 GUI 的标准运行级别 |
| 6 | 重启机器 |

7. 如果你担心在此时犯错误，请输入 `ls -la S > /root/rulisting`。此命令将详细的文件列表保存到文件 /root/rulisting 中，以便在必要时你可以恢复到之前的状态。
8. 删除对应于你不想使用的服务的文件。此目录中的项不是真正的守护进程。它们全都是指向真正守护进程的软链接。因此，只要你备份了文件列表，你稍后可以在必要时恢复这些项目。
9. 现在你已经移除了不需要的守护进程，你可以开始移除其他在启动时运行的程序。如果整理思路有帮助，请输入 `shutdown -r now` 立即重启机器，并在系统恢复后再次查看正在运行的进程。
10. 在 Red Hat Linux 中，输入 `vi /etc/rc.d/rc.local` 以打开最可能包含在启动时运行的非守护进程程序的文件。默认情况下，此文件包含以下内容：

```
#!/bin/sh
#
# This script will be executed *after* all the other init scripts.
# You can put your own initialization stuff in here if you don't
# want to do the full Sys V style init stuff.

if [ -f /etc/redhat-release ]; then
    R=$(cat /etc/redhat-release)

    arch=$(uname -m)
    a="a"
    case "_-$arch" in
        _a*) a="an";;
        _i*) a="an";;
    esac

    NUMPROC=`grep -c \`'acpu\[0-9\]+' /proc/stat`
    if [ "$NUMPROC" -gt "1" ]; then
    SMP="$NUMPROC-processor "
    if [ "$NUMPROC" = "8" -o "$NUMPROC" = "11" ]; then
    a="an"
    else
    a="a"
    fi
    fi

    # This will overwrite /etc/issue at every boot. So, make any
    # changes
    # you want to make to /etc/issue here or you will lose them when
    # you reboot.
    echo "" > /etc/issue
    echo "$R" >> /etc/issue
    echo "Kernel $(uname -r) on $a $SMP$(uname -m)" >> /etc/issue

    cp -f /etc/issue /etc/issue.net
    echo >> /etc/issue
fi
```

11. 在此 shell 脚本的默认版本中（有关 shell 脚本的更多内容，请参见第 20 章），不会启动任何新程序。请浏览文件，查看你或任何安装例程是否添加了内容。如果有，请在行首加上井号（#）将其注释掉。
12. 按下 Esc 键，然后输入 "ZZ" 以保存并退出文件。新的更改将在启动时显示。
13. 在方便的时候重启系统，以确保它能顺利启动。

> **注意：** 每个 Linux 发行版对启动信息的处理方式略有不同，尤其是运行级别和系统初始化文件。如果你使用的是其他发行版，可能需要遵循不同的步骤。要确定某个发行版的运行级别，请输入 `more /etc/inittab`。运行级别键应位于文件开头附近。

**相关解决方案：**

| | 见第...页： |
|---|---|
| 关闭和重启 | 97 |
| 编写你自己的软件包更新脚本 | 611 |
| 编写你自己的用户创建脚本 | 615 |

