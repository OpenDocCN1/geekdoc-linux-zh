
在我的个人电脑上，`enp4s0` 是我的网络接口，`lo` 是环回接口。环回接口允许机器与自身通信——其他计算机无法通过环回接口访问这台计算机。如果我们想运行某个服务，但不希望让网络上的其他机器访问，这就非常有用。`enp4s0` 是我的以太网口。在我的服务器上，`enol1` 是以太网口插入的接口，因此我将 `enol1` 替换为你实际的网络接口名称。不过，我会使用那个名称。

- 1. 运行此命令创建或编辑 netplan 配置文件：

```
sudo nano /etc/netplan/01-netplan.yaml
```

- 2. 将内容替换为以下配置。我在每行都添加了注释，以便你知道应该留多少空格：

```
networks:
  # 0 spaces
  version: 2 4 spaces
  renderer: networkd 4 spaces
  ethernets:
    eno1: # 4 spaces
      dhcp4: no 12 spaces
  bridges:
    br0: # 8 spaces
      interfaces: [eno1] 12 spaces
      addresses:
        - 192.168.5.2/24 16 spaces
      routes:
        - to: default 12 spaces
          gateway: 192.168.5.1 16 spaces
      nameservers:
        addresses: [8.8.8.8] 12 spaces
```

- 3. 完成后，记得更改你的 netplan 文件的权限，否则 netplan 不会信任你，路径为：

```
sudo chmod 600 /etc/netplan/01-netcfg.yaml
```

> 配置说明：`enol1` 将成为 `(br0)` 的一部分，但将不再拥有 IP 地址。`br0` 是桥接接口，将分配静态 IP `192.168.5.2`。`br0` 接口将配置与之前相同的网关和 DNS 服务器设置。网关是 `psfe` 路由器，这是它连接以获取 IP 地址并连接到互联网（即“最后出口网关”），而 DNS 服务器是我们的路由器；这是它连接以将 google 等内容翻译为 `142.250.138.101`。`br0` 是我们创建的虚拟接口，`enol` 是这台机器上存在的接口。你的网络接口很可能是其他的；这个是过时的。请根据你所有机器的实际名称使用你的网络接口。

注意：你可能习惯了旧式的配置文件，在那里 `pasv_enable=YES` 等同于 `pasv_enable:YES`。YAML 不是那样的写法。一个空格就是你与“正常运行且幸福”以及“彻底的痛苦”之间的区别。YAML 对空格敏感；缩进错误至关重要，并会导致配置文件无法工作。某些文本编辑器对编辑 yaml 文件很有帮助，可以帮你避免错误。有些则没有

# 第 4 步：应用新配置

现在配置已就绪，请应用它。

- 1. 运行以下命令应用新的 netplan 配置：

```
sudo netplan apply
```

> 注意：你可能会出错，因为 yaml 文件是极其严格的；为了确保配置生效，请在运行 `netplan apply` 之前运行 `netplan try`。虽然 达说“要做或不做，没有尝试”是有道理的，但他从未处理过 Linux 文档。

- 2. 运行此命令验证桥接接口是否已启动并具有正确的配置：

```
ip addr show br0
```

- 3. 你应该看到 `br0` 拥有 IP 地址 `192.168.5.2`。

- 4. 运行以下命令检查路由表，确保默认路由设置正确：

```
ip route show
```

- 5. 验证默认路由指向 `192.168.5.1`。

# 第 5 步：测试网络配置

验证更改后你的服务器是否仍然可以访问网络。

- 1. 通过运行 ping 路由器：

```
ping 192.168.5.1
```

- 2. 运行 ping 外部 IP 以测试连通性。这是 Google 的 DNS 服务器，它应该一直在线：

```
ping 8.8.8.8
```

# 第 6 步：为桥接添加 iptables 规则

