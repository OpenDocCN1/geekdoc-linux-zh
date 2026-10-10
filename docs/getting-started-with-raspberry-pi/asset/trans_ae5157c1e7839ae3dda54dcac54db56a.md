
| 功能 | 目的 |
| --- | --- |
| `i2c_smbus_read_block_data()` | 从指定偏移读取一块数据。 |
| `i2c_smbus_write_block_data()` | 向指定偏移发送一块数据（<= 32 字节）。 |

## 总线事务

在实现示例驱动程序之前，让我们通过“放大镜”观察一下线缆，以便更好地理解 I²C 协议。**列表 8.1** 展示了一段与 I²C EEPROM 通信的代码片段，以及总线上发生的相应事务。这些事务是通过在运行代码片段时连接 I²C 总线分析仪捕获的。代码使用了用户模式 I²C 函数。（我们在第 19 章“用户空间驱动程序”中更详细地讨论用户模式 I²C 编程。）

### 列表 8.1. I²C 总线上的事务

```c
/* ... */
/*
 * Connect to the EEPROM. 0x50 is the device address.
 * smbus_fp is a file pointer into the SMBus device.
 */
ioctl(smbus_fp, 0x50, slave);

/* Write a byte (0xAB) at memory offset 0 on the EEPROM */
i2c_smbus_write_byte_data(smbus_fp, 0, 0xAB);

/*
 * This is the corresponding transaction observed
 * on the bus after the write:
 * S 0x50 Wr [A] 0 [A] 0xAB [A] P
 *
 * S is the start bit, 0x50 is the 7-bit slave address (0101000b),
 * Wr is the write command (0b), A is the Accept bit (or
 * acknowledgment) received by the host from the slave, 0 is the
 * address offset on the slave device where the byte is to be
 * written, 0xAB is the data to be written, and P is the stop bit.
 * The data enclosed within [] is sent from the slave to the
 * host, while the rest of the bits are sent by the host to the
 * slave.
 */
/* Read a byte from offset 0 on the EEPROM */
res = i2c_smbus_read_byte_data(smbus_fp, 0);

/*
 * This is the corresponding transaction observed
 * on the bus after the read:
 * S 0x50 Rd [A] 0 [A] S 0x50 Rd [A] [0xAB] NA P
 *
 * The explanation of the bits is the same as before, except that
 * Rd stands for the Read command (1b), 0xAB is the data received
 * from the slave, and NA is the Reverse Accept bit (or the
 * acknowledgment sent by the host to the slave).
 */
```

## 设备示例：EEPROM

我们的第一个示例客户端设备是一个位于 I²C 总线上的 EEPROM，如图 8.1 所示。几乎所有笔记本电脑和台式机都拥有这样的 EEPROM，用于存储 BIOS 配置信息。示例 EEPROM 有两个存储库。驱动程序为每个存储库导出 `/dev/interfaces` 节点：`/dev/eep/0` 和 `/dev/eep/1`。应用程序通过操作这些节点与 EEPROM 交换数据。

每个 I²C/SMBus 客户端设备都被分配一个从机地址，用作设备标识符。示例中的 EEPROM 响应两个从机地址：`SLAVE_ADDR1` 和 `SLAVE_ADDR2`，每个存储库对应一个。

示例驱动程序使用与 SMBus 兼容的 I²C 命令，因此适用于 I²C 和 SMBus EEPROM。

### 初始化

与所有驱动类一样，I²C 客户端驱动程序也拥有 `init()` 入口点。初始化包括分配数据结构、向 I²C 核心注册驱动程序，以及与 sysfs 和 Linux 设备模型进行关联。这在列表 8.2 中完成。

#### 列表 8.2：初始化 EEPROM 驱动程序

```cpp
/* Driver entry points */
static struct file_operations eep_fops = {
    .owner    = THIS_MODULE,
    .llseek   = eep_llseek,
    .read     = eep_read,
    .ioctl    = eep_ioctl,
    .open     = eep_open,
    .release  = eep_release,
    .write    = eep_write,
};

static dev_t dev_number;            /* Alotted Device Number */
static struct class *eep_class;     /* Device class */

/* Per-device client data structure for each
 * memory bank supported by the driver
 */

struct eep_bank {
    struct i2c_client *client;      /* I²C client for this bank */
    unsigned int addr;             /* Slave address of this bank */
    signed short current_pointer;  /* File pointer */
    int bank_number;               /* Actual memory bank number */
    /* ... */                      /* Spinlocks, data cache for
                                     slow devices,... */
};

#define NUM_BANKS 2               /* Two supported banks */
#define BANK_SIZE 2048            /* Size of each bank */
struct ee_bank *ee_bank_list;      /* List of private data
                                    structures, one per bank */
```

```c
/*
 * Device Initialization
 */
int __init
eep_init(void)
{
  int err, i;

  /* Allocate the per-device data structure, ee_bank */
  ee_bank_list = kmalloc(sizeof(struct ee_bank)*NUM_BANKS,
                         GFP_KERNEL);
  memset(ee_bank_list, 0, sizeof(struct ee_bank)*NUM_BANKS);
  /* Register and create the /dev interfaces to access the EEPROM
     banks.  Refer back to Chapter 5, "Character Drivers" for
     more details */
  if (alloc_chrdev_region(&dev_number, 0,
                          NUM_BANKS, "eep") < 0) {
    printk(KERN_DEBUG "Can't register device\n");
    return -1;
  }

  eep_class = class_create(THIS_MODULE, DEVICE_NAME);
  for (i=0; i < NUM_BANKS; i++) {

    /* Connect the file operations with cdev */
    cdev_init(&ee_bank[i].cdev, &eep_fops);

    /* Connect the major/minor number to the cdev */
    if (cdev_add(&ee_bank[i].cdev, (dev_number + i), 1)) {
      printk("Bad kmalloc\n");
      return 1;
    }
    class_device_create(eep_class, NULL, (dev_number + i),
                        NULL, "eeeprom%d", i);
  }
  /* Inform the I2C core about our existence.  See the section
     "Probing the Device" for the definition of eep_driver */
  err = i2c_add_driver(&eep_driver);

  if (err) {
    printk("Registering I2C driver failed, errno is %d\n", err);
    return err;
  }

  printk("EEPROM Driver Initialized.\n");
  return 0;
}
```

