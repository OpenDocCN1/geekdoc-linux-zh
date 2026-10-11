
```
root@imx7dsabres:/sys/bus/iio/devices/device:2# cat in_accel_scale /* 读取加速度计比例因子 */
```

"Sysfs trigger interface"

```
root@imx7dsabres:/sys/bus/iio/devices/device:2# ls /* 查看创建的 iio_sysfs_trigger 文件夹 */
iio:device0 iio:device1 iio:device2
iio_sysfs_trigger
```

```
root@imx7dsabres:/sys/bus/iio/devices/device:2# echo 1 > iio_sysfs_trigger/add_trigger /* 创建一个 sysfs 触发器 */
root@imx7dsabres:/sys/bus/iio/devices/device:2# ls /* 查看触发器 */
iio:device0 iio:device1 iio:device2 iio_sysfs_trigger
```

```
root@imx7dsabres:/sys/bus/iio/devices/device:2# echo trigger0 > iio:device2/trigger/current_trigger /* 将触发器附加到 iio 设备 */
```

```
root@imx7dsabres:/sys/bus/iio/devices/device:2# echo 1 > iio:device2/scan_elements/in_accel_x_raw /* 开启 x 扫描 */
root@imx7dsabres:/sys/bus/iio/devices/device:2# echo 1 > iio:device2/scan_elements/in_accel_y_raw /* 开启 y 扫描 */
```

```
root@imx7dsabres:/sys/bus/iio/devices/device:2# echo 1 > iio:device2/scan_elements/in_timestamp /* 开启时间戳扫描 */
```

```
root@imx7dsabres:/sys/bus/iio/devices/device:2# echo 100 > iio:device2/buffer/length /* 设置缓冲区可持有的样本数量 */
root@imx7dsabres:/sys/bus/iio/devices/device:2# echo 1 > iio:device2/buffer/enable /* 开启缓冲区 */
```

```
root@imx7dsabres:/sys/bus/iio/devices/device:2# echo 1 > trigger0/now /* 执行数据采集 */
root@imx7dsabres:/sys/bus/iio/devices/device:2# echo 1 > trigger0/now /* 执行数据采集 */
root@imx7dsabres:/sys/bus/iio/devices/device:2# hexdump -v -e '16 "%02x" "\n"' < /dev/iio:device2/* 显示获取的值：轴数据 + 时间戳 */
```

```
ff ff ff f0 00 00 a8 47 52 12 21 be 26 fc ff
ff ff ff ff f1 04 00 a8 10 4f 91 93 bc 64 fc
```

```
root@imx7dsabres:/sys/bus/iio/devices/device:2# echo 0 > iio:device2/buffer/enable /* 关闭缓冲区 */
root@imx7dsabres:/sys/bus/iio/devices/device:2# echo "" > iio:device2/trigger/current_trigger /* 移除触发器 */
```

```
root@imx7dsabres:~ rrmod adxl345_imix_io /* 移除模块 */
```

再次启动你的目标系统。使用 `iio_generic_buffer` 应用程序设置

# 第 12 章

# 在 Linux 驱动程序中使用 Regmap API

## 在 Linux 设备驱动程序中使用 Regmap API

缓冲区长度和采集次数，启用扫描元素并显示采集到的值

```bash
root@imx7adsabres:# insmod adx1345_imx_iio.ko /*加载模块 */
```

```bash
/* 创建 sysfs 触发器 */
root@imx7adsabres:# echo 1 /sys/bus/io/devices/iio_sysfs_trigger/add_trigger
root@imx7adsabres:# echo 1 /sys/bus/io/devices/iio:device1/sysstrig /sys/bus/io/devices/iio:device2/current_trigger /* 将触发器附加到设备 */
```

```bash
root@imx7adsabres:# ./iio_generic_buffer --device-num 2 -T O -a 1l 10 -c 5 & /* 启动 iio_generic_buffer 应用 */
```

```bash
[1] 600
root@imx7adsabres:~#使用的 iio 设备编号为 2
使用的 iio 触发器编号为 0
```

未启用通道，启用所有通道

启用: in_accel_y_en

启用: in_accel_x_en

启用: in_timestamp_en

启用: in_accel_z_en

`/sys/bus/io/devices/iio:device2/systrigger1`

```bash
root@imx7adsabres:# echo 1 /sys/bus/io/devices/trigger0/trigger_now /* 执行第一次采集，可以进行 5 次转换 */
0.033800 -0.532600 9.268600 151654248322659500
```

```bash
root@imx7adsabres:# echo 1 /sys/bus/io/devices/trigger0/trigger_now /* 执行第二次采集 */
0.229800 0.153200 -9.919700 1510654243356220000
```

```bash
root@imx7adsabres:# echo 1 /sys/bus/io/devices/iio:device2/buffer/enable /* 禁用缓冲区 */
root@imx7adsabres:# echo 1 /sys/bus/io/devices/iio:device2/trigger/current_trigger /* 分离触发器 */
```

```bash
root@imx7adsabres:# rmmod adx1345_imx_iio.ko /* 移除模块 */
```

使用 hrtimer 现在进行采集。重启你的目标系统

```bash
root@imx7adsabres:# insmod adx1345_imx_iio.ko /* 加载模块 */
root@imx7adsabres:# mkdir /config /* 创建配置文件 */
root@imx7adsabres:# mount -t configs /config /* 挂载 configs 文件系统 */
/config/triggers/hrtimer /* 创建 hrtimer 触发器 */
```

```bash
root@imx7adsabres:# echo 50 /sys/bus/io/devices/trigger0/sampling_frequency /* 设置采样频率 */
root@imx7adsabres:# echo trigger0 /sys/bus/io/devices/iio:device2/trigger/current /* 将触发器附加到设备 */
```

```bash
root@imx7adsabres:~ ./iio_generic_buffer --device-num 2 -T O -a 1l 10 -c 10 & /* 使用 iio_generic_buffer 应用设置缓冲区长度和转换次数；该应用启用扫描元素，执行采集并显示它们；之后，禁用扫描元素 */
```

使用的 iio 设备编号为 2

使用的触发 编号为 0

未启用通道，启用所有通道
