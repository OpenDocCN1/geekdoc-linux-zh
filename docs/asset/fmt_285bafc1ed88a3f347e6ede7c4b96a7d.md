
导航到 **Configuration** ⇒ **SECURITY** ⇒ **Authentication** ⇒ **Servers** ⇒ **Server Group** 将带你进入服务器组菜单，在其中可以使用 WebUI 界面添加角色条件。从服务器组菜单中选择一个组，然后在配置窗口的底部是 Server Rules 区域，在该区域点击 `New` 按钮添加规则。

如果你想查看已创建的所有服务器组列表，以下显示了 CLI 命令和相应的输出：

```
#show aaa server-group summary

Server Groups
| Name | Servers | Rules | hits | Out-of-service |
| :--- | :--- | :--- | :--- | :--- |
| default | 1 | 1 | 0 | |
| derivation1 | 2 | 1 | 0 | |
| failthrough-1 | 2 | 0 | 0 | |
| internal | 1 | 1 | 0 | |
| radius-group01 | 2 | 0 | 0 | |
| servergroup1-2 | 2 | 0 | 0 | |
| servergroup2-1 | 2 | 0 | 0 | |
```

显示服务器组列表后，你可以显示任何一个服务器组的详细信息，如下 CLI 输出所示：

```
#show aaa server-group derivation1

Fail Through: No
Load Balance: No

Auth Servers
| Name | Server-Type | trim-FQDN | Match-Type | Match-Op | Match-Str |
| :--- | :--- | :--- | :--- | :--- | :--- |
| radius01 | Radius | No | | | |
| radius02 | Radius | No | | | |

Role/VLAN derivation rules
| Priority | Attribute | Operation | Operand | Type | Action | Value | Validated |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | filter-id | value-of | String | set role | Yes | |
```

IETF 属性 `filter-id` 已使用多年，因为它是一个基于标准的属性，被不同厂商支持并并在它们之间提供互操作性。随着 BYOD 设备的普及，角色和 VLAN 的分配已成为 AAA 过程中不可或缺的组成。AAA 和认证服务器的进步（例如 ClearPass）增强了认证器与认证服务器之间交换的属性。包括 Aruba 在内的许多厂商都提供了 VSA（厂商特定属性），以提供更具定制且强大的 AAA 环境。

当你使用如 `filter-id` 等 IETF 属性时，必须创建规则将该属性转换为角色。VSA 不需要规则。当认证服务器将 VSA 发送给认证器时，它本质上是在说“我正在设置角色，这是值”。在这个示例中，返回的 VSA 是 `Aruba-User-Role`，该 VSA 的值就是角色分配。

为了使用 VSA，认证服务器必须支持 Aruba VSAs。认证服务器必须拥有一个厂商名为 Aruba 或厂商特定代码为 14823 的 RADIUS 字典文件、厂商属性编号、属性格式和属性值。对于每个 VSA，字典必须具有厂商分配的属性编号和属性格式（例如 `String` 或 `Integer`）。以下 CLI 命令将显示 Aruba 控制器支持的所有 RADIUS 属性。此列表包含了 Aruba VSAs 以及其他厂商属性。由于 RADIUS 属性列表非常长，因此仅显示命令输出的一部分。

```
#show aaa radius-attributes

Dictionary
| Attribute | Value | Type | Vendor Id |
| :--- | :--- | :--- | :--- |
| WISPr-Session-Term-End-Of-Day | 10 | Integer | WISPr | 14122 |
| MS-CHAP-NT-Enc-PW | 6 | String | Microsoft | 311 |
| essid | 304 | String | | |
| ARAP-Security | 73 | Integer | | |
| Tunnel-Client-Endpoint | 66 | String | | |
| Aruba-Mdps-Max-Devices | 18 | Integer | Aruba | 14823 |
| MS-CHAP-Challenge | 11 | String | Microsoft | 311 |
| Aruba-User-Role | | |
```

防火墙角色是一组防火墙策略。每个连接到 Aruba 无线网络的用户都会被分配一个角色。不同的角色允许对网络进行不同程度的访问。例如，访客用户可能只被允许与互联网进行流量传输，而员工则被允许访问互联网和公司网络。最终，AAA 配置文件（AAA profile）会在用户进行身份验证时引导角色的分配。

