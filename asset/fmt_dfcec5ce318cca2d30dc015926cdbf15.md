
你也可以通过 `-id` 将 `xev` 扩展到窗口 ID（使用从 `xwinfo` 获取的 id 作为 id）或使用 `-root` 根窗口。

### 14.3.2 理解 X 输入和偏好设置

X 最令人困惑的特征之一是，设置偏好通常有多种方法，且方法可能无效。例如，Linux 系统上常见的键盘偏好是重新映射

将 `Caps Lock` 键更改为 `Control` 键有多种方法可以实现，从使用旧的 `xmodmap` 命令进行微调，到使用 `setxkb` 工具提供完全全新的键盘映射。你如何知道应该使用哪一种（如果有的话）呢？这取决于你系统中哪些部分负责该功能，但确定这一点可能困难。请记住，桌面环境可能会提供自己的设置和覆盖。

话虽如此，关于底层基础设施有一些建议。

## 输入设备（通用）

X 服务器使用输入扩展（Input Extension）来管理来自许多不同设备的输入。输入设备有两种基本类型——键盘和指针，你可以连接尽可能数量的设备。为了同时使用多个相同类型的设备，X 输入扩展创建了一个“虚拟核心”，将输入汇聚到 X 服务器中。核心设备被称为主设备（master），你插入的物理设备成为从设备（slave）。

要查看你机器上的设备配置，请尝试运行：

```
$ xinput --list

Virtual core pointer      id=2 master pointer ([3])

Virtual XTEST pointer     id=4 slave pointer ([2])

Logitech Unifying Device id=8 slave pointer ([2])

Virtual core keyboard    id=3 master keyboard ([2])

Virtual XTEST keyboard id=5 slave keyboard ([3])

Power Button             id=6 slave keyboard ([3])

Power Button             id=7 slave keyboard ([3])

Cypress USB Keyboard id=9 slave keyboard ([3])
```

每个设备都有一个关联的 ID，你可以配合 `xinput` 和其他命令使用。在此输出中，ID 2 和 3 是核心设备，ID 8 和 9 是真实设备。注意，机器上的电源按钮也被视为 X 输入设备。

大多数 X 客户端都监听来自核心设备的输入，因为没有理由去担心事件源自哪一个特定设备。然而，大多数客户端对 X 输入扩展一无所知。

每个设备都有一组关联属性。要查看这些属性，请使用设备编号配合 `xinput`，例如：

```
$ xinput --list-props 8

Device 'Logitech Unifying Device. Wireless PID:4026':

Device Enabled (126): 1

  Coordinate Matrix (128): 1.000000, 0.000000, 0.000000,

  0.000000, 0.000000, 0.000000, 1.000000

  Device Accel Profile (256): 0

  Device Accel Constant Acceleration (257): 1.000000

  Device Accel Adaptive Acceleration (258): 1.000000

  Device Accel Velocity Scaling (259): 10.000000

--snip--
```

如你所见，有很多有趣的属性可以通过 `--set-prop` 更改（更多信息请参阅 `input(1)` 手页）。

## 鼠标

你可以通过 `input` 命令操作设备相关的设置，其中许多实用的适用于鼠标（指针）。你可以直接作为属性更改许多设置，但通常使用 `input` 专用的 `--set-pt-feedback` 和 `--set-button-map` 选项更简单。例如，如果你在 `dev` 上有一个三键鼠标，并想要反转按钮顺序（这对于左手用户非常方便），可以这样做：

```
$ xinput --set-button-map dev 3 2 1
```
