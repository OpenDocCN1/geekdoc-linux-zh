
系统重启后，您需要为服务器上的 `root` 用户设置密码。`root` 是 Linux 系统管理员的名称。与普通用户（可能权限在系统上执行某些操作）不同，`root` 拥有执行任何操作的无限权限。作为 `root` 用户，您可以：

- 访问系统中的每个文件和设备
- 修改系统配置
- 安装软件
- 设置硬件

`root` 账户应用于系统管理、维护和修复。以 `root` 身份登录日常工作是有风险的——一个小的错误就会导致许多系统文件遭受不可挽回的损失。

您需要在安装过程中设置 `root` 密码。YaST 显示如下屏幕：

# 第 2 部分 安装 SUSE Linux Server 11

图 2-27 SLES 11 安装：Root 密码 "root"

![](img/1402b35afb63db85442c13e1f1f806f4_197_0.png)

感谢 Novell, Inc.

在对话框的两个文本字段中输入相同的密码。

您应该使用一个不容易猜的密码。我们建议您使用数字和大写字母以避免字典攻击。如果需要，可以选择 **Expert Options** 来自定义密码加密算法。在大多数情况下，您只需使用 **Blowfish** 的默认设置。

输入 `root` 密码后，点击 `Next` 继续。如果密码太简单或太弱，将显示警告。您可以返回指定更强的密码，或接受较弱密码并继续。

## 设置主机名

接下来，您需要为服务器设置主机名。YaST 建议默认主机名为 `linux-xxxx`，其中 `xxxx` 由随机字符组成。域名默认为 `site`。将主机名和域名更改为适用于您网络的正确值。

如果您网络上的计算机通过 DHCP 选项获取主机名和域名，可以勾选 `Change Hostname via DHCP`。否则，您应该取消选择此选项并选择 `Write Hostname to /etc/hosts`。

完成后，点击 `Next`。

## 配置网络

接下来，您需要在大服务器上设置网络配置。YaST 显示网络配置屏幕，如下所示：

图 2-28 SLES 11 安装：网络配置

![](img/1402b35afb63db85442c13e1f1f806f4_198_0.png)

在此屏幕的顶部，您可以选择以下选项之一：

- Skip Configuration（跳过配置）。暂时跳过网络配置。您可以在系统安装完成后后再配置网络设置。
- Use Following Configuration（使用以下配置）。使用当前显示的网络配置建议。

网络配置建议与基础安装初期的安装建议类似。可以选择标题来查看和配置特定参数。该建议包含以下项目：

- General Network Settings（通用网络设置）。让您在传统的网络连接管理方法和使用 NetworkManager 工具之间进行切换。在服务器上，您应该使用传统方法。NetworkManager 工具更适用于笔记本系统，允许用户在有线和无线接口之间切换。
- Firewall（防火墙）。让您自定义防火墙设置。如果您希望能够使用 SSH 远程管理服务器，请通过选择 open 来将“SSH port is blocked”切换为“SSH port is open”。
- 此外，您可以通过选择 `Disable` 来完全禁用防火墙。选择 **Firewall** 标题本身会打开对话框，允许您配置详细的防火墙设置。
- `Network Interfaces`（网络接口）。显示系统检测到的网络接口及其配置设置。
- `DSL Connections`（DSL 连接）。显示系统检测到的 DSL 设备及其配置设置。
- `ISDN Adapters`（ISDN 适配器）。显示系统检测到的 ISDN 设备及其配置设置。
- `Modems`（调制解调器）。显示系统检测到的模拟调制解调器及其配置设置。
- `VNC Remote Administration`（VNC 远程管理）。让您使用 VNC 配置远程管理。
- `Proxy`（代理）。显示 HTTP 和 FTP 代理。

可以通过选择项目的标题或从 `Change` 下拉列表中项目更改配置。此菜单还允许您将所有设置重置为 YaST 生成的默认值。如果您不确定使用哪些设置，请使用 YaST 生成的默认值。

默认情况下，您的网络接口配置为使用 DHCP。由于您正在配置服务器系统，应该配置网络接口使用静态 IP 地址。选择 `Network Interfaces` 标题执行此操作。

