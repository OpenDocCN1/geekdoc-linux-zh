
`apenvarr@foxnet.net`

```
标准内核中包含了用于设置跳线帽和通用提示的信息文件。
```

据设驱动程序也适用于`100Mbs Arcnet`卡！

## 5.8 AT&T

注意`AT&T`的`StarLan`是一项被弃的技术，类似于`SynOptics LattisNet`，如果没有同时“通话”两种语言的集线器，它无法在标准的`10Base-T`环境中使用。

### 5.8.1 AT&T T7231 (LanPACER+)

状态 - 不支持

这些`StarLan`卡使用类似于`i82586`芯片的接口。曾经，Matthijs Melchior (`matthijs.n.melchior@att.com`) 正在尝试`3c507`驱动，并几乎做出了可用的效果。之后就没怎么消息了。

## 5.9 AT-Lan-Tec / RealTek

### 5.9.1 AT-Lan-Tec / RealTek Pocket适配器

状态 - 支持

这是一种由`AT-Lan-Tec`以及（可能还有）其他供应商销售的通用低成本`OEM`口袋适配器。标准内核中包含了它的驱动程序。注意驱动源文件`atpc.c`中包含大量信息。

请注意，此设备传递给`ifconfig`的设备名称不是`eth0`而是`atp0`。

### 5.9.2 RealTek 8029

状态 - 支持

这是`NE2000`克隆的`PCI`单芯片实现。现在许多供应商都在销售带有这种芯片的卡。请参考`52.26.2` (`NE2000-PCI`) 获取有关使用任何此类卡的信息。

### 5.9.3 RealTek 8129/8139

状态 - 半支持

来自`RealTek`的另一个`PCI`单芯片以太网解决方案。基于此芯片的卡驱动程序将包含在`linux v2.0.34`版本中。更多信息，请参阅：

```
http://cesdisis.gsfc.nasa.gov/linux/drivers/rt18139.html
```
