
## 12. 定义一个 `spi_device_id` 数组：

```c
static const struct spi_device_id adxl345_id_id[] = {
    .name = "adxl345",
};
MODULE_DEVICE_TABLE(spi, adxl345_id_id);
```

## 13. 添加一个 `spi_driver` 结构体到 SPI 总线：

```c
static struct spi_driver adxl345_driver = {
    .driver = {
        .name = "adxl345",
        .owner = THIS_MODULE,
        .match_table = adxl345_dt_ids,
    },
    .probe = adxl345_spi_probe,
    .remove = adxl345_spi_remove,
    .id_table = adxl345_id_id;
};
```

## 14. 注册你的驱动 `module_spi_driver(adxl345_driver);`

## 15. 构建修改后的设备树并将其加载到目标处理器。参见 i.MXTD 处理器的 `adxl345_imx` 代码。注意：SAM (`adxl345_sam.c`) 和 BCM2837 (`adxl345_rpi.c`) 的驱动可以从本书的 GitHub 仓库下载。

# Listing 10-2: `adxl345_imx.c`

```c
#include <linux/input.h>
#include <linux/module.h>
#include <linux/spi/spi.h>
#include <linux/of_gpio.h>
#include <linux/spi/spi.h>
#include <linux/interrupt.h>
```

```c
#define ADXL345_CMD_MULTB (1 << 6)
#define ADXL345_CMD_READ
#define ADXL345_WRITCMD(reg) (reg & 0x3F)
#define ADXL345_CMD_READ(reg) (ADXL345_CMD_READ | (reg & 0x3F))
#define ADXL345_READMB_CMD(reg) (ADXL345_CMD_READ | ADXL345_CMD_MULTB | (reg & 0x3F))
```

```c
/* ADXL345 寄存器映射 */
#define DEVID 0x00 /* 设备 ID */
#define THRESH_TAP 0x1D /* R/W 击中阈值 */
#define DUR 0x21 /* R/W 持续时间 */
#define TAP_APES 0x2A /* R/W 击中控制 */
#define ACT_TAP_STATUS 0x2B /* 击中/双击状态 */
#define BW_RATE 0x2C /* R/W 速率控制 */
#define POWER_CTL 0x2D /* R/W 省电控制 */
#define INT_ENABLE 0x2E /* R/W 中断启用 */
#define INT_MAP 0x2F /* R/W 中断映射 */
#define INT_SOURCE 0x30 /* 中断源 */
```

```c
#define DATA_FORMAT    0x31/* R/W 数据格式控制 */
#define DATAX0         0x32/* X 轴数据 0 */
#define DATAX1         0x33/* X 轴数据 1 */
#define DATY0         0x34/* Y 轴数据 0 */
#define DATY1         0x35/* Y 轴数据 1 */
#define DATZ0         0x36/* Z 轴数据 0 */
#define DATZ1         0x37/* Z 轴数据 1 */
#define FIFO_CTL       0x38/* R/W FIFO 控制 */
```

```c
/* DEVID */
#define DEVID 0x00
/* INT_SOURCE */
#define INT_SOURCE 0x30
/* DATA_FORMAT */
#define DATA_FORMAT 0x31
/* POWER_CTL */
#define POWER_CTL 0x2D
/* BW_RATE */
#define BW_RATE 0x2C
/* FIFO_CTL */
#define FIFO_CTL 0x38
/* INT_MAP */
#define INT_MAP 0x2F
/* INT_ENABLE */
#define INT_ENABLE 0x2E
/* TAP_APES */
#define TAP_APES 0x2A
/* ACT_TAP_STATUS */
#define ACT_TAP_STATUS 0x2B
/* DUR */
#define DUR 0x21
/* THRESH_TAP */
#define THRESH_TAP 0x1D
/* DATAX0 */
#define DATAX0 0x32
/* DATAX1 */
#define DATAX1 0x33
/* DATY0 */
#define DATY0 0x34
/* DATY1 */
#define DATY1 0x35
/* DATZ0 */
#define DATZ0 0x36
/* DATZ1 */
#define DATZ1 0x37
/* ADXL345_CMD_MULTB */
#define ADXL345_CMD_MULTB (1 << 6)
/* ADXL345_CMD_READ */
#define ADXL345_CMD_READ
/* ADXL345_WRITCMD */
#define ADXL345_WRITCMD(reg) (reg & 0x3F)
/* ADXL345_CMD_READ */
#define ADXL345_CMD_READ(reg) (ADXL345_CMD_READ | (reg & 0x3F))
/* ADXL345_READMB_CMD */
#define ADXL345_READMB_CMD(reg) (ADXL345_CMD_READ | ADXL345_CMD_MULTB | (reg & 0x3F))
```

/*
* TAP_X/Y/Z Enable: 设置 TAP_X, Y, 或 Z Enable 将启用 X,
* Y, 或 Z 参与击中检测。设置为 '0' 将排除选定的
* 轴参与击中检测。
* 设置 SUPPRESS 位将在当在此期间存在大于 tap_threshold 
* 的加速度时，抑制双击检测。
*/

# 第 10 章

设备驱动的输入子系统框架

```c
/* 点击击延迟周期，即在第一次击击之后、第二个击击
 * 窗口打开之前。
 */
```

```c
#define ADXL_TAP_X_EN   (1 << 2)
#define ADXL_TAP_Y_EN   (1 << 1)
#define ADXL_TAP_Z_EN   (1 << 0)
```

`u8 tap_axis_control;`

```c/*
 * data_rate:
 * 选择带宽和输出数据率。
 * 速率 = 3200 / (2^(15 - x)). 默认值为 0xA，即 100 Hz
 * 输出数据率。应选择与所选通信协议和频率
 * 的输出数据率。在低通信速率下选择
 * 过高的输出数据率会导致样本被丢弃。
 */
```

`u8 data_rate;`

```c/*
 * data_range:
 * FULL_RES: 当设备设置此位时，设备处于
 * 高分辨率模式（In-Resolution Mode），此时输出分辨率
 * 随 RANGE 增加，以保持 4 mg/LSB 的比例因子。
 * 当此位清零时，设备处于 10 位模式，RANGE 决定
 * 最大的 g 范围和比例因子。
 */
```

```c
#define ADXL_RANGE_FULL_RES  (1 << 3)
#define ADXL_RANGE_PM_2g    0
#define ADXL_RANGE_PM_4g    1
#define ADXL_RANGE_PM_8g    2
#define ADXL_RANGE_PM_16g   3
```

`u8 data_range;`

```c/*
 * 有效的 BTN 或 KEY 代码；使用 tap_axis_control 禁用
 * 事件报告
 */
```
