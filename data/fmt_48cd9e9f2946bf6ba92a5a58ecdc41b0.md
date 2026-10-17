
### 编译与部署步骤

- 在 `linux_5.4_rpi_drivers` 中创建一个新的 `CY8C950A_rpi3.c` 文件和一个 `Makefile` 文件，并将 `CY8C950A_rpi3.o` 添加到你的 Makefile 变量中，然后编译并将模块部署到树莓派：

  `~/linux_5.4_rpi_drivers/linux_5.4_CY8C950A_driver$ make`

  `~/linux_5.4_rpi_drivers/linux_5.4_CY8C950A_driver$ make`

- 编译修改后的设备树并加载到目标处理器：

  `~/linux_rpi3/linux$ make=arm CROSS_COMPILE=arm-linux-gnueabihf arch/arm/dtts/bcm2710-rpi-3.dt`

- 重启树莓派：

  `root@raspberrypi:/home# reboot`

### 列表 7-4: `CY8C950A_rpi3.c`

```c
#include <i2c.h>
#include <linux/interrupt.h>
#include <linux/irq.h>
#include <linux/gpio/driver.h>
#include <linux/kernel.h>
#include <linux/module.h>
#include <linux/slab.h>

#define DRV_NAME"cy8c950a"

/* cy8c950a 设置 */
#define GPIO                   20
#define DEVID_CYC950A        0x20
#define NPORTS                 3

/* 寄存器偏移量 */
#define REG_INPUT_PORT0         0x00
#define REG_OUTPUT_PORT0        0x08
#define REG_INTR_STAT_PORT0     0x10
#define REG_PORT_SELECT        0x18
#define REG_SELECT_Pwm         0x1a
#define REG_INTR_MASK          0x19
#define REG_PIN_DIR            0x1c
#define REG_DRIVE_PUP         0x1d
#define REG_DRIVE_OWN          0x1e
#define REG_DEV_STAT           0x2e

/* 驱动程序的全局结构体定义 */
struct cy8c950a {
	struct i2c_client *client;
	struct gpio_chip gpio_chip;
	struct gpio_desc *gpio;
	int irq;
	struct mutex lock;
	/* 中断控制器序列化访问 */
	struct mutex irq_lock;
	/* 缓存的输出寄存器 */
	u8 outreg_cache[NPORTS];
	/* 缓存的 irq_mask[NPORTS]; */
	/* 应用的 IRQ 掩码 */
	u8 irq_mask[NPORTS];
};

/* 端口 GPIO 偏移量 */
static const u8 cy8c950a_port_ffs[] = {
	0,
	8,
	16,
};
```

```c
/* 返回 gpio 的端口 cypress_get_port(unsigned int) */

static inline u8 cypress_get_port(unsigned int gpio)

{

    u8 i = 0;

    for (i = 0; i < sizeof(cy8c950a_port_ffs) - 1; i++) {

        if (!(gpio / cy8c950a_port_ffs[i + 1])) {

            break;

        }

    }

    return i;

}

/* 获取对应端口内的 gpio 偏移量 */

static inline u8 cypress_get_offs(unsigned int gpio, u8 port)

{

    return gpio - cy8c950a_port_ffs[port];

/* struct gpio_chip get 回调函数。

 * 它获取 GPIO 线的值 (0=low, 1=high)

 * 访问 REG_INPUT_PORT 寄存器

 */

static int cy8c9520a_gpio_get(struct gpio_chip *chip, unsigned int gpio)

{

    int ret;

    u8 port, in_reg;

    struct cy8c950a *cygpio = gpiochip_get_data(chip);

    dev_info(chip->parent, "cy8c950a_gpio_function is called\n");

    /* 获取 GPIO 的输入端口地址 (in_reg) */

    port = cypress_get_port(cygpio);

    in_reg = REG_INPUT_PORT0 + port;

    dev_info(chip->parent, "the in_reg address is %u\n", in_reg);

    mutex_lock(&cygpio->lock);

    ret = i2c_smbus_read_byte(cygpio->client, in_reg);

    if (ret < 0) {

        dev_err(chip->parent, "can't read input port %u\n", in_reg);

    }

    dev_info(chip->parent, "cy8c950a_gpio_function with %d value is returned\n", ret);

    mutex_unlock(&cygpio->lock);

/* 检查输入端口中 GPIO 的状态

 * 并返回。如果表达式为 0 则返回 1

 */

    return !!(ret & cypress_get_offs(gpio, port));

}
```
