
PPP dynamic channel allocation code copyright 1995 Calder, Inc.

PPP line discipline registered.

# 第 18 章：Linux 中的拨号上网

如果你在内核中没有看到 PPP 支持的证据，你应该按照第 2 章的步骤重新编译内核。然后，你应该确保在 `make config` 步骤中启用 PPP 支持。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_594_0.png)

## 收集 PPP 连接信息

许多 ISP（互联网服务供应商）通过其维护的一个或多个系统提供 PPP 接入。如果你注册了此类服务，ISP 应为你提供建立到远程系统 PPP 连接所需的信息。至少，这些信息应包含以下内容：

- 你连接端的 IP 地址。（此 IP 地址将与你 PC 的 PPP 接口——串口关联。）
- ISP PPP 接口的 IP 地址。（此地址可能列为“网关”地址，因为该接口是你系统访问互联网的网关。）
- 连接到远程系统的拨号号码。
- 登录远程系统时使用的用户名和密码。

大多数 ISP 还提供域名服务器、邮件服务器和新闻服务器的 IP 地址。然而，这些地址对于建立 PPP 连接的机制并不重要。

## 使用 pppd 和 chat 创建 PPP 连接

要在两个系统之间建立 PPP 网络连接，你必须在两端都运行 PPP 软件。通常情况下，你的 ISP 会为你提供一个设置好的账户，以便 PPP 软件运行。在尝试任何操作之前，你的 Linux 内核必须包含 PPP 网络设备。

要在两个系统之间建立 PPP 网络连接，你必须在两端都运行 PPP 软件。通常情况下，你的 ISP 会为你提供一个设置好的账户，以便 PPP 软件运行。在拨号连接到远程系统后，会自动启动 PPP 程序。

以下是设置 PPP 连接的两个基本步骤：

- 1. 拨号连接到远程系统。
- 2. 启动 PPP 程序。

正如 `dip` 程序帮助你自动化 SLIP 设置一样，你使用另外两个程序——`pppd` 和 `chat`——来设置和配置 PPP 连接。在尝试任何操作之前，你的 Linux 内核必须包含 PPP 网络设备。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_593_0.png)

## 第四部分：PPP 的乐趣

PPP 是一个比 SLIP 更复杂、功能更丰富的协议，但使用 PPP 连接到远程网络的机制与你为 SLIP 使用的步骤非常相似。你仍然会为 PPP 连接的两个端获取 IP 地址、一个需要拨打的电话号码以及一个用于登录远程系统的用户名。

正如 `dip` 程序帮助你自动化 SLIP 设置一样，你使用另外两个程序——`pppd` 和 `chat`——来设置和配置 PPP 连接。在尝试任何操作之前，你的 Linux 内核必须包含 PPP 网络设备。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_594_0.png)

## 检查 PPP 支持

与 SLIP 一样，你必须配置内核以支持 PPP。在重新编译 Linux 内核的 `make config` 步骤中（详情请参考第 2 章），你应该对 PPP 支持的问题回答 Yes：

PPP (point-to-point) support (`CONFIG_PPP`) [M/n/y] y

你可以使用命令 `/proc/net/dev` 来验证系统上是否有 PPP 设备。通常情况下，你应该能在输出中看到 `ppp0` 设备。

此外，当系统启动时，请查看启动消息以确认 PPP 设备是否已配置。使用 `dmesg | more` 命令查看启动消息。你应该会在启动消息中看到类似下面的行：

IP Protocols: IGMP, ICMP, UDP, TCP

TCP version 2.2.0 (dynamic channel allocation)

TCP compression code copyright 1989 Regents of the University of California

PPP dynamic channel allocation code copyright 1995 Calder, Inc.

PPP line discipline registered.

## 收集 PPP 连接信息

许多 ISP（互联网服务供应商）通过其维护的一个或多个系统提供 PPP 接入。如果你注册了此类服务，ISP 应为你提供建立到远程系统 PPP 连接所需的信息。至少，这些信息应包含以下内容：

