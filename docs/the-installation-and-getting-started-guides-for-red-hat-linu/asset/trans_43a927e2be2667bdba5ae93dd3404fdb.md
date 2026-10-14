

```
-gateway 10.0.2.254 ~
-nameserver 10.0.2.1
```

**请注意：** 整个网络配置必须出现在同一行！我们在这里进行了换行以便于阅读。

如果你使用静态方法，有两点限制必须牢记：

所有静态网络配置信息必须指定在一行上；你不能使用反斜杠来换行，例如。

你只能在此处指定一个 nameserver。然而，如果需要，你可以使用 kickstart 文件的 %post 部分（在第 H.3.22 节中描述）来添加更多 nameserver。

## 安装方法

下一个必填项是安装方法。该项指示安装程序获取安装 Red Hat Linux 所需其余文件的来源。有两个选择：NFS 或 CD-ROM。我们先从 NFS 开始，分别来看一下。

### nfs — NFS 安装方法

对于 NFS 安装方法，你必须包含 NFS 服务器的名称和要挂载的目录。以下是一个示例：

```
nfs -server hostname.of.server -dir
/path/to/RH/CD/image
```

### cdrom — CD-ROM 安装方法

## device — 可选硬件信息

kickstart 文件中的下一组项用于指定可选硬件信息。对于大多数基于 PCI 的硬件，你可以省略此步骤，因为这些信息可以直接从硬件获取。请注意，IDE 硬盘和常见的 PCI 卡都属于此类。任何其他硬件可能需要在此处指定。要指定一个设备，请以 device 关键字开头，后跟设备类型：

- ethernet（用于以太网卡）
- scsi（用于 SCSI 卡）
- cdrom（用于非 SCSI、非 IDE 的 CD-ROM 驱动器；通常是带专有 CD-ROM 接口的声卡）

如果需要内核模块来支持该设备，模块名称跟在设备类型之后。最后，如果设备需要任何参数，可以使用 --opts 选项指定。用引号将参数括在 --opts 之后。我们将在下面给出一些示例。请注意，你可以在一个 kickstart 文件中指定多个类型的设备。例如，如果你知道将进行 kickstart 安装的机器具有 Adaptec 1542 或 Buslogic SCSI 卡，你可以在 kickstart 文件中同时输入两者。但请注意，安装程序只使用找到的第一张卡，因此请适当排序设备条目。ISA 3com 以太网卡的示例为：

```
device ethernet 3c509 --opts "io=0x330, irq=7"
```

Adaptec 1542 SCSI 卡的示例行如下：

```
device scsi aha154x
```

SoundBlaster CD-ROM 的示例可能如下所示：

```
device cdrom --opts "io=0x240"
```

## keyboard — 键盘类型

接下来你需要指定的项目是键盘类型的正确代码。对于美国键盘，类型为 us。对于其他键盘，请在已安装的 Red Hat Linux 系统上运行 /usr/sbin/kbdconfig 程序。另一种方法是先将键盘类型设置为 us，并在安装完成后在已安装的系统上运行 kbdconfig 以正确设置它。示例为：

```
keyboard us
```

## noprobe

如果你不想让系统设备控制器被自动探测，则可以发出以下命令：

```
noprobe
```

配置此命令后，你的系统将不会探测任何设备控制器，SCSI 或其他类型均不探测。这仅在你希望手动指定系统上的设备时使用。

请注意：安装过程中不会在任何时候提示你输入设备。你必须手动将它们输入到 kickstart 配置文件中，否则将无法继续安装。

## device —continue

你的系统通常设置为获取或找到一种类型的设备一个。未作更改时，kickstart 配置将为一种类型的设备加载模块，例如为一种 SCSI 适配器类型加载模块。除此之外，程序将不会为该类型的设备加载更多模块。为了为超过 1 个适配器类型加载模块（例如，两个不同的 SCSI 适配器），你需要添加以下命令：

```
device --continue
```

因此，如果你需要为 Adaptec 和 BusLogic 适配器加载模块，

