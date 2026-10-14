
# 第二部分：Ubuntu 桌面用户

## 第 24 章：使用虚拟机和模拟器

第一部分将 `eth0` 定义为网络启动时自动启动的 TCP/IP 网络设备，但手动配置静态 IP 地址 `0.0.0.0`，并将其设置为混杂模式。混杂模式是一种特殊模式，网络接口可以接收网络上的所有流量，即使流量不是给该特定网卡的。在本节使用的示例中，注释掉任何现有网络设备（`eth0`）条目！第二部分说明 `br0` 是在网络启动时自动启动的 IP 桥（因为有 `bridge_ports` 条目），通过 DHCP 获取配置，在跨桥接器转发数据包时不施加延迟（`bridge_fd` 条目），桥接器在启动后立即进入转发模式（`bridge_maxwait` 条目），并且该接口被认为是可以到达默认网关的高优先级接口

### 提示

遗憾的是，Ubuntu 系统没有提供描述如何在 `/etc/network/interfaces` 文件中定义设置的映射。有关我使用的设置（以及我未使用的设置）的更多信息，请参阅 `bridge-utils-interface additions` 页面，你可以在网络上的以下位置找到：`http://web.iesrodeira.com/cgi-bin/man/man2html.bridge-interfaces5`。

3. 修改在启动过程中创建与 VirtualBox 关联的设备时使用的规则文件，添加一条规则，指定 TUN/TAP 虚拟设备 `/dev/net/tun` 允许 `vboxusers` 组中的任何人写入。你需要将以下内容添加到 `/etc/udev/rules.d/99-virtualbox-ose.rules` 文件的末尾。以下内容应单行输入，且不要包含 `\` 字符：

    ```
    KERNEL=="vboxdrv", NAME="vboxdrv", OWNER="root", MODE="0660"
    ```

4. 如果你正在使用 Network Manager 或 WiIC 管理你的网络接口，请确保它不会自动激活或连接 `eth0`。

5. 重启你的系统。当系统重新启动后，你可以使用 `brctl` 命令验证是否已创建桥接，以及是否挂载了正确的物理和虚拟网络设备。本节使用的示例输出如下所示：

    ```
    $ brctl show
    bridge name id STP enabled interfaces
    br0 8000.019d1239f01 no eth0
    ```

    你还可以通过执行 `route -n` 命令发现路由设置正确——你只会看到几条条目，它们都与桥接有关。

6. 启动 VirtualBox 并更新你每台虚拟机的网络配置信息。要实现这一点：

    a. 在左窗格中选择一个虚拟机，点击 VirtualBox 工具栏中的“设置 (Settings)”。设置对话框弹出，显示指定虚拟机的当前配置。点击左窗格中的“网络 (Network)”项，显示如图 24-19 所示的对话框。

    > **注意**：“设置”仅适用于已正常关闭且没有快照或保存状态信息的系统。在修改虚拟机的任何设置之前，你必须删除你的快照和保存状态信息。

    b. 点击“连接到 (Attached to)”项旁边的下拉列表，从下拉列表中选择“桥接适配器 (Bridged Adapter)”。点击“名称 (Name)”下拉列表，选择你之前创建的桥接名称（如果你完全按照操作，则选择 `br0`）。对话框看起来应该如图 24-20 所示。

    c. 点击“确定”保存更新后的网络配置信息。

#### 图 24-19

虚拟机的默认网络设置

![](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_927_0.png)

#### 图 24-20

虚拟机的宿主机接口设置

![](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_927_1.png)

在更新了所有的虚拟机后，现在启动的任何虚拟机都将成为你本地网络的真正公民。还不错吧！

### 为 VirtualBox 虚拟机访问重映射端口

端口转发（Port forwarding）是一种技术，一个系统将网络端口上的请求转发到另一个系统。如今，端口转发可能最常用于网关，将来自外部网关的请求转发到内部网络上的特定系统。VirtualBox 提供了端口转发的内置支持，允许外部系统（或你的宿主机系统）直接访问虚拟机上的服务，而无需让虚拟机成为本地网络的完全参与者。

你使用 `VBoxManage` 来设置端口转发，这必须在虚拟机未实际运行时完成。对于你想要在虚拟机上访问的每个服务，都需要执行三个命令，如下例所示，它允许外部访问运行在你的 Ubuntu-Hardy 虚拟机上的 SSH 服务器：

```
VBoxManage setextradata "Ubuntu-Hardy" \
"VBoxInternal/Devices/pcnet/0/dev0#/Config/ssh/Protocol" TCP
VBoxManage setextradata "Ubuntu-Hardy" \
"VBoxInternal/Devices/pcnet/0/dev0#/Config/ssh/GuestPort" 22
VBoxManage setextradata "Ubuntu-Hardy" \
"VBoxInternal/Devices/pcnet/0/dev0#/Config/ssh/HostPort" 2222
```

（这些命令通常在单行中输入——每行末尾的反斜杠仅用于书中的格式化排版。）

这些命令中的第一个识别了你正在转发的网络传输协议。第二个识别了虚拟机上的端口，来自你宿主机特定端口的请求应该被转发到该端口。第三个识别了你宿主机系统上的端口，外部系统使用该端口连接与此规则关联的服务。该规则的名称是第一个 `Config` 条目，且位于规则关键字之前——在本例中，规则名称为 `ssh`。

一旦你输入了所示命令，该规则就会永久定义在特定虚拟机（在本例为 Ubuntu-Hardy）的 VirtualBox 配置信息中。启动虚拟机后，网络上的任何主机都可以通过命令 `ssh host-system -p 2222` 访问你虚拟机上的 SSH 服务。

在 VirtualBox 中设置端口转发时，你需要识别虚拟机上运行特定服务的端口（你可以通过 `/etc/services` 文件实现此操作），并在宿主机系统上选择一个没有现有服务运行的端口。你始终应该在宿主机系统上使用大于 1,024 的端口号，因为小于 1,024 的端口号通常保留给可能在物理系统上实际运行的服务。

将来，如果你不记得设置了哪些规则，可以使用类似 `VBoxManage getextradata Ubuntu-Hardy enumerate` 的命令列出你为特定虚拟机定义的任何端口转发规则。

### 解决虚拟机启动/安装问题

正如本节早期提到的，任何想要运行 VirtualBox 用户必须是 `vboxusers` 组的成员。这通常对安装 VirtualBox 的用户自动完成，但其他用户在通过类似 `sudo adduser USERNAME vboxusers` 的命令加入 `vboxusers` 组之前无法运行 VirtualBox。

即使当前用户是该组的成员，你可能会遇到的相关问题是：一个对话框提示当前用户无法访问 `/dev/vboxdev` 设备。该设备应始终由 `root` 用户和 `vboxusers` 组所有，并应设置为 `0660`，以便 `vboxusers` 组中的成员可以读写。你可以通过以下命令手动设置：

```
sudo chown root:vboxusers /dev/vboxdev
sudo chmod 0660 /dev/vboxdev
```

另一个常见问题是当你在使用多种虚拟化技术时，不同的虚拟化方案并不总是兼容。例如，当内核中加载了 KVM 虚拟机时，你会看到类似图 24-21 所示的错误：

![](img/c20d2eef7a2778ee7a3a4ec5714c4d3c_927_1.png)

幸运的是，这个对话框具有误导性，提示你需要重新编译内核。要解决这个问题，你需要使用以下命令移除加载的模块：

```
sudo /sbin/rmmod kvm-intel kvm-amd
```

运行此命令后，你应该关闭 VirtualBox 窗口，点击虚拟机的“重启”，并继续内核

### 提示

系统启动时，其他技术的可加载内核模块会自动加载。检查 `/etc/rc.d` 中的启动脚本——你可以删除指向“其他”虚拟化技术（如 KVM）的符号链接，以防止下次启动时加载其内核模块。

### 安装和使用 KVM