为了让桥接正常工作，你需要允许桥接接口上的流量转发。这需要 iptables 规则并让它们在重启后保持有效。这是一个非常重要的细节，在设置桥接接口的指南中经常被遗漏（https://www.tecmicro.com/create-network-bridge-ubuntu/）。跳过这部分将导致设置无效；你将深陷于 GNU/Linux 论坛发帖的地狱，那里智商为 180 的人会告诉你“RTFM（去读手册）”，哥们，那手册有 200000 多页。

这好比德雷克·杰特（Derek Jeter）告诉你“盯着球看”。

你可能会奇怪为什么会这样。用开源配置东西就像 12 年前的 Macbook 维修一样：它是一个俱乐部，而你不在其中。大多数老师都熟悉自己的领域。结果，他们忘记了第一次尝试某事是什么感觉。

这就是为什么我要像我这样从零开始构建机器。告诉我在我的机器上是如何做的永远行不通的。会有一些我潜意识里知道但你不知道的小细节；或者可能我自己也忘记了某些细节，因为是我十年前在衣柜里设置过的的服务！

通过执行我所写的任务，我被迫为你提供**确实有效**的指令。

- 1. 运行以下命令添加 iptables 规则：

```
sudo iptables -I FORWARD 1 -br0 -j ACCEPT
sudo iptables -I FORWARD 1 -o br0 -j ACCEPT
```

注意：这些 iptables 规则通过桥接接口通过，因此你的虚拟机可以在你的网络上工作。没有它们，你的虚拟机将无法连接，你也无法连接到它们（使用 `'-I'` 会将它们置于顶端）。iptables 中规则的顺序非常重要。如果流量转发未按预期工作，请运行 `'sudo iptables -L -v -n'` 来检查规则和顺序。

- 2. 运行以下命令验证 iptables 规则：

```
sudo iptables -L
```

你应该能看到在 `br0` 上接受流量的规则。

# 第 7 步：使 iptables 规则持久化

为了确保 iptables 规则在重启后仍然生效，你需要保存它们并配置为在启动时加载。

1. 安装 iptables-persistent 包：

```bash
sudo apt install iptables-persistent
```

2. 安装过程中，会询问你是否保存当前的 iptables 规则。选择 Yes。

3. 如果没有提示，可以通过运行以下命令手动保存规则：

```
sudo netfilter-persistent save
```

> 注意：安装 iptables-persistent 是为了让 iptables 在重启后依然。你不会经常关闭它。几个月后当你真的关闭它时，你不会忘记指南中的任何一个字符，更不用说上面的 iptables 规则了！也不会忘记规则缺失会导致你的虚拟机无法工作。

4. 通过检查文件 `/etc/iptables/rules.v4` 确认规则已保存。通过这些更改，桥接接口现在可以正确允许流量。iptables 规则将在重启后持续，虚拟机可以从相同的网络获取 IP 地址。为虚拟机准备 Ubuntu

接下来，让我们使用虚拟机管理器 (`virt-manager`) 为虚拟机准备 Ubuntu。我们将涵盖从准备 ISO 到配置静态 IP 的所有内容，包括安装 GUI。在创建虚拟机之前，你需要将 Ubuntu ISO 放在正确的目录并设置正确的权限。你可以通过使用 SSH FTP 和像 Filezilla 这样的程序进行传输。或者，如果你是个动物，可以去 ubuntu.com 下载 LTS 版本的 Ubuntu Server。

- 1. 将你用于安装接口的 USB 盘放到你的服务器上。你可以通过将其挂载磁盘、使用 SSH FTP 和像 Filezilla 这样的程序进行传输。或者，如果你是个动物，可以去 ubuntu.com 下载 LTS 版本的 Ubuntu Server。

- 2. 将 ISO 文件移动到 `/var/lib/libvirt/images/`，将源位置和文件名更改为你实际的。只要文件进入 `/var/lib/libvirt/images/` 就没问题：

```
sudo mv ~/Downloads/ubuntu-server.iso /var/lib/libvirt/images/
```

- 3. 更改 ISO 文件的所有权和组：

```
sudo chown libvirt-qemu:libvirt /var/lib/libvirt/images/ubuntu-server.iso
```