AAA 配置文件的创建包括为每种身份验证类型定义默认角色。尽管定义了默认角色，但可以通过多种方法分配角色。此分配过程被称为*角色派生*（role derivation），并将在第 7 章“角色派生”中进行详细介绍。

第 8 章“策略执行防火墙”不仅解释了如何将角色分配给用户，还将解释如何创建角色。现在，请记住，当你创建一个虚拟接入点（virtual AP）配置文件时，需要定义一个默认角色并将其分配给 AAA 配置文件。

## AAA 配置文件 (802.1X/EAP 认证)

AAA 配置文件的目的是将验证和角色分配所需的所有资源整合到一个逻辑结构中。AAA 配置文件指定了 802.1X 用户将进行验证的服务器组、如何执行身份验证（802.1X/EAP 认证配置文件）以及用户身份验证成功后将分配的默认权限（防火墙角色）。

AAA 配置文件本质上是 AAA 参数的组合，如图 6-3 所示，它将所有单独的部分组合成一个配置文件。请记住，服务器组由一个或多个服务器组成，防火墙角色由一个或多个防火墙策略组成；因此，AAA 配置文件实际上是以下五个组件的聚合：

- 身份验证服务器
- 服务器组
- 防火墙策略
- 防火墙角色
- 802.1X 认证配置文件

![](img/f0a787182fde585d5ed5e23c147a0298_182_0.png)

**图 6-3:** AAA 配置文件

以下 CLI 命令用于创建 AAA 配置文件，然后将服务器组、认证配置文件和默认角色链接到该配置文件：

```
(config) #aaa profile employee-aaa-profile
(AAA Profile "employee-aaa-profile") #dot1x-server-group radius-group01
(AAA Profile "employee-aaa-profile") #authentication-dot1x 1x-auth-profile
(AAA Profile "employee-aaa-profile") #dot1x-default-role authenticated
```

**Configuration** ⇒ **SECURITY** ⇒ **Authentication** ⇒ **AAA Profiles** 将带您进入菜单，在那里可以使用 WebUI 界面创建 AAA 配置文件。

## SSID 配置文件 (802.1X/EAP 认证)

AAA 配置文件定义了客户端在连接网络时必须执行的认证方法，而 SSID 配置文件定义了客户端连接到 SSID 必须具备的连接属性。因此，SSID 配置文件在 AAA 配置文件生效之前对客户端产生影响。SSID 配置文件定义了多个核心组件：客户端将连接的 WLAN 标识（SSID）、将使用的网络认证方法、将使用的加密方法，以及数据速率和 QoS 参数等组件。

要为 802.1X/EAP 认证配置 SSID 配置文件，首先需要定义 SSID；可以使用最多 32 个字符，区分大小写，且不应包含空格。

任何 802.1X/EAP 网络都应该配置 WPA2 认证和 AES 加密。Aruba 简称为 *WPA2* 的认证方法在许多操作系统中通常被称为 *WPA2-Enterprise*。

AES 加密是唯一应该使用的加密方法。IEEE 和 Wi-Fi 联盟已经声明 WEP 和 TKIP 是过时的加密方法。它们仍然被支持以保持与旧设备的向后兼容；但是，如果你选择其中一种，该 VAP 将仅使用较旧的 pre-802.11ac 和 pre-802.11n 数据速率运行。与许多厂商一样，Aruba 也实施了此项策略。

可以使用以下 CLI 命令创建 SSID 配置文件并分配带有 AES 加密的 WPA2 认证：

```
wlan ssid-profile employee-ssid-profile
essid employee1
opmode wpa2-aes
```

要进入 All Profiles 菜单（在可以在那里创建和配置 SSID 配置文件），请导航到 **Configuration** ⇒ **ADVANCED SERVICES** ⇒ **All Profiles** ⇒ **Wireless LAN** ⇒ **SSID**。

## VLAN (802.1X/EAP 认证)

如前所述，用户将验证其凭据并请求 IP 地址。配置 VAP 的重要部分是为无线 LAN 分配默认 VLAN。默认 VLAN 是 VAP 配置文件的一部分分配的。此 VLAN 在稍后的身份验证过程中可以覆盖。

