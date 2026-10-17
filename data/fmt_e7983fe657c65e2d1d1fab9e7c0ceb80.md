
## 描述

`newhostkey`

输出（输出到文件名，可以使用 `-` 表示标准输出）一个适用于该主机的 RSA 私钥，格式类似于 `/etc/ipsec.secrets`（请参见 `ipsec.secrets(5)`），默认使用 `--quiet` 选项。

`--output` 选项是强制性的。如果指定的文件不存在，将根据 `umask 077` 创建它；如果文件已存在且非空，则向标准错误发送关于该点的警告信息，并将输出追加到文件中。

`--quiet` 选项会抑制 RSA 密钥的生成过程说明以及文件已存在的警告信息。

当带有 NSS 支持编译时（默认值），`--configdir` 指定 NSS 配置目录，证书密钥和 modsec 数据库均位于该目录。没有默认值，但 `/etc/ipsec.d` 可能是一个合理的选择。

当带有 NSS 支持编译时（默认值），`--password` 指定一个模块认证密码，如果启用了 FIPS 模式，可能需要该密码。

`--bits` 选项指定 RSA 密钥的位数；当前的默认值是 3072 到 4096 之间的随机值（16 的倍数）。允许的最小值为 2172。

`--random` 用于指定随机设备（默认使用 `/dev/random` 为加密库的 RNG 种子）。

`--hostname` 选项传递给 `rsasikey`，告诉它使用哪个主机名来标记输出（通过其 `--hostname` 选项）。

输出格式采用 `rsasikey` 格式，并添加括号以完成 `ipsec.secrets` 格式。在通常情况下，如果 `ipsec.secrets` 只包含主机自身的私钥，则 `newhostkey` 的输出就足够构成完整的 `ipsec.secrets` 文件。

## 文件

`/dev/random`, `/dev/urandom`

## 参见

`ipsec_rsasigkey(8)`, `ipsec.secrets(5)`

## 历史

最初为 Linux FreeS/WAN 项目 <http://www.freeswan.org/m> 由 Henry Spencer 编写。由 Paul Wouters 更新。

# 缺陷

与 `rsasigkey` 一样，其运行时间难以预测，因为系统随机数池的耗尽可能导致对随机位的任意长时间等待，而且质数搜索也可能消耗不可预测的（且可能是大量的）CPU 时间。请参见 `ipsec_rsasigkey(8)`。

如果有一个处理切换新密钥等性细节的高级工具将非常有帮助。

## 作者

Paul Wouters

用于抑制警告的占位符

# IPSEC_PF_KEY

`ipsec_pf_key` - 显示在使用 KLIPS 或 MAST 栈时内核发出的 pfkey 消息。

## 概要

`pf_key`—`ah`—`esp`—`ipip`—`ipcomp`—`daemon` `file` `hmac-md5-96` | `hmac-sha1-96`

## 栈

注意 `pf_key` 仅在 KLIPS 和 MAST 栈上支持。其他任何栈都不支持。

## 描述

`pf_key` 是一个打开 PF_KEY 套字并打印从中接收到的所有消息的程序。在不提供选项的情况下，它将注册自身以接收 AH、ESP、IPIP 和 IPCOMP 安全关联的密钥请求。如果给了更具体的选项，它将只监听列出的协议。

如果消息被识别，将对消息进行解码。

如果提供了 `--daemon` 选项，在完成注册后，程序将派生到后台运行。提供的文件将被打开，后台进程的进程 ID 将写入其中。此选项是为了是为了回归测试中呈现竞态条件。

## 文件

`/proc/net/pf_key`

## 参见

`pf_key(5)`, `ipsec(8)`, `ipsec_eroute(5)`, `ipsec_spi(5)`, `ipsec_spigrp(5)`, `ipsec_klipsdebug(5)`, `ipsec_tncfg(8)`, `ipsec_version(5)`

## 历史

为 Linux FreeS/WAN 项目 <http://www.freeswan.org/m[]> 由 Michael Richardson <mcr@freeswan.org> 编写。

## 作者

Paul Wouters

用于抑制警告的占位符

# IPSEC_PLUTO

`pluto` - ipsec IKE 守护进程和控制接口

## 概要

`ipsec pluto [help] [version] [--leak-all]`

## 描述

### pluto

`pluto` 是一个 IKE（“IPSec 密钥交换”）守护进程。`whack` 则是一个辅助程序，允许向运行中的 `pluto` 请求。

