
每个 Aruba 控制器都配有一个八位八触点 (8P8C) 模块化控制台端口，允许管理员直接连接到控制器并运行 CLI 命令。在整个行业中，该插座和连接器被误称为 RJ-45 插座和 RJ-45 连接器。由于 Aruba 文档（以及大多数网络行业）使用 RJ-45 术语称为此端口和插座，为了保持并防止混淆，本书也将这样做。较新的控制器配备了一个微 USB 端口（微型 B），也设计用于控制台连接。当控制器尚未配置，或者网络问题阻止了通过 TCP/IP 访问控制器时，控制台连接尤为有用。

为了使用 RJ-45 控制台端口连接到控制器，你需要通常被称为“控制台线”（console cable）。控制台线的一端有一个 `DB-9` 母头串口连接器，用于连接到计算机的串口。另一端是一个 `RJ-45` 插头，用于连接到控制器的控制台端口。这种电缆可以使用多个组件组装，也可以是集成电缆。控制台线确实需要“回绕”（rollover）配置，连接到 `RJ-45` 连接器引脚 1 到 8 的线被回绕，且连接反转到引脚 8 到 1。

请不要将这种电缆称为 `crossover cable`。`crossover cable` 的布线方式通常是使电缆一端的发送线连接到电缆另一端的接收线。`crossover cable` 差异很大，具体取决于它们所使用的的通信技术和设备。

回绕线（rollover cable）是网络世界中非常常见的电缆，许多网络管理员会在电脑包里随身携带这些线。多年来我遇到的问题之一是，这些线缆通常很短，长度小于 6 英尺。这听起来可能长度足够了，但当你必须对数据机架中的设备进行维护时，6 英尺的线会极大限制你的活动，通常迫使你站着，一手拿着笔记本电脑，另一只手使用终端仿真软件为控制器编程。

大多数旧的 Aruba 控制器出货时带有一个 `DB-9` 到 `RJ-45` 适配器以及根网线。Aruba `DB-9` 到 `RJ-45` 适配器的布线方式在适配器内部提供了回绕功能。这意味着你可以使用任何直通网线连接适配器和控制器的控制台端口。如果你的脑子还没转过来，让我帮你解释一下：这意味着有了回绕适配器，可以使用任何直通网线来连接适配器和控制器的控制台端口。

## SSH 和 Telnet

在控制器完成基础配置并能够在 TCP/IP 上通信后，就不再需要物理连接到控制台端口。只需打开你喜欢的仿真器，选择 `SSH` 并连接到控制器的 IP 地址。默认情况下，`Telnet` 是禁用的且应该保持禁用，因为它不提供安全的通信。

## CLI 命令环境

我认为没有必要审查 CLI 环境的细节，因为它与你可能熟悉的许多交换或路由产品相似，而且 Aruba 已经在文档中对其进行了很好的解释。如果你不熟悉基础 CLI，*Aruba CLI Reference Guide* 中有一个名为“CLI Access”的章节，解释得很好。与其他网络产品一样，Aruba CLI 在你输入时会在终端中提供帮助。你可以通过问号 `?` 获取提示，并进行命令补全。

## 管道操作符

我想强调的一个命令功能是管道（pipe）功能。管道实际上是一个字符，即向上和向下的竖线（`|`）。这个命令可以添加到任何生成屏幕输出的命令末尾。与任何命令或参数一样，管道功能必须在前后都有空格，例如 `| |`。管道功能可以过滤或精炼显示的输出。管道功能可以使用四种方式来精炼输出：

- `command | include keyword`：只显示包含关键字的命令输出行。
- `command | exclude keyword`：只显示不包含关键字的命令输出行。
- `command | begin keyword`：显示包含关键字的第一行输出，以及此之后的所有行。
- `command | redirect-output`：不再将命令输出显示在屏幕上，而是将其写入控制器闪存分区中名为 `redirect-output.log` 的文件中。