- 你连接端的 IP 地址。（此 IP 地址将与你 PC 的 PPP 接口——串口关联。）
- ISP PPP 接口的 IP 地址。（此地址可能列为“网关”地址，因为该接口是你系统访问互联网的网关。）
- 连接到远程系统的拨号号码。
- 登录远程系统时使用的用户名和密码。

大多数 ISP 还提供域名服务器、邮件服务器和新闻服务器的 IP 地址。然而，这些地址对于建立 PPP 连接的机制并不重要。

## 使用 pppd 和 chat 创建 PPP 连接

要在两个系统之间建立 PPP 网络连接，你必须在两端都运行 PPP 软件。通常情况下，你的 ISP 会为你提供一个设置好的账户，以便 PPP 软件运行。在拨号连接到远程系统后，会自动启动 PPP 程序。

以下是设置 PPP 连接的两个基本步骤：

- 1. 拨号连接到远程系统。
- 2. 启动 PPP 程序。

正如 `dip` 程序帮助你自动化 SLIP 设置一样，你使用另外两个程序——`pppd` 和 `chat`——来设置和配置 PPP 连接。在尝试任何操作之前，你的 Linux 内核必须包含 PPP 网络设备。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_593_0.png)

## 终止 SLIP 连接

要终止 SLIP 连接，你必须使用 `dip` 程序本身并带有 `-k` 选项，随后是用于 SLIP 连接的串口设备。以 root 身份登录，并输入以下命令关闭 `dev/cua0` 上的 SLIP 连接：

```
dip k cua0
DIP: Dialup IP Protocol Driver version 3.3.7-uri (8 Feb 96)
Written by Fred N. van Kempen, MicroWalt Corporation.
```

DIP: process 951 killed.

## 连接到远程网络

作为 PPP 客户端

PPP 是一个比 SLIP 更复杂、功能更丰富的协议，但使用 PPP 连接到远程网络的机制与你为 SLIP 使用的步骤非常相似。你仍然会为 PPP 连接的两个端获取 IP 地址、一个需要拨打的电话号码以及一个用于登录远程系统的用户名。

正如 `dip` 程序帮助你自动化 SLIP 设置一样，你使用另外两个程序——`pppd` 和 `chat`——来设置和配置 PPP 连接。在尝试任何操作之前，你的 Linux 内核必须包含 PPP 网络设备。

![](img/a5afb9ccf4a412511e9fcfa4280141e3_594_0.png)

## 检查 PPP 支持

与 SLIP 一样，你必须配置内核以支持 PPP。在重新编译 Linux 内核的 `make config` 步骤中（详情请参考第 2 章），你应该对 PPP 支持的问题回答 Yes：

PPP (point-to-point) support (`CONFIG_PPP`) [M/n/y] y

你可以使用命令 `/proc/net/dev` 来验证系统上是否有 PPP 设备。通常情况下，你应该能在输出中看到 `ppp0` 设备。

此外，当系统启动时，请查看启动消息以确认 PPP 设备是否已配置。使用 `dmesg | more` 命令查看启动消息。你应该会在启动消息中看到类似下面的行：

IP Protocols: IGMP, ICMP, UDP, TCP

TCP version 2.2.0 (dynamic channel allocation)

TCP compression code copyright 1989 Regents of the University of California

PPP dynamic channel allocation code copyright 1995 Calder, Inc.

PPP line discipline registered.

## 收集 PPP 连接信息

许多 ISP（互联网服务供应商）通过其维护的一个或多个系统提供 PPP 接入。如果你注册了此类服务，ISP 应为你提供建立到远程系统 PPP 连接所需的信息。至少，这些信息应包含以下内容：

- 你连接端的 IP 地址。（此 IP 地址将与你 PC 的 PPP 接口——串口关联。）
- ISP PPP 接口的 IP 地址。（此地址可能列为“网关”地址，因为该接口是你系统访问互联网的网关。）
- 连接到远程系统的拨号号码。
- 登录远程系统时使用的用户名和密码。