`pluto` 用于在具有 IPsec 的系统上自动构建共享关联。数据包的安全传输是系统其他部分——即内核的责任。`Pluto` 可以与各种内核实现交互，如 KLIPS、NETKEY 以及 KAME IPsec 栈。`ipsec_auto(8)` 为 `pluto` 和 `whack` 提供了一个更方便的接口。

### IKE 的工作

安全关联（SA）是两个网络节点之间如何处理流量的协议。这种处理涉及封装、认证、加密或压缩。

IKE 可以部署在网络节点上为该节点协商安全关联。IKE 实现只能与其他 IKE 实现进行协商，因此作为 IKE 协商安全关联的端点必须安装 IKE。

一个 IKE 实例（即特定网络节点上的 IKE 实现）使用 UDP IP 包与另一个 IKE 实例通信，因此节点之间必须存在路由。

安全关联（Security Association）拥有一组一致的特征，当双方都认可彼此的身份验证时，它们就可以建立安全关联。标准并没有规定是什么导致 IKE 实例启动协商。

总而言之，IKE 实例准备用于在 IPsec 环境中自动管理安全关联，但有许多问题被视为策略范畴，并留给系统管理员处理。

### Pluto

`pluto` 是 IKE 的一种实现。它作为守护进程运行在网络节点上。目前，这种网络节点模式是指运行着 KLIPS 或 NETKEY 实现的 IPsec 的 LINUX 系统，或者是运行 KAME 实现的 IPsec 的 FreeBSD/NetBSD/Mac OSX 系统。

`pluto` 实现了 IKE 的很大一个子集。这足以让它与其他 `pluto` 实例以及许多其他 IKE 实现协同工作。它目前支持 XAUTH、ModeConfig、X.509、死对端检测（Dead Peer Detection）、机会加密以及所有的 NAT 穿越（NAT Traversals）。

安全关联可接受特征的策略大部分硬编码在 `pluto` 的代码（`spdb.c`）中。最终，这将移动到一个具有响应式表达能力且更方便使用的的安全策略数据库中。

`pluto` 使用密钥或 RSA 签名来对与其协商的伙伴进行身份验证。这些 RSA 签名可以来自 DNS(SEC)、配置文件或 X.509 和 CA 证书。

当 `pluto` 被手动触发时，它会启动安全关联协商：通过运行 `whack` 程序来触发。当 KLIPS 捕获到用于机会加密的出站数据包时，它也会启动协商。

`pluto` 自身实现了 ISAKMP SA。在协商完 IPsec SA 的特征后，它会指导实现它。如有必要，它还会调用脚本来调整任何防火墙和 `route(8)` 命令以重定向 IP 包。

当 `pluto` 关闭时，它会关闭所有的安全关联。

### 在运行 Pluto 之前

`pluto` 以 root 用户身份作为守护进程运行。在运行它之前，必须设置好几项内容。

- `pluto` 需要一个良好的 IPsec 栈。
- `pluto` 支持多个公共网络（即被认为是不安全的且需要对其流量进行加密或身份验证的网络）。它通过查看所有已配置的接口来发现要使用的公共接口（可以使用 `--interface` 选项来限制考虑的接口）。这仅在 `whack` 告诉它 `--listen` 时发生，接口必须由它们配置。名称格式为 `ipsec[0-9]` 的接口被视为 KLIPS 虚拟公共接口。另一个具有 IP 地址的网络接口（将使用找到的第一个）被相应的真实公共接口。`--listen` 可用于限制在中心接口的一个 IP 地址上监听。`ifconfig(8)` 或带有 `-a` 标志的 `ip(8)` 将显示每个网络接口的名称和状态。
- `pluto` 需要预共享密钥和 RSA 私钥数据库。这在 `ipsec.secrets(5)` 中描述。通过 `whack` 命令告知 `pluto` RSA 公钥。如果连接是机会性的，且未知 RSA 公钥，`pluto` 将尝试使用域名命名系统（DNS）获取 RSA 密钥。

### 为 pluto 配置 KLIPS

`pluto` 支持的最基础网络拓扑是安全网关代表客户端子集进行协商。RGB 测试平台的图示是一个很好的例子（参见 `klips/doc/rgb_setup.txt`）。

该发行版根目录下的 `INSTALL` 文件解释了如何启动整个 KLIPS 系统。

确保安全网关之间有路由。这通常由默认路由覆盖，但可能需要发布 `route(8)` 命令。路由必须通过特定的 IP 接口（我们假设是 `eth0`，但不必如此）。连接安全网关到客户端的接口必须是不同的。

需要在每个网关上执行 `ipsec-tncfg(8)` 命令。所需的命令是：

```
ipsec tncfg --attach virtual ipsec0--physical eth0
```
