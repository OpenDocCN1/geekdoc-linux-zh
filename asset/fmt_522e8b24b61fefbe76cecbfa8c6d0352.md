
# 将内核模块移植到 HummingBoard 平台

```c
#include <adxl34x.h> // #define ADXL34X_H_

#define READ(ac, reg) 	((ac)->bops->read((ac)->dev, reg))

#define WRITE(ac, reg, val) 	((ac)->bops->write((ac)->dev, reg, val))

static int gpio_nb;

static int irq;

struct axis_triple {

	int x;

	int y;

	int z;

};
```

/* 创建私有数据结构 */

```c
struct device *dev;
struct input_dev *input;
struct adxl345_platform_data pdata;
struct axis_triple swcal;
struct axis_triple hwcal;
struct axis_triple saved;
char phys[32];
bool fifo_delay;
int irq;
unsigned model;
unsigned int_mask;
const struct adxl345_bus_ops *bops;
};
```

/* 设置初始 adxl345 寄存器值 */

```c
static const struct adxl345_platform_data adxl345_default_init = {
	tap_threshold = 35,
	tap_duration = 3,
	tap_axis_control = ADXL_TAP_X_EN | ADXL_TAP_Y_EN | ADXL_TAP_Z_EN,
	tap_axis_control = ADXL_TAP_Z_EN,
	data_rate = 0,
	data_range = ADXL_FULL_RES,
	ev_type = EV_ABS, // 选择事件类型
	ev_code_x = ABS_X,
	ev_code_y = ABS_Y,
	ev_code_z = ABS_Z,
	ev_code_tap = {BTN_TOUCH, BTN_TOUCH, BTN_TOUCH},
	fifo_mode = FIFO_BYPASS,
	watermark = 0,
};
```

/* 获取 adxl345 数据 */

```c
static void adxl345_get_triple(struct adxl345 *ac, axis_triple *axis) {
    short buf[3];
    ac->bops->read_block(ac->dev, DATAX, 1, buf);
    ac->saved.x = (s32)buf[0];
    axis->x = ac->saved.x;
    ac->saved.y = (s32)buf[1];
    axis->y = ac->saved.y;
    ac->saved.z = (s32)buf[2];
    axis->z = ac->saved.z;
}
```

/* 当发生 DATA_READY 事件时，在 ISR（中断服务程序程序）内部调用此函数 */

```c
static void adxl345_service_fifo(struct adxl345 *ac) {
    struct adxl345_platform_data *pdata = &ac->pdata;
    axis_triple axis;
    adxl345_get_triple(ac, &axis);
    input_event(ac->input, pdata->ev_type, pdata->ev_code_x, axis->swcal.x);
    input_event(ac->input, pdata->ev_type, pdata->ev_code_y, axis->swcal.y);
    input_event(ac->input, pdata->ev_type, pdata->ev_code_z, axis->swcal.z);
}
```

/* 当发生 SINGLE TAP 事件时，在 ISR 中被 `adxl345_do_tap()` 调用。
 * 该函数检查 `ACT_TAP_STATUS` (0x2B) 的 `TAP_X`、`TAP_Y`、`TAP_Z` 位。
 * 如果轴涉及该事件，则生成 `EV_KEY` 事件。 */

```c
static void adxl345_send_events(struct adxl345 *ac, struct adxl345_platform_data *pdata, int status, int press) {
    int i;
    for (i = ADXL_Z_AXIS; i >= 0; i--) {
        if (status & (1 << (ADXL_Z_AXIS - i))) {
            input_report_key(ac->input, pdata->ev_code_tap[i], press);
        }
    }
}
```

/* 当发生 SINGLE_TAP 事件时在 ISR 中调用的函数 */

```c
static void adxl345_do_tap(struct adxl345 *ac, struct adxl345_platform_data *pdata, int status) {
    adxl345_send_events(ac, pdata, true);
    input_sync(ac->input);
    adxl345_send_events(ac, pdata, false);
}
```

/* 中断处理程序 */

```c
static irqreturn_t adxl345_irq(int irq, void *handle) {
    struct adxl345 *ac = handle;
    struct adxl345_platform_data *pdata = &ac->pdata;
    int int_stat, tap_stat, samples;
    /* 在清除中断前应读取 ACT_TAP_STATUS，以防 TAP 检测禁用 */
    pr_info("interrupt entered \n");
    /* 如果任何轴已启用，则读取 ACT_TAP_STATUS */
    if (pdata->tap_axis_control & (TAP_X_EN | TAP_Y_EN | TAP_Z_EN))
        tap_stat = AC_READ(ac, ACT_TAP_STATUS);
    else
        tap_stat = 0;
    /* 读取 INT_SOURCE (0x30) 寄存器。
     * 如果发生了 SINGLE_TAP 事件，则带 ACT_TAP_STATUS 寄存器参数调用 adxl345_do_tap 函数 */
    if (int_stat & (SINGLE_TAP)) {
        adxl345_do_tap(ac, pdata, tap_stat);
    }
    /* 检查是否发生了 DATA_READY 或 WATERMARK 事件。
     * 如果设置了这些事件中的任何一个，则生成 EV_ABS 事件 */
    if (int_stat & (DATA_READY | WATERMARK)) {
        if (pdata->fifo_mode)
            samples = ENTRIES(AC_READ(ac, FIFO_STATUS)) + 1;
        else
            samples = 1;
        // (剩余逻辑继续...)
    }
    return IRQ_HANDLED;
}
```
