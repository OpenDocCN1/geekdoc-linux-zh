
## 代码片段

```c
.id_table = network_driver_pci_table,	/* See above */

/* suspend() and resume() methods that implement power

   management are not used by this driver */

};

/* Ethernet driver initialization */

static int __init

network_driver_init(void)

{

  pci_register_driver(&network_pci_driver);

  return 0;

}

/* Ethernet driver exit */

static void __exit

network_driver_exit(void)

{

  pci_unregister_driver(&network_pci_driver);

}

module_init(network_driver_init);

module_exit(network_driver_exit);

MODULE_DEVICE_TABLE(pci, network_driver_pci_table);
```

## 列表 10.2. 注册调制解调器功能

```c
#include <linux/pci.h>

#define MY_VENDOR_ID		0xABCD
#define MY_DEVICE_ID_MDM	0xEF02

/* The set of PCI cards that this driver supports */
struct pci_device_id modem_driver_pci_table[] __devinitdata = {
{	MY_VENDOR_ID,			/* Interface chip manufacturer ID */
	MY_DEVICE_ID_MDM,			/* Device ID for the modem
				function */
	PCI_ANY_ID,			/* Subvendor ID wild card */
	PCI_ANY_ID,			/* Subdevice ID wild card */
	0, 0,				/* Class and classmask are
				unspecified */
	modem_driver_private_data	/* Use this to co-relate
			configuration information if the driver
			supports multiple cards. Can be an
			enumerated type. */
}, {0},
};

struct pci_driver modem_pci_driver = {
.name		= "mdm",				/* Unique name */
.probe		= modem_driver_probe,	/* See Listing 10.4 */
.remove	= __devexit_p(modem_driver_remove);/* See Listing 10.4 */
.id_table	= modem_driver_pci_table,	/* See above */
/* suspend() and resume() methods that implement power
management are not used by this driver */
};

/* Modem driver initialization */
static int __init

modem_driver_init(void)

{
	pci_register_driver(&modem_pci_driver);
	return 0;
}

/* Modem driver exit */
static void __exit

modem_driver_exit(void)

{
	pci_unregister_driver(&modem_pci_driver);
}

module_init(modem_driver_init);
module_exit(modem_driver_exit);

MODULE_DEVICE_TABLE(pci, modem_driver_pci_table);
```

列表 10.3 实现了网络功能的 `probe()` 方法。该方法：

- 启用 PCI 设备
- 发现资源信息，例如 I/O 基地址和 IRQ
- 分配并填充与该设备关联的网络数据结构
- 向内核网络层注册自己

列表 10.4 为调制解调器功能执行类似的工作。在这种情况下，驱动程序向内核串行层而不是网络层注册。

列表 10.3 和 10.4 还实现了 `remove()` 方法，这些方法在 CardBus 卡被弹出或驱动程序模块被卸载时调用。`remove()` 是 `probe()` 的反向操作；它释放资源，并从相关子系统中注销驱动程序。列表 10.1 中用于声明 `remove()` 方法的 `__devexit_p()` 宏会在编译时丢弃提供的函数，前提是你没有启用热插拔支持，且该驱动程序不是可动态加载的模块。

PCI 子系统调用 `probe()` 时带有两个参数：

1. 指向 `pci_dev` 的指针，该数据结构描述此 PCI 设备。该结构体定义在 `include/linux/pci.h` 中，由 PCI 子系统为系统中的每个 PCI 设备维护。
2. 指向 `pci_device_id` 的指针，这是驱动程序 `pci_device_id` 表中的条目，与插入卡配置空间中发现的信息相匹配。

## 列表 10.3. 探测网络功能

```c
#include <linux/pci.h>

unsigned long ioaddr;

/* Probe method */
static int __devinit

net_driver_probe(struct pci_dev *pdev,
const struct pci_device_id *id)
{

/* The net_device structure is defined in include/linux/netdevice.h.
See Chapter 15, "Network Interface Cards", for the description */
struct net_device *net_dev;

/* Ask low-level PCI code to enable I/O and memory regions for
this device. Look up the IRQ for the device that the PCI
subsystem allotted when it walked the bus */
pci_enable_device(pdev);

/* Use this device in bus mastering mode, since the network
function of this card is capable of DMA */
pci_set_master(pdev);

/* Allocate an Ethernet interface and fill in generic values in
the net_dev structure. prv_data is the private driver data
structure that contains buffers, locks, and so on. This is
left undefined. Wait until Chapter 15 for more on
alloc_etherdev() */
net_dev = alloc_etherdev(sizeof(struct prv_data));

/* Populate net_dev with your network device driver methods */
net_dev->hard_start_xmit = &mydevice_xmit; /* See Listing 10.6 */

/* More net_dev initializations */
/* ... */

/* Get the I/O address for this PCI region. All card registers
specified in Table 10.3 are assumed to be in bar 0 */
ioaddr = pci_resource_start(pdev, 0);

/* Claim a 128-byte I/O region */
request_region(ioaddr, 128, "ntwrk");

/* Fill in resource information obtained from the PCI layer */
```