为了说明这一点，以下是命令 `show ap database` 的输出。为了让后续示例中的屏幕输出更易读，我删除了三个必要的列：Flags、Switch IP 和 Standby IP。

```
#show ap database

| AP Database |

| :--- |

| 名称 | 组组 | AP 类型 | IP 地址 | 状态 |

| :--- | :--- | :--- | :--- | :--- |

| AP115-70-1 | controller70 | 115 | 10.1.90.150 | Up 1d:8h:23m:11s |

| AP135-80-1 | controller80 | 135 | 10.1.90.151 | Up 1d:8h:25m:39s |

| AP135-80-2 | controller80 | 135 | 10.1.90.153 | Up 1d:8h:25m:32s |

| AP225-90-1 | Roletest-group | 225 | 10.1.90.152 | Up 1d:8h:20m:30s |
```

标志位：U = 未配置 (Unprovisioned); N = 重名 (Duplicate name); G = 不存在该组 (No such group); L = 未授权 (Unlicensed)

I = 未激活 (Inactive); D = 配置无效或无配置 (Dirty or no config); E = 区域不匹配 (Regulatory Domain Mismatch)

X = 维护模式 (Maintenance Mode); P = PPPoE AP; B = 内置 AP (Built-in AP); s = LACP 链路聚合 (LACP striping)

R = 远程 AP (Remote AP); R- = 远程 AP 需要认证 (Remote AP requires Auth); C = 蜂窝 RAP;

c = 基于证书的 RAP (CERT-based RAP); 1 = 802.1x 认证 AP; 2 = 使用 IKE 第 2 版本

u = 自定义证书 RAP (Custom-Cert RAP); S = 备用模式 AP (Standby-mode AP); J = AP 处的 USB 证书

i = 室内 (Indoor); o = 户外 (Outdoor)

M = Mesh 节点; Y = Mesh 恢复 (Mesh Recovery)

总 AP 数量：4

如果你执行带有 `| include 135` 的 `show ap database` 命令，输出将仅显示包含字符串 135 的行，如下所示所示。请注意，在上一个示例中存在列头；但在本示例中，由于列头行不包含字符串 135，因此输出中不包含该列头。

```
#show ap database | include 135

AP135-80-1 controller80 135 10.1.90.151 Up 1d:8h:26m:48s

AP135-80-2 controller80 135 10.1.90.153 Up 1d:8h:26m:41s
```

如果你执行带有 `| begin 135` 的 `show ap database` 命令，输出将从第一个出现 135 的行开始显示，如下输出所示：

```
#show ap database | begin 135

AP135-80-1 controller80 135 10.1.90.151 Up 1d:8h:30m:8s

AP135-80-2 controller80 135 10.1.90.153 Up 1d:8h:30m:1s

AP225-90-1 Roletest-group 225 10.1.90.152 Up 1d:8h:24m:59s

标志位：U = 未配置 (Unprovisioned); N = 重名 (Duplicate name); G = 不存在该组 (No such group); L = 未授权 (Unlicensed)

I = 未激活 (Inactive); D = 配置无效或无配置 (Dirty or no config); E = 区域不匹配 (Regulatory Domain Mismatch)

X = 维护模式 (Maintenance Mode); P = PPPoE AP; B = 内置 AP (Built-in AP); s = LACP 链路聚合 (LACP striping)

R = 远程 AP (Remote AP); R- = 远程 AP 需要认证 (Remote AP requires Auth); C = 蜂窝 RAP;

c = 基于证书的 RAP (CERT-based RAP); 1 = 802.1x 认证 AP; 2 = 使用 IKE 第 2 版本

u = 自定义证书 RAP (Custom-Cert RAP); S = 备用模式 AP (Standby-mode AP); J = AP 处的 USB 证书 

i = 室内 (Indoor); o = 户外 (Outdoor)

M = Mesh 节点; Y = Mesh 恢复 (Mesh Recovery)

总 AP 数量：4
```

如果你执行带有 `| exclude 135` 的 `show ap database` 命令，输出将显示除包含文本 135 外的所有行，如下输出所示。