以下 CLI 命令将创建 VLAN 51，在本例中我们将其分配给此无线 LAN。假设 VLAN 51 的 DHCP 服务器位于不同的子网，则还需要分配 DHCP 中继地址。

```
(config) #vlan 51
(config) #interface vlan 51
(config-subif)#ip address 10.1.51.2 255.255.255.0
(config-subif)#ip helper-address 10.254.1.21
```

*VAP 配置文件*本质上是所有 WLAN 组件的集合。其中一个部分是 VLAN，它被分配给 VAP 配置文件，所示：

```
(config) #wlan virtual-ap "employee-vap-profile" #vlan 50
```

## VLAN 池 (802.1X/EAP 认证)

随着无线 LAN 跨越楼层、建筑和园区，因此需要更多的 IP 地址。增加 IP 地址的一种方法是使用超网（supernetting）。超网的一个潜在问题是跨子网的组播和广播。作为超网的替代方案，引入了 VLAN 池。

VLAN 池是子网的集合；与其为 VAP 配置文件分配单个 VLAN，不如可以分配多个 VLAN 或 VLAN 范围。`hash` 方法使用客户端哈希值来选择 VLAN，而 `even` 方法尝试在 VLAN 之间均匀分布客户端。如果你计划使用 VLAN 池，需要研究文档以确定哪种方法适用于你。

## 命名 VLAN (802.1X/EAP 认证)

多控制器环境的挑战之一是用户 VLAN 在不同位置之间可能不同，每个位置都需要不同的 VLAN。例如，同一园区内的两个控制器可能需要不同的 VLAN，因为一个控制器位于 1 号楼，另一个位于 2 号楼。这在 VAP 配置文件中指定 VLAN 时带来了挑战。VAP 配置文件是全局配置，但它们引用的是本地 VLAN。命名 VLAN 通过链接本地 VLAN 到别名来提供更大的灵活性。

步骤如下：

1. 在主控制器上创建一个 VLAN 名称（本质是别名）。该名称会自动同步到所有本地控制器。
2. 在本地控制器上，将实际的 VLAN ID 分配给 VLAN 名称。这会将本地定义的 VLAN 映射到别名。
3. 现在，当你为 VAP 配置文件分配 VLAN 时，请分配（别名的）VLAN 名称。这是一个全局设置；但是当 VAP 分发到本地控制器时，VLAN 名称将被替换为本地 VLAN。

图 6-4 展示了位于波士顿、纽约和伦敦的 Aruba 网络。在这些位置中，都创建了两个用于员工 WLAN 的 VLAN。

![](img/f0a787182fde585d5ed5e23c147a0298_184_0.png)

**图 6-4:** 多控制器网络

波士顿：VLAN 70 和 71

纽约：VLAN 80 和 81

伦敦：VLAN 90 和 91

创建虚拟接入点（VAP）配置文件时，会为其分配一个或多个 VLAN。由于每个位置都有不同的 VLAN，因此需要为每个位置创建一个 VAP。这并不高效，也不灵活。

*命名 VLAN*（named VLAN）类似于别名。要使用命名 VLAN，必须在主控制器上创建 VLAN 名称。随后，该命名 VLAN 将自动在每个本地控制器上创建。在示例中，创建了一个名为 `employee` 的命名 VLAN。创建命名 VLAN 后，将每个地点的本地 VLAN 分配给该 VLAN 名称。此时，不再是为 VAP 分配 VLAN 编号，而是将名为 `employee` 的命名 VLAN 分配给 VAP。这允许将单个 VAP（在本例中为 `employee-vap`）分配给三个 AP 组中的：BOS、NYC 和 LON，而每个地点的 WLAN 分配有不同的 VLAN。

## 虚拟 AP 配置文件 (802.1X/EAP 认证)

创建 802.1X/EAP 无线局域网的最后一步是配置 VAP 配置文件。这只需通过将 AAA 配置文件、SSID 配置文件和 VLAN 分配给 VAP 配置文件来实现，如下 CLI 命令所示并在图 6-5 所示。
