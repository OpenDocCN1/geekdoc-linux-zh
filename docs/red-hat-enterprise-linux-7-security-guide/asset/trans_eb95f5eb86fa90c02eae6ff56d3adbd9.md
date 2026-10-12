

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_152_0.png)

### 5.3.2.2. 使用 CLI 查看 firewalld 设置

通过 CLI 客户端，可以获取当前防火墙设置的不同视图。`--list-all` 选项会显示 `firewalld` 设置的完整概览。

`firewalld` 使用区域来管理流量。如果未通过 `--zone` 选项指定区域，则该命令在分配给活动网络接口和连接的默认区域中生效。

要列出默认区域的所有相关信息：

```text
~]$ firewall-cmd --list-all
public
	target: default
	icmp-block-inversion: no
	interfaces:
	sources:
	services: ssh dhcpv6-client
	ports:
	protocols:
	masquerade: no
	forward-ports:
source-ports:
icmp-blocks:
rich rules:
```

**注意**

若要指定要显示设置的区域，请在 `firewall-cmd --list-all` 命令中添加 `--zone=区域名称` 参数，例如：

```text
[~]# firewall-cmd --list-all --zone=home
home
  target: default
  icmp-block-inversion: no
  interfaces:
  sources:
  services: ssh mdns samba-client dhcpv6-client
... [输出已截断]
```

若要查看特定信息（如服务或端口）的设置，请使用特定选项。请参阅 `firewalld` 的手册页，或通过使用命令帮助获取选项列表：

```text
[~]# firewall-cmd --help

Usage: firewall-cmd [OPTIONS...]

General Options
 -h, --help                Prints a short help text and exits
 -V, --version             Print the version string of firewalld
 -q, --quiet               Do not print status messages

Status Options
 --state                   Return and print firewalld state
 --reload                  Reload firewall and keep state information
... [输出已截断]
```

例如，要查看当前区域中允许哪些服务：

```text
[~]# firewall-cmd --list-services
ssh dhcpv6-client
```

使用 CLI 工具列出特定子部分的设置有时可能难以解读。例如，你显示 SSH 服务，`firewalld` 会为该服务打开必要的端口 (22)。稍后，如果你列出允许的服务，列表会显示 SSH 服务，但如果你列出开放端口，则不会显示任何内容。因此，建议使用 `--list-all` 选项，以确保你获取完整的信息。

## 5.4. 启动 FIREWALLD

要启动 `firewalld`，请以 `root` 身份输入以下命令：

```text
[~]# systemctl unmask firewalld
[~]# systemctl start firewalld
```

若要确保 **firewalld** 在系统启动时自动启动，请以 **root** 身份输入以下命令：

```text
~]# systemctl enable firewalld
```

## 5.5. 停止 FIREWALLD

要停止 **firewalld**，请以 **root** 身份输入以下命令：

```text
~]# systemctl stop firewalld
```

若要阻止 **firewalld** 在系统启动时自动启动，请以 **root** 身份输入以下命令：

```text
~]# systemctl disable firewalld
```

若要确保 firewalld 不会通过访问 **firewalld D-Bus** 接口而启动，并且即使其他服务需要 **firewalld** 也不会启动，请以 **root** 身份输入以下命令：

```text
~]# systemctl mask firewalld
```

## 5.6. 控制流量

### 5.6.1. 预定义服务

可以使用图形 **firewall-config** 工具、**firewall-cmd** 和 **firewall-offline-cmd** 来添加和删除服务。

