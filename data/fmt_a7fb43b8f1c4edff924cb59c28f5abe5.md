
### 将文件合并到运行系统
最后一步是将所有文件合并到运行系统（`livesystem`）并在 Portage 后端注册这些文件。`ebuild` 的 "`qmerge`" 步骤涉及以下操作：

- 如果指定，执行 `pkg_preinst()` 函数
- 将所有文件复制到运行系统
- 在 Portage 后端注册文件
- 如果指定，执行 `pkg_postinst()` 函数

运行 `ebuild` 的 `qmerge` 功能来完成这些步骤：

#### 代码列表 8：在运行系统上合并 ebuild

```
# ebuild path/to/ebuild qmerge
```

### 清理临时目录
最后，你可以使用 `ebuild` 的 `clean` 功能清理临时目录：

#### 代码列表 9：清理临时目录

```
# ebuild path/to/ebuild clean
```

## 6.c. 额外的 Ebuild 功能
### 运行合并相关命令
使用 `ebuild` 的 `merge` 功能，你可以一次性运行 `fetch`、`unpack`、`compile` 和 `qmerge` 命令：

#### 代码列表 10：安装软件

```
# ebuild path/to/ebuild merge
```

### 执行配置操作
某些应用程序包含了进一步配置你的系统的指令。这些指令是交互式的，因此不会自动执行。要运行 `ebuild`（可选的）`config()` 函数中列出的这些步骤，请使用 `ebuild` 的 `config` 功能：

#### 代码列表 11：配置包

```
# ebuild path/to/ebuild config
```

### 构建包（或 RPM）
你可以指示 Portage 创建二进制包或 RPM 文件。使用 `ebuild` 的 `package` 或 `rpm` 功能来创建归档。这些功能之间存在一些差异：

- `package` 功能类似于 `merge` 功能，在创建包之前执行所有必要的步骤（`fetch`、`unpack`、`compile`）
- `rpm` 功能在运行 `install` 功能后构建 RPM 包

#### 代码列表 12：创建包

```
（对于二进制包）

# ebuild path/to/ebuild package

（对于 RPM 包）

# ebuild path/to/ebuild rpm
```

生成的 RPM 文件不包含依赖信息。

## 6.d. 更多信息
关于 Portage、`ebuild` 应用和 `ebuild` 文件的更多信息请参考以下帮助页：

#### 代码列表 13：帮助页

```
$ portage (Portage 本身)

$ emerge (emerge 命令)

$ ebuild (ebuild 命令)

man ebuild (ebuild 文件)
```

你还可以在《开发者手册》中找到开发相关信息。

## D. Gentoo 网络
### 1. 开始
#### 1.a. 开始
注意：本文假设你已经正确配置了内核、硬件模块以及接口名称。我们还假设你配置的是 `eth0`，但可能是 `eth1`、`wlan0` 等。

注意：本文需要更好的布局。要启动你的网卡，你需要告知 Gentoo RC 系统。这是通过在 `/etc/init.d` 中从 `net.lo` 到 `net.eth0` 创建符号链接实现的。

#### 代码列表 1：将 net.eth0 链接到 net.lo

```
# cd /etc/init.d

# ln -s
```

Gentoo 的 RC 系统现在知道了接口。它还需要知道如何配置新接口。所有的网络接口都在 `/etc/conf.d` 中配置。以下是 DHCP 和静态地址的示例。

#### 代码列表 2：etc/conf.d 示例

```
# 对于 DHCP

config_eth0=( "dhcp" )

# 使用 CIDR 法的静态 IP

config_eth0="192.168.0.7/24"

routes_eth0=( "default via 192.168.0.1" )
```

```
# 使用子网掩码法的静态 IP

config_eth0=("192.168.0.7 255.255.255.0")

routes_eth0=("default gw 192.168.0.1")
```

注意：如果你没有为接口指定配置，则假设为 DHCP。注意：CIDR 代表无类域间。IPv4 地址被分类为 A、B 或 C。早期的分类系统并没有阻止互联网的巨大力量，有一种地址方案允许一个 IP 地址表示许多 IP 地址。CIDR 地址看起来像普通的 IP 地址，结尾是一个斜杠加上一个数字；192.168.0.0/16。CIDR 在 RFC 1519 中描述。

