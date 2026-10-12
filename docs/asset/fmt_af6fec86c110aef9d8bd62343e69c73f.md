
7. 重启 Portainer 后，你可以返回浏览器并刷新页面。现在应该可以进入 Portainer 欢迎页。

![](img/110fa0d6324f93fff03cee639414d_473_1.png)

# 新 Portainer 安装

请创建初始管理员用户。

| 用户名 | admin |
| --- | --- |
| 密码 | |
| 确认密码 | |
| 此连接是不安全的。在此输入的登录信息可能会被破解。了解更多
使用安全生成的密码
<vH6VGU3S0fe3RK>
它将为此网站保存此密码。
查看保存的登录信息

密码至少需要 12 个字符

创建用户

允许收集匿名统计数据。你可以在我们的隐私政策中找到更多信息。

# 从备份恢复 Portainer

图 13.24 – Portainer 初始配置

8. Portainer 将让你为环境设置一个 12 位的字母数字密码。

![](img/110fa0d6324f0893fff03cee6394144d_474_0.png)

## 安装新的 Portainer

请创建初始管理员用户。

| 用户名 | admin |
| --- | --- |
| 密码 | ************ |
| 确认密码 | ************ |

> 此连接不安全。在此处输入的登录信息可能会被泄露。了解更多

密码长度至少为 12 个字符。

允许收集匿名统计数据。你可以在我们的隐私政策中找到更多信息。

从备份恢复 Portainer

图 13.25 – Portainer 密码创建

现在你拥有了一个运行在 Docker 容器中的 Portainer 环境，该环境由 OCI 中的一台虚拟机托管。

## 使用 VirtualBox 将虚拟机跳迁到 OCI

处理工作负载的 9 到 5 点工作。

在这些配方中的一个共同因素是将工作负载从一个环境移动到另一个环境。在不同类型的虚拟机程序（例如 VMware、KVM 和 Xen）之间进行工作是使用通用格式，例如**开放虚拟化格式/开放虚拟化设备 (OVF/OVA)** 完成的。本质上，这会将组件放入大多数虚拟化环境都能理解的清晰格式。镜像在虚拟化格式之间是可以传输和交换的。在这种情况下，有几个需要到位的碎片，例如网络、存储以及连接驱动器数量限制。

想象这样一个世界：任何工作负载（无论是基于应用程序还是数据库的）可以在整个项目周期内随你，并在不同的虚拟机集群或云服务供应商（CSP）之间传输。你可以带着这些创建的环境穿于你的环境中。

VirtualBox 作为宿主机存在于你的系统中，并被分类为“2 型”虚拟机程序，允许在你的主机环境中运行多个虚拟机。VirtualBox 具有人们对大型企业产品所预期的所有方面，只是被分解成了更小、更简单的部分。计算和内存资产是从你的主机环境（计算机）中划分的。存储组件由本地硬盘的部分或外部存储环境（如外部 NVMe 驱动器）组成。最后，网络由桥接组件组成，这些是位于物理接口之上的虚拟网络。

### 先有虚拟机还是先操作系统？

每一次演进都始于基础。在我们考虑将虚拟机从 VirtualBox 迁移到 OCI 之前，我们必须为迁移准备虚拟机。在 VirtualBox 的情况下，在构建迁移到云环境（如 OCI）的虚拟机之前只有几项需要完成。我们将在整个配方中介绍这些前提条件。接下来的图描述了配置迁移虚拟机到 CSP 的阶段。

![](img/110fa0d6324f0893fff03cee6394144d_475_0.png)

图 13.26 – 虚拟机配置阶段

## 准备工作

准备操作系统与在盖房子之前打基础没有区别。我发现最初在 VirtualBox 用户界面配置上配置操作系统比较简单，然后当你启动网络并建立通信时，意味着你已经有了与虚拟机的连接性。

准备将虚拟机镜像导入到 OCI 作为镜像有五个阶段。阶段如下：

- 1. **接口名称**：这涉及标准化，以确保接口名称被主机环境识别。这可以转换为主机系统如何实现网络。
- 2. **接口配置**：在这里，我们确认没有 MAC 地址，以及其他预配置任务。重复的 MAC 地址会导致额外的复杂性，这成为配置中的一个关键点。
- 3. **GRUB(2) 配置**：这涉及准备内核。
- 4. **串口控制台配置**：这一步是导入时常见的错误。没有它，你的 OCI 环境将导入失败，或者虚拟机将无法启动。
- 5. **重启操作系统**，即重启你的机器。

接下来的图显示了从启动到重启的操作系统配置阶段：

![](img/110fa0d6324f0893fff03cee6394144d_476_0.png)

注意更改后的接口名称：

```
root@small-018 ~# dmesg | grep -i eth

[ 4.702620] e1000 0000:00:03.0 eth0 (PCI:33MHz-2bit) 08:00:27:64

[ 4.702628] e1000 0000:00:03.0 eth1 (PCI:33MHz-2bit) Network Connection

[ 5.731103] e1000 0000:00:08.0 eth2 (PCI:33MHz-2bit) 08:00:27:98

[ 5.731132] e1000 0000:00:08.0 eth3 (PCI:33MHz-2bit) Network Connection

[ 5.372962] e1000 0000:00:08.0 enp0s renamed from eth1

[ 5.374971] e1000 0000:00:03.0 enp0s renamed from eth0
```

我们需要按照以下块中的更改在内核上执行更改，重命名接口名称。这将需要 `GRUB(2)`，因为 `GRUB` 是内核和操作系统之间的中间层。我们有了当前的接口名称，那么我们要去哪里呢？我们将接口重命名为更易接受的名称，例如 `net0`。所以，我们必须移动 (`mv`) 或重命名接口名称：

```
root@small-018:network-scripts# mv /etc/config/network-scripts/ifcfg-enp0s

/etc/config/network-scripts/ifcfg-enp0s

root@small-018:network-scripts# mv /etc/config/network-scripts/ifcfg-enp0s

/etc/config/network-scripts/ifcfg-1
```

重命名它们后，我们需要更改配置文件中的条目以匹配接口。在接下来的代码中，我们正在重命名 `net0` 的配置：

```
root@small-018:network-scripts# vi /etc/config/network-scripts/ifcfg-net0

TYPE=ethernet

PROXY_METHOD=none

BROWSER_ONLY=no

BOOTPROTO=dhcp

DEFROUTE=yes

IPV4_TIMEOUT=no

IPV6_INIT=yes

IPV6_CONF=yes
```
`IPV6_FAILURE=no`
`IPV6_GEN_MODE=ui64`
`NAME=enp03`
`UUID=e958f0d8-3fcc-4a43-b605-79abc99f`
`DEVICE=enp03`
`UNBOOT=yes`
`TYPE=ethernet`
`PROXY_METHOD=none`
`BROWSER_ONLY=no`
`BOOTPROTO=dhcp`
`IPV4_FAILURE=no`
`IPV6_INIT=yes`
`IPV6_AUTCONF=yes`
`IPV6_ROUTE=yes`
`IPV6_FAILURE=no`
`IPV6_GEN_MODE=ui64`
`NAME=net0`
`UUID=e958f0d8-3fcc-4a43-b605-79abc99f`
`UNBOOT=yes`
```

我们在这里的操作与之前相同，但在这种情况下我们正在更改 `net1`：
