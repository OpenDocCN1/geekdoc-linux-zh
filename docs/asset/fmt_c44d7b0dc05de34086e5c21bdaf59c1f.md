
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```
[/content]

Wait that's example. Need actual processing.

Let's do proper.

[content]
`192.168.1.0/24`网络上的主机应将其默认路由设置为`192.168.1.15`，`192.168.2.0/24`网络上的主机应将其默认路由设置为`192.168.2.1`。最重要的是，不要忘记将添加路由和启用`ip_forward`部分作为启动脚本的一部分。

> 提示：脑子里没有 DNS 服务器了？如需对外部可靠的 DNS 服务器进行快速查询，请尝试`4.2.2.1`,`4.2.2.2`,`4.2.2.3`,`4.2.2.4`,`4.2.2.5`,`4.2.2.6`,`8.8.8.8`或`8.8.4.4`。这些地址已经存在很长时间，由一组易记忆的数字组成。

# VPC、子网、IP 和路由配置

（AWS 云示例）

作为一个示例，我们将介绍如何设置网络拓扑结构，以便在第三方云环境中启动并托管 Fedora Linux 服务器。请注意，除了在本节中选择的工具和操作系统环境外，这里没有任何本质上特定的 Linux 内容。你会感到如在家一样，因为这里使用的命令非常有 Linux 风格或类似于 FOSS 风格。你可以按照完全相同的步骤启动其他非 FOSS（非 Linux）系统。

> 注意：你可能感兴趣的是，大多数云提供商系统都会间接地与某种基于 Linux 的服务器进行交互；服务器负责完成大部分工作，如处理请求、托管虚拟机、执行路由、托管应用程序等。

假设你有一个授权的 AWS 账户，并已正确设置了所有前提条件（AWS 账户、计费、访问密钥、密钥密钥等）。使用 AWS 作为示例云，在接下来的章节中我们将创建一个 VPC、创建一个子网、将子网设置为公共、创建防火墙规则，最后启动实例。

> 注意：云提供商使用长随机字符串组成的特殊标识符来唯一标识（标记）云中的众多资源。Amazon 将这些称为资源 ID。为了避免混淆，我们在示例输出中特意掩盖了实际的 VPC 值，例如将`vpc-0321z38`改为`vpc-*`。

# VPC 和子网 (AWS)

VPC 是包含并提供访问云资源的总体容器。要创建一个跨越`10.0.0.0/16` CIDR块的 VPC，请输入：

```bash
# aws ec2 create-vpc --cidr-block 10.0.0.0/16
```

```
{
  "Vpc": {
    "VpcId": "vpc-*",
    <OUTPUT TRUNCATED>
  }
}
```

注意输出中的 VPC ID (`VpcId`)。在新创建的 VPC 下创建一个`10.0.0.0/24` CIDR块的子网，如下：

```bash
# aws ec2 create-subnet --vpc-id vpc-* --cidr-block 10.0.0.0/24
```

# Internet 网关和路由 (AWS)

Internet 网关 (`IG`) 用于不同网络之间的通信。我们将 VPC 中的唯一子网设置为公共。这可以通过将 IG 附加到 VPC、创建路由表并配置子网与 IG 之间的路由来实现，让 VPC 中的资源能够访问互联网。

让我们创建一个 Internet 网关：

```bash
# aws ec2 create-internet-gateway
```

```
{
  "InternetGateway": {
    "InternetGatewayId": "igw-*",
    <OUTPUT TRUNCATED>
  }
}
```

注意输出中的 Internet 网关值 (`InternetGatewayId`)。将 Internet 网关 (`igw-*`) 附加到 VPC：

```bash
# aws ec2 attach-internet-gateway --vpc-id vpc-* --internet-gateway-id igw-*
```

为 VPC 定义自定义路由表，输入：

```bash
# aws ec2 create-route-table --vpc-id vpc-*
```

```
{
  "RouteTable": {
    "RouteTableId": "rtb-*",
    <OUTPUT TRUNCATED>
  }
}
```

注意输出中的路由表值 (`RouteTableId`)。接下来在新创建的路由表中创建路由。这将是默认路由 (`0.0.0.0/0`)，我们将将其指向 Internet 网关，如下：

```bash
# aws ec2 create-route --route-table-id rtb-* --destination-cidr-block 0.0.0/0 --gateway-id igw-*
```

让我们通过路由表查看我们刚刚查询的路由：

```bash
# aws ec2 describe-route-tables --route-table-id rtb-*
```

```
{
  "RouteTables": [
    "Associations": [],
    "RouteTableId": "rtb-*",
    "VpcId": "vpc-**",
    "Routes": [
      {
        "GatewayId": "igw-**",
        "DestinationCidrBlock": "0.0.0.0/0",
        "State": "active",
        "Origin": "CreateRoute"
      }
    ]
  ]
}
```

自定义路由表看起来是正确的。然而，为了将流量从此子网引导到 Internet 网关，我们需要将路由表与该子网关联。查询 VPC 中定义的子网：

```bash
# aws ec2 describe-subnets --filters "Name=vpc-id,Values=vpc-**"
--query 'Subnets[*].{ID:SubnetId,CIDR:CidrBlock}'
```

```
{
  "CIDR": "10.0.0.0/24",
  "ID": "subnet-**"
}
```

注意输出中的子网 ID (`ID`)。为了使其成为公共子网，让我们子网与我们的自定义路由表绑定：

```bash
# aws ec2 associate-route-table --subnet-id subnet-* --route-table-id rtb-*
```

# 安全组 (AWS)

安全组充当虚拟防火墙，控制进出云实例的流量。分配给实例的安全组在启动实例时定义。因此，你需要在你的虚拟防火墙上“打几个洞”，以便从公共互联网访问资源或服务。

# 第 13 章 网络配置

由于我们希望能够连接到云 Linux 服务器，我们将首先在 VPC 中定义一个新的安全组，允许从任何地方进行 SSH 访问：

```bash
# aws ec2 create-security-group --group-name SSH --description "Security group for SSH" --vpc-id vpc-*
```

```
{
  "GroupId": "sg-*"
}
```

注意安全组组值 (`GroupId`)。为新创建的安全组创建 TCP/IP 规则：

```bash
# aws ec2 authorize-security-group-ingress --group-id sg-* --protocol tcp --port 22 --cidr 0.0.0.0/0
```

# 在自己的子网中启动 Linux 服务器 (AWS)

我们终于完成了演示环境的基础网络设置。假设你已经创建并拥有现有的密钥对 `THE_KEY_NAME`，你应该能够在你的 AWS 账户下配置一个新的虚拟机。

在我们刚刚创建的公共子网中启动一个新的虚拟机镜像：

```bash
# aws ec2 run-instances --image-id ami-0520e698dd50bd1d --count 1 --instance-type t2.micro --key-name <THE_KEY_NAME> --security-group-ids sg-* --subnet-*
```

注意输出中新启动的实例。要查看新实例的信息，输入：

```bash
# aws ec2 describe-instances --instance-id i-*
```