列表 8.2 启动了设备节点的创建，但为了完成它们的生成，需要在 `/etc/udev/rules.d/` 下的适当规则文件中添加以下内容：

当接收到来自内核的相应事件时，这将创建 `/dev/eep/0` 和 `/dev/eep/1`。需要读取第 $n^{\mathrm{th}}$ 个存储库的用户模式程序随后可以操作 `/dev/eep/n`。

列表 8.3 实现了 EEPROM 驱动程序的 `open()` 方法。当应用程序打开 `/dev/eep/X` 时，内核会调用 `eep_open()`。`eep_open()` 将在私有区域存储每个设备的数据结构，以便驱动程序的其余方法可以直接访问它。

#### 列表 8.3. 打开 EEPROM 驱动程序

```c
int
eep_open(struct inode *inode, struct file *file)
{
  /* The EEPROM bank to be opened */
  n = MINOR(file->f_dentry->d_inode->i_rdev);
  file->private_data = (struct ee_bank *)ee_bank_list[n];

  /* Initialize the fields in ee_bank_list[n] such as
  size, slave address, and the current file pointer */

  /* ... */
}
```

### 探测设备

I²C 客户端驱动程序与主机控制器驱动程序和 I²C 核心合作，按照以下方式将自己附加到从机设备：

1. 在初始化期间，它注册了一个 `probe()` 方法，当检测到相关的主机控制器时，I²C 核心会调用该方法。在列表 8.2 中，`eep_init()` 通过调用 `i2c_add_driver()` 注册了 `eep_probe()`：

   ```c
   static struct i2c_driver eep_driver =
   {
       .driver = {
           .name = "EEP", /* Name */
       },
       .id = I2C_DRIVERID_EEP, /* ID */
       .attach_adapter = eep_probe, /* Probe Method */
       .detach_client = eep_detach, /* Detach Method */
   };
   i2c_add_driver(&eep_driver);
   ```

   驱动程序标识符 `I2C_DRIVERID_EEP` 对于该设备应该是唯一的，并且应定义在 `include/linux/i2c-id.h` 中。

2. 当核心调用驱动程序的 `probe()` 方法表示存在主机适配器时，它反过来调用 `i2c_probe()`，其参数指定了驱动程序负责的从机设备的地址以及相关的 `attach()` 例程。

列表 8.4 实现了 `eep_probe()`，即 EEPROM 驱动程序的 `probe()` 方法。`normal_i2c` 指定 EEPROM 存储库地址，并作为 `i2c_client_address_data` 结构的一部分填充。该结构中的其他字段可用于请求更精细的地址控制。你可以使用 `ignore` 字段要求 I²C 核心忽略一定范围的地址。或者，你可以使用 `probe` 字段指定 `(adapter, slave address)` 对，如果你希望将某个从机地址绑定到特定的主机适配器。例如，如果你的处理器支持两个 I²C 主机适配器，而你在总线 1 上有一个 EEPROM，在总线 2 上有一个温度传感器，两者响应相同的从机地址，这将很有用。

3. 主机控制器遍历总线，寻找第 2 步中指定的从机设备。为此，它生成一个总线事务，例如 `S SLAVE_ADDR Wr`，其中 `S` 是起始位，`SLAVE_ADDR` 是设备数据手册中指定的相关 7 位从机地址，`Wr` 是写命令，如“总线事务”部分所述。如果总线上存在可用的从机设备，它将通过发送确认位（`[A]`）进行响应。

4. 如果主机适配器在第 3 步中检测到从机，I²C 核心将调用通过 `i2c_probe()` 在第二步中提供的第三个参数传递的 `attach()` 例程。对于 EEPROM 驱动程序，这个例程是 `eep_attach()`，它注册每个设备的客户端数据结构，如列表 8.5 所示。如果你的设备期望有一个初始编程序列（例如，I²C 数字视频接口传输芯片上的寄存器在芯片开始工作前必须初始化），请在这个例程中执行这些操作。

#### 列表 8.4. 探测 EEPROM 存储库的存在

```c
#include <linux/i2c.h>

/* The EEPROM has two memory banks having addresses SLAVE_ADDR1
 * and SLAVE_ADDR2, respectively
 */
static unsigned short normal_i2c[] = {
    SLAVE_ADDR1, SLAVE_ADDR2, I2C_CLIENT_END
};

static struct i2c_client_address_data addr_data = {
    .normal_i2c = normal_i2c,
    .probe      = ignore,
    .ignore     = ignore,
    .forces     = ignore,
};

static int
eep_probe(struct i2c_adapter *adapter)
{
  /* The callback function eep_attach(), is shown
   * in Listing 8.5
   */
  return i2c_probe(adapter, &addr_data, eep_attach);
}
```

#### 列表 8.5. 附加客户端

