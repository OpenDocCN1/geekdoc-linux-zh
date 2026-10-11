
```c
static int ioaccel_probe(struct i2c_client *client,
                    struct i2c_device_id *id) {
    /* 声明私有结构实例 */
    struct ioaccel_dev *ioaccel;

    dev_info("ioaccel_probe is called.\n");

    /* 为新设备分配私有结构 */
    ioaccel = devm_kzalloc(&client->dev, sizeof(struct ioaccel_dev), GFP_KERNEL);
    dev_info(&client->dev, "ioaccel_probe\n");

    /* 将 client-dev 与 ioaccel 私有结构关联 */
    i2c_set_client_data(client, ioaccel);
    i2c_smbus_write_byte(client, CTRL_REG1, CTRL_REG1_ACTIVE);

    /* 分配 struct input_polled_dev */
    ioaccel->polled_input = input_allocate_polled_device();

    /* 初始化 input */
    ioaccel->polled_input->client = ioaccel;
    ioaccel->polled_input->private = ioaccel;
    ioaccel->polled_input->poll_interval = 50;
    ioaccel->polled_input->poll = ioaccel_poll;
    ioaccel->polled_input->output = ioaccel_open;
    ioaccel->polled_input->input->dev = &client->dev;
    ioaccel->polled_input->input->name = "IOACCEL";
    ioaccel->polled_input->input->id.bustype = BUS_I2C;

    /* 设置事件类型 */
    set_bit(EV_KEY, ioaccel->polled_input->input->evbit);
    set_bit(KEY_1, ioaccel->polled_input->input->keybit);
    set_bit(KEY_2, ioaccel->polled_input->input->keybit);

    /* 注册设备，现在设备在注销前是全局的 */
    input_register_polled_device(ioaccel->polled_input);
    return 0;
}
```

```c
static int ioaccel_remove(struct i2c_client *client) {
    struct ioaccel_dev *ioaccel;
    ioaccel = i2c_get_client_data(client);
    input_unregister_polled_device(ioaccel->polled_input);
    input_free_polled_device(ioaccel->polled_input);
    devm_kfree(&client->dev, ioaccel);
    dev_info(&client->dev, "ioaccel_remove\n");
    return 0;
}
```

```c
/* 向设备树添加项 */
static const struct of_device_id ioaccel_dt_ids[] = {
    { .compatible = "arrow,mma8451" },
};
MODULE_DEVICE_TABLE(of, ioaccel_dt_ids);

static const struct i2c_device_id i2c_ids[] = {
    { .name = "mma8451" },
};
MODULE_DEVICE_TABLE(i2c, i2c_ids);

/* 创建 struct i2c_driver */
static struct i2c_driver ioaccel_driver = {
  .driver = {
    .name = "mma8451",
    .owner = THIS_MODULE,
    .of_match_table = ioaccel_dt_ids,
  },
  .probe = ioaccel_probe,
  .remove = ioaccel_remove,
  .id_table = i2c_ids,
};
/* 注册 i2c 总线 */
module_i2c_driver(ioaccel_driver);
```

## i2c_accel.ko 演示

打开 minicom 并启动。按下 RESET 键开始序列。按任意键停止 U-Boot 序列，然后使用 `run netboot` 命令进行网络启动。

```
U-Boot > run netboot  /* 开始网络启动 */
```

使用 `i2c-utils` 工具包与传感器交互（加载模块之前）

`i2cdetect` 是 `i2c-utils` 工具包中的一个工具。它可以从用户空间探测 i2c 总线并报告正在使用的地址

```
root@im6qsabres:~# i2cdetect -l /* 列出可用总线，加速度计在总线 0 */
```

| I2C-0 | 21a0000.i2c | I2C 适配器 |

| I2C-1 | 21a40000.i2c | I2C 适配器 |

| I2C-2 | 21a80000.i2c | I2C 适配器 |

```c
root@im6qsabres:~# i2cdetect -F 0 /* 总线 0 的功能 */
```

| /dev/i2c-0 实现的功能: | |

| :--- | :--- |

| I2C | |

| SMBus Quick Command | yes |

| SMBus Send Byte | yes |

| SMBus Receive Byte | yes |

| SMBus Write Byte | yes |

| SMBus Read Byte | yes |

| SMBus Write Word | yes |

| SMBus Read Word | yes |

| SMBus Process Call | yes |

| SMBus Data Write | yes |

| SMBus Block Read | no |

| SMBus Block Process Call | no |

| SMBus PEC | yes |

| I2C Block Write | yes |

| I2C Block Read | yes |

"`i2cdetect` 在 i2c 总线 #0 上发现了三个正在使用的地址：0x1c、0x4a 和 Oxla。Oxla 地址标记为正在使用（UU 字符）。这是该组件实际上已被 Linux 设备驱动程序占用并附加的标志。如果你检查 `imx6qdi-sabre.dtsi` 文件，可以看到该地址对应于 `wm8962` 音解码器"

## 第 9 章

`root@imx6qsabres:~# i2cdetect -y 0` /* 查看检测到的设备，查看 "1c" 加速度计地址 */

```
  0 1 2 3 4 5 6 7 8 9 a b c d e f
00:
10:                               uu1c
20:
30:
40:                               4a
50:
60:
70:
```

（注：上方文本已针对 OCR 错误进行修正）

“使用 imx6qsabres：通过 `i2cget` 和 `i2cset` 与 `mma8451` 加速度计交互”

```
root@imx6qsabres:~# i2cget -y 0 0x1c 0x2a /* 读取 0x2a 地址。如果返回 01，则加速度计处于激活状态 */
root@imx6qsabres:~# i2cset -y 0 0x1c 0x2a 01 /* 如果上一个命令返回 00，则使用 i2cset 设置加速度计 */
root@imx6qsabres:~# while true; do i2cget -y 0 0x1c 0x01; do /* 你可以看到 OUT X MSB 寄存器的值。0x01 值对应 OUT X MSB 寄存器地址。你可以移动 SABRE 板并观察 OUT X MSB 寄存器值的变化。设置不同的值范围来生成事件。这些范围的值将被写入 ioaccel_poll() 中 */
```