YaST 显示 `Network Settings Overview`（网络设置概述）。它列出了所有已配置和未配置的网络卡：

### 图 2-29 SLES 11 安装：网络设置

![](img/1402b35afb63db85442c13e1f1f806f4_200_0.png)

屏幕的上半部分显示网卡列表。下半部分显示所选卡的配置。

此时，您可以执行以下操作之一：

- Add a Network Card（添加网卡）
- Edit an Existing Configuration（编辑现有配置）
- Delete an Existing Configuration（删除现有配置）

如果您想配置未检测到的网卡，将显示 `Hardware` 对话框：

### 第 2 部分 安装 SUSE Linux Server 11

图 2-30 SLES 11 安装：Hardware 对话框

![](img/1402b35afb63db85442c13e1f1f806f4_201_0.png)

感谢 Novell, Inc.

在此屏幕上，您可以配置以下内容：

- Device Type（设备类型）。网络设备（如以太网、蓝牙等）
- Configuration Name（配置名称）。如果您的网络是 PCMCIA 或 USB，选择相应的设备。YaST 会自动为所选网卡加载适当驱动程序。

2. 点击 `Next`。

### 执行 SLES 11 安装

图 2-31 SLES 11 安装：网卡设置

![](img/1402b35afb63db85442c13e1f1f806f4_202_0.png)

如果您选择了 Wireless 作为设备类型，将显示 Network Card Setup 对话框：

3. 在 Address 标签页使用以下选项配置您的接口：

- Dynamic Address（动态地址）。如果您的网络使用 DHCP 服务器，可以选择此选项自动设置系统网络地址。您可以从下拉列表中选择几种动态地址分配方法。如果您的本地网络运行着 DHCP 服务器，请选择 DHCP。如果您想搜索 IP 地址并进行静态分配，请从下拉列表中选择 Zeroconf。选择 DHCP + Zeroconf。
- Statically Assigned IP Address（静态分配 IP 地址）。如果您想使用静态地址，请选择此选项。然后为网络输入相应的 IP 地址和子网掩码。您还应该在 Hostname 字段中输入服务器的主机名。
- Hostname and Name Server（主机名和名称服务器）。让您可以手动设置主机名和名称服务器。

4. 配置您的设置，然后选择 WEP Keys 输入密钥信息。

5. 完成后，点击 `Next` 返回 Network Settings。

### 编辑现有配置

除了添加新的网络接口外，还可以编辑现有的接口配置。要编辑网卡，请执行以下操作：

1. 从 Network Settings 对列表中选择网卡，点击 `Edit`。
2. 选择 Hostname/DNS 标签页。

图 2-34 SLES 11 安装：网络设置

![](img/1402b35afb63db85442c13e1f1f806f4_205_0.png)

5. 输入以下内容：

- 主机名 (Hostname)
- 域名 (Domain name)
- 名称服务器 (Name servers)

6. 选择“路由 (Routing)”选项卡。

显示以下内容：

SLES 11 安装：网络设置

![](img/1402b35afb63db85442c13e1f1f806f4_206_0.png)

7. 在“默认网关 (Default Gateway)”字段中输入您的默认网关路由器 IP 地址。

8. 点击 `OK`。

#### 删除现有配置

要删除现有的网卡配置，请在网络设置界面的顶部选中它并点击 `Delete`。

完成添加、编辑或删除网卡配置后，保存网络设备配置并点击 `OK` 返回到网络配置建议。

完成网络接口配置后，点击 `Next`。

### 测试互联网连接

接下来，YaST 将要求你测试与互联网的连接：

#### 第 2 节 安装 SUSE Linux Enterprise Server 11

图 2-36 SLES 11 安装：互联网连接测试

![](img/1402b35afb63db85442c13e1f1f806f4_207_0.png)

选择以下选项之一：

- 是，测试互联网连接。YaST 将通过下载最新的发行说明并检查可用更新来尝试测试互联网连接。结果将在下一个屏幕显示。
- 否，跳过此测试。YaST 将跳过连接测试。如果你这样做，你可以在安装期间更新系统。

选择上述任一选项并点击 `Next`。