或者，你可以编辑 **/etc/firewalld/services/** 目录中的 XML 文件。如果用户未添加或更改某个服务，则在 **/etc/firewalld/services/** 中找不到相应的 XML 文件。如果你要添加或更改服务，可以使用 **/usr/lib/firewalld/services/** 目录中的文件作为模板。

### 5.6.2. 在紧急情况下使用 CLI 禁用所有流量

在紧急情况下，如系统遭受攻击，可以禁用所有网络流量以切断攻击者。

要立即禁用网络流量，请开启恐慌模式：

```text
~]# firewall-cmd --panic-on
```

关闭恐慌模式会将防火墙恢复为其永久设置。要关闭恐慌模式：

```text
~]# firewall-cmd --panic-off
```

要查看恐慌模式是否已开启，请使用：

```text
~]# firewall-cmd --query-panic
```

### 5.6.3. 使用 CLI 通过预定义服务控制流量

控制流量最直接的方法是向 firewalld 添加预定义服务。这会打开所有必要的端口，并根据 *服务定义文件* 修改其他设置。

1. 检查该服务是否已允许：

```text
~]# firewall-cmd --list-services
ssh dhcpv6-client
```

2. 列出所有预定义服务：

```text
~]# firewall-cmd --get-services
RH-Satellite-6 amanda-client amanda-k5-client bacula bacula-client bitcoint-bitcoin-rpc bitcointestnet bitcointestnet-rpc ceph ceph-
mon cfengine condor-collector ctdb dhcp dhcpv6 dhcpv6-client dns
docker-registry ...
[输出已截断]
```

3. 将服务添加到允许的服务中：

```text
~]# firewall-cmd --add-service=<service-name>
```

4. 使新设置持久化：

```text
~]# firewall-cmd --runtime-to-permanent
```

### 5.6.4. 使用 GUI 通过预定义服务控制流量

要启用或禁用预定义或自定义服务，请启动 firewall-config 工具并选择要配置服务的网络区域。选择 **服务** 选项卡，并勾选每种你希望信任的服务类型。取消勾选以阻止某项服务。

要编辑服务，请启动 firewall-config 工具，并在标有 **配置** 的菜单中选择 **永久**。在 **服务** 窗口底部会出现额外的图标和菜单按钮。选择你要配置的服务。

**端口**、**协议** 和 **源端口** 选项卡允许为选定的服务添加、更改和删除端口、协议和源端口。模块选项卡用于配置 **Netfilter** 辅助模块。**目标** 选项卡允许将流量限制到特定的目标地址和 Internet Protocol（IPv4 或 IPv6）。

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_155_0.png)

**注意**

在 **运行时** 模式下，无法更改服务设置。

### 5.6.5. 添加新服务

可以使用图形 firewall-config 工具、firewall-cmd 和 firewall-offline-cmd 来添加和删除服务。或者，你可以编辑 `/etc/firewalld/services/` 中的 XML 文件。如果用户未添加或更改某个服务，则找不到相应的 XML 文件位于 `/etc/firewalld/services/`。如果你要添加或更改服务，可以使用 `/usr/lib/firewalld/services/` 中的文件作为模板。

要在终端中添加新服务，请使用 `firewall-cmd`，或者在 `firewalld` 未激活时使用 `firewall-offline-cmd`。输入以下命令以添加一个新的空服务：

```text
~]$ firewall-cmd --new-service=service-name
```

要使用本地文件添加新服务，请使用以下命令：

```text
~]$ firewall-cmd --new-service-from-file=service-name.xml
```

你可以使用附加的 `--name=service-name` 选项更改服务名称。

一旦更改了服务设置，该服务的更新副本就会被放置到 `/etc/firewalld/services/` 中。

作为 root，你可以输入以下命令手动复制服务：

```bash
~]# cp /usr/lib/firewalld/services/service-name.xml \
    /etc/firewalld/services/service-name.xml
```

`firewalld` 首先从 `/usr/lib/firewalld/services` 加载文件。如果文件放置在 `/etc/firewalld/services` 中且有效，那么这些文件将覆盖来自 `/usr/lib/firewalld/services` 的匹配文件。一旦 `/etc/firewalld/services` 中的匹配文件被删除，或者当要求 `firewalld` 加载服务默认值时，`/usr/lib/firewalld/services` 中被覆盖的文件将被使用。这仅适用于永久环境。要在运行时环境获取这些回退设置，需要重新加载。

### 5.6.6. 使用 CLI 控制端口

端口是逻辑设备，使操作系统能够接收并区分网络流量，并相应地将其转发到系统服务。通常由一个监听该端口的守护进程来表示，即它等待传入该端口的任何流量。

通常，系统服务监听为其保留的标准端口。例如，`httpd` 守护进程监听端口 80。然而，系统管理员默认配置守护进程监听不同的端口，以增强安全性或出于其他原因。

#### **打开端口**

通过开放端口，系统可以从外部访问，这代表安全风险。通常，保持端口关闭，仅当特定服务需要时才打开它们。

要获取当前区域中开放端口的列表：

1. 列出所有允许的端口：

```bash
~]# firewall-cmd --list-ports
```

2. 添加端口到允许端口以开放传入流量：

```bash
~]# firewall-cmd --add-port=port-number/port-type
```