现在我们已经配置了接口，可以使用以下命令启动和停止：

```
# /etc/init.d/net.eth0 start

# /etc/init.d/net.eth0 stop
```

重要：在排除网络故障时，建议在 `/etc/conf.d/rc` 中设置 `RC_VERBOSE="yes"` 以获取更多信息。

现在你已经成功启动并停止了接口，可能希望它在 Gentoo 启动时自动运行。做法如下，“`rc`”命令指示 Gentoo 启动运行级别（runlevel）中尚未启动的脚本：

```
# rc-update add net.eth0 default

# rc
```

## 2. 高级配置
### 2.a. 高级配置
`config_eth0` 变量是接口的核心。它是配置接口（在本例中为 `eth0`）的高级指令。列表中的命令都会执行。如果至少有一个有效，则认为接口是正常的。

以下是内置指令列表：

| 命令 | 描述 |
| --- | --- |
| null | 如果操作接口已启动且有地址，则成功终止配置 |
| IPv4 或 IPv6 地址 | 将地址添加到接口。dhcp、adsl 或 ip6（后者是来自第三方模块的自定义命令） | 运行提供该命令的模块。例如，dhcp 将运行一个提供 DHCP 的模块，可以是 `dhcp`、`udhc`、`client` 或 `prompt` 之一 |

如果命令失败，你可以指定一个回退命令。回退命令必须与配置结构完全匹配。

你可以将这些命令链起来。这里是一些真实的示例：

```
# 添加三个 IPv4 地址

config_eth0={

  "192.168.0.2/24"

  "192.168.0.3/24"

  "192.168.0.4/24"

}

# 添加一个 IPv4 地址和两个 IPv6 地址

config_eth0={

  "192.168.0.5/32"

  "4321:0:1:2:3:4:567:89ab"

  "4321:0:1:2:3:4:567:89ac"

}
```

保留我们内核分配的地址，除非接口掉线，否则通过 DHCP 分配另一个。如果 DHCP 失败，我们将添加一个由 APIPA 确定的静态地址
```
config_eth0={

  "nop"

  "dhcp"

}

fallback_eth0={

  "null"

  "apipa"

}
```

> 注意：使用 `ifconfig` 模块并添加多个地址时，会为每个额外的地址创建接口别名。因此，通过上述两个示例，你将获得 `eth0`、`eth1` 和 `eth2`。你无法对这些接口进行任何特殊操作，因为内核和其他程序会将 `eth0` 和 `eth1` 视为 `eth2`。

> 重要：回退顺序非常重要！如果我们没有指定 `null`，那么只有在 `noop` 命令失败时，`apipa` 命令才会运行。

注意：APIPA 和 DHCP 将在稍后进行讨论。

### 2.b. 网络依赖
`/etc/init.d` 中的初始化脚本可以依赖于特定的接口，或者在 `/etc/conf.d/rc` 中定义的 `net` 也可以具有不同的含义，这取决于 `RC_NET_STRICT_CHECKING` 变量。

#### 值描述

- `net` 服务至少有一个服务 `bednet` 必须处于启动状态。这可以用于带有 WIFI 的笔记本用户，他们只想在给定时间开启一个网络，以便 `net` 服务被视为已启动。
- 此没有选项，但 `net.eth0` 也已连接。这对于不关心特定接口是否启动状态的人很有用。
- 所有网络接口必须处于启动状态，`net` 服务才能被考虑。

但是 `net.br0` 依赖于 `net.eth0` 和 `net.eth1` 呢？`net.eth1` 是一个无线或 PPP 设备，在添加到网桥之前需要进行配置。这不能在 `/etc/init.d/net.br0` 中完成，因为它是它的符号链接。

答案是在你的 `/etc/conf.d/net` 中编写 `depend()` 函数。

```
代码行 2: /etc/conf/net 中的 net.br0 依赖
```

```
# 你可以使用当前脚本中找到的任何依赖关系（use, after, before）

depend_br0()

need net.eth0 net.eth1
```
