
你还可以使用图形化的 Red Hat 服务配置向导（Red Hat Service Configuration Druid）。以下指令将向你展示如何使用向导启动或停止您的防火墙。

1. 点击 Gnome 主菜单按钮并选择“程序：系统：服务配置”。
2. 如果没有以 root 身份登录，会弹出输入窗口并要求你输入 root 密码。

输入你在 Red Hat 安装过程中设置的 root 密码。

出现服务配置窗口，如图 8-2 所示。此窗口控制所有的 Linux 守护进程（提供服务的进程）。
3. 向下滚动服务配置窗口，直到找到 `iptables` 服务。点击复选框使其出现勾选标记，如图 8-3 所示。
4. 点击窗口左上角的重启（Restart）按钮。

你可以点击启动（Start）按钮，但我们建议你使用重启功能。启动和重启按钮的效果相同，但如果服务已经在运行，重启功能将会起作用。如果服务已经在运行，使用启动功能将不起作用。

点击停止（Stop）按钮关闭您的防火墙。

在服务重启后，你会看到一条类似图 8-4 所示的确认消息。
5. 点击确定。

你的防火墙已重启，你可以退出服务配置窗口。

你还可以防止 `iptables` 脚本在系统启动时自动启动。点击服务名称正左侧的框以取消勾选标记。点击保存（Save）按钮，指向启动脚本（`/etc/init.d/iptables`）的符号链接（`/etc/rc.d/rc5/S0iptables`）将被移除。你可以通过点击框让勾选标记重新出现来恢复该链接。

## 显示您的防火墙规则

在配置防火墙后，你自然会想要验证过滤规则是否设置正确。要显示防火墙规则，请按照以下步骤操作：

1. 点击 GNOME 面板上的终端图标打开终端窗口。
2. 面板是屏幕底部巨大的菜单栏。终端图标看起来像一个显示器。
3. 如果你不是 root 用户，在终端窗口的命令提示符处输入 `su -` 并按回车变为 root。
4. 输入 root 密码。
5. 输入以下命令显示防火墙规则：

`iptables -L`

## 第 8 章：火，，火，嘿，嘿，防火墙真酷 123

![](img/5275bfa3908ad63320aaea42eefe467c_146_0.png)

8-2：服务配置窗口。

![](img/5275bfa3908ad63320aaea42eefe467c_146_1.png)

8-3：找到 `iptables` 服务。

## 124 第二部分：联网了吗？

## 第 8 章：火，，火，嘿，嘿，防火墙真酷

你应该会在终端窗口中看到如下列表：

```
Chain input (policy DENY):
target      prot opt source      destination ports
ACCEPT      all   anywhere      n/a
ACCEPT      all   anywhere      n/a
ACCEPT      tcp ly-       anywhere      -> -
            any                                    
ACCEPT      UDP        anywhere      domain -
Chain forward (policy DENY):
Chain output (policy DENY):
target      prot opt source      destination ports
ACCEPT      all   anywhere      n/a
ACCEPT      all   anywhere      n/a
ACCEPT      tcp       anywhere      -> -
            any                                    
ACCEPT      UDP        anywhere      any ->
            domain
```

第一个链（简单来说是一组用于共同目的或功能的规则）是用于入站 IP 数据包的。你可以看到默认策略是拒绝所有 IP 数据包。前两个规则告诉 `iptables` 允许逻辑环回（`lo`）和以太网（`eth0`）接口上的所有内部数据包。下一条规则允许来自传出连接的返回包进入。最后一条规则允许入站的 UDP 域名包，这些数据包用于域名服务（DNS）。

下一个链（简单来说是一组用于共同目的或功能的规则）是用于入站 IP 数据包的。你可以看到默认策略是拒绝所有 IP 数据包。前两个规则告诉 `iptables` 允许逻辑环回（`lo`）和以太网（`eth0`）接口上的所有内部数据包。下一条规则允许来自传出连接的返回包进入。最后一条规则允许入站的 UDP 域名包。

第三个链（简单来说是一组用于共同目的或功能的规则）是用于入站 IP 数据包的。你可以看到默认策略是拒绝所有 IP 数据包。前两个规则告诉 `iptables` 允许逻辑环回（`lo`）和以太网（`eth0`）接口上的所有内部数据包。下一条规则允许来自传出连接的返回包进入。最后一条规则允许入站的 UDP 域名包。

第四个链（简单来说是一组用于共同目的或功能的规则）是用于入站 IP 数据包的。你可以看到默认策略是拒绝所有 IP 数据包。前两个规则告诉 `iptables` 允许逻辑环回（`lo`）和以太网（`eth0`）接口上的所有内部数据包。下一条规则允许来自传出连接的返回包进入。最后一条规则允许入站的 UDP 域名包。

第五个链（简单来说是一组用于共同目的或功能的规则）是用于入站 IP 数据包的。你可以看到默认策略是拒绝所有 IP 数据包。前两个规则告诉 `iptables` 允许逻辑环回（`lo`）和以太网（`eth0`）接口上的所有内部数据包。下一条规则允许来自传出连接的返回包进入。最后一条规则允许入站的 UDP 域名包。

第六个链（简单来说是一组用于共同目的或功能的规则）是用于入站 IP 数据包的。

![](img/5275bfa3908ad63320aaea42eefe467c_146_0) 测试您的防火墙

在配置防火墙后，你自然会想要验证过滤规则是否设置正确。要显示防火墙规则，请按照以下步骤操作：

1. 点击 GNOME 面板上的终端图标打开终端窗口。
2. 面板是屏幕底部巨大的菜单栏。终端图标看起来像一个显示器。
3. 如果你不是 root 用户，在终端窗口的命令提示符处输入 `su -` 并按回车变为 root。
4. 输入 root 密码。
5. 输入以下命令显示防火墙规则：

你应该会在终端窗口中看到如下列表：

```
Chain input (policy DENY):
target      prot opt source      destination ports
ACCEPT      all   anywhere      n/a
ACCEPT      all   anywhere      n/a
ACCEPT      tcp ly-       anywhere      -> -
            any                                    
ACCEPT      UDP        anywhere      domain -
Chain forward (policy DENY):
Chain output (policy DENY):
target      prot opt source      destination ports
ACCEPT      all   anywhere      n/a
ACCEPT      all   anywhere      n/a
ACCEPT      tcp       anywhere      -> -
            any                                    
ACCEPT      UDP        anywhere      any ->
            domain
```

第一个链（简单来说是一组用于共同目的或功能的规则）是用于入站 IP 数据包的。你可以看到默认策略是拒绝所有 IP 数据包。前两个规则告诉 `iptables` 允许逻辑环回（`lo`）和以太网（`eth0`）接口上的所有内部数据包。下一条规则允许来自传出连接的返回包进入。最后一条规则允许入站的 UDP 域名包，这些数据包用于域名服务（DNS）。

下一个链（简单来说是一组用于共同目的或功能的规则）是用于入站 IP 数据包的。你可以看到默认策略是拒绝所有 IP 数据包。前两个规则告诉 `iptables` 允许逻辑环回（`lo`）和以太网（`eth0`）接口上的所有内部数据包。下一条规则允许来自传出连接的返回包进入。

第三个链（简单来说是一组用于共同目的或功能的规则）是用于入站 IP 数据包的。

# 第 9 章

## 使用 Mozilla 浏览网页和管理电子邮件

### 本章

- 介绍 Mozilla
- 根据你的喜好调整 Mozilla
- 浏览网页
- 接收和阅读电子邮件
