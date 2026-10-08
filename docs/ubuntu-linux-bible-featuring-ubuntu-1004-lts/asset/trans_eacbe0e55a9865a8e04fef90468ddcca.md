

## 第 24 章：使用虚拟机和模拟器

- 3. 修改系统启动过程中创建与 VirtualBox 关联的设备时使用的规则文件，添加一条规则指定 TUN/TAP 虚拟设备 `/dev/net/tun` 将允许 `vboxusers` 组中的任何人写入。你需要将以下条目添加到 /etc/udev/rules.d/99-virtualbox-ose.rules 文件的末尾。以下内容应单行输入，不要包含冒号：

```
KERNEL==="vboxdrv", NAME="vboxdrv", OWNER="root", MODE="0660"
```

- 4. 如果你正在使用 Network Manager 或 WicD 管理网络接口，请确保它不会自动激活或连接 eth0。

- 5. 重启你的系统。当系统重新启动后，你可以使用 `brctl` 命令验证是否已创建桥，以及正确的物理和虚拟网络设备已附加到其上。在本节中使用的示例相关输出如下：

```
$ brctl show
bridge name id STP enabled interfaces
br0 8000.019d1239f01 no eth0
```

你还应该执行 `route -n` 命令来验证路由设置是否正确——你只会看到几条记录，它们都与桥有关。

- 6. 启动 VirtualBox 并更新每台虚拟机的网络配置信息。操作步骤如下：

  - a. 在左窗格中选择一个虚拟机，点击 VirtualBox 工具栏中的设置图标。设置对话框将弹出，显示虚拟机的当前配置。点击左窗格中的“Network”项，将显示如图 24-19 所示的对话框。

    注意
    设置图标仅适用于已正常关闭且没有快照或保存状态信息的系统。在修改虚拟机的任何设置之前，你必须删除你的快照和保存状态信息。■

  - b. 点击“Attached to”旁边的向下箭头，从下拉列表中选择“Bridged Adapter”（桥接适配器）。点击“Name”下拉列表并选择你之前创建的桥名称（如果你完全按照此操作，则选择 br0）。对话框看起来应该如图 24–20 所示。

  - c. 点击 OK 保存更新后的网络配置信息。

## 第二部分：面向桌面用户的 Ubuntu

虚拟机的默认网络设置

![](img/1a233c34336fbf5a85d6eb785e401709_927_0.png)

虚拟机的主机接口设置

![](img/1a233c34336fbf5a85d6eb785e401709_927_1.png)

更新完所有虚拟机后，现在启动的任何虚拟机都将成为你本地网络的真正公民。真不错！

## 为 VirtualBox 虚拟机访问重新映射端口

端口转发是一种技术，一个系统将某些网络端口上的请求转发到另一个系统。现在，端口转发通常用于家庭网关，将来自外部网关的请求转发到内部网络上的特定系统。VirtualBox 提供了内置的端口转发支持，允许外部系统（或你的主机系统）直接访问虚拟机上的服务，而无需让虚拟机成为本地网络的完全参与者。

你使用 `VBoxManage` 命令来设置端口转发，这必须在虚拟机未实际运行时进行。对于你想要连接到虚拟机的每个服务，需要三条命令，如下所示，该示例允许外部访问运行在旧虚拟机 Ubuntu-Hardy 上的 SSH 服务器：

```
VBoxManage setextradata "Ubuntu-Hardy" \
VBoxInternal/Devices/pcnet/0/LINU/Config/ssh/Protocol" TCP
VBoxManage setextradata "Ubuntu-Hardy" \
VBoxInternal/Devices/pcnet/0/LINU/Config/ssh/GuestPort" 22
VBoxManage setextradata "Ubuntu-Hardy" \
VBoxInternal/Devices/pcnet/0/LINU/Config/ssh/HostPort" 2222
```

（这些命令通常在单行中输入——每行中的反斜杠仅是为了书中的格式化目的。）

这些命令中的第一条识别你正在转发的网络协议。第二条识别虚拟机上的端口，主机上特定端口的请求应被转发到该端口。第三条识别主机上的端口，外部系统通过它联系与此规则关联的服务。该规则的名称是 Config 条目之后、规则关键字之前的字段——在本例中，规则名称为 ssh。

一旦你输入了上述命令，该规则就会永久地定义在指定虚拟机（在本例中为 Ubuntu-Hardy）的 VirtualBox 配置中。启动虚拟机后，网络上的任何主机都可以类似 `ssh host-system -p 2222` 的命令访问虚拟机上的 SSH 服务。

在 VirtualBox 中设置端口转发时，你需要识别虚拟机上运行服务的端口（可以通过检查 /etc/services 文件来实现），并在主机上选择一个没有正在运行服务的端口。你应该始终使用大于 1 的端口号。

将来，如果你忘记了设置的规则，可以使用 `VBoxManage` 列出所有端口转发规则。

## 解决虚拟机启动问题

如前所述，如果你想运行 VirtualBox，必须是 `vboxusers` 组的成员。即使当前用户是该组成员，可能会遇到的一个常见问题是 `/dev/kvm` 不可用。要解决这个问题，你应该更改设备的所有者：

```
sudo chown root:vboxusers /dev/kvm
sudo chmod 660 /dev/kvm
```

另一个常见问题是，如果系统启动时自动加载了其他技术的可加载内核模块，检查 /etc/modules/ 下的符号链接——你可以使用以下命令删除指向“其他””的符号链接：

```bash
sudo rmmod kvm_intel kvm
```

