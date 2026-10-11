
- `devm_gpiod_get()` 函数 141
- `devm_gpiod_get_index()` 函数 141
- `devm_gpiod_put()` 函数 141
- `devm_iio_alloc()` 函数 480
- `devm_iio_register()` 函数 481
- `devm_iio_triggered_buffer_setup()` 函数 488
- `devm_input_allocated_device()` 函数 428
- `devm_ioremap()` 函数 146
- `devm_iounmap()` 函数 146
- `devm_kmalloc()` 函数 362
- `devm_kzalloc()` 函数 362
- `devm_led_classdev_register()` 函数 174
- `devm_pinctrl_register()` 函数 130
- `devm_regmap_init_i2c()` 函数 541
- `devm_regmap_init_spi()` 函数 541
- `devm_request_irq()` 函数 272-273
- `devm_request_threaded_irq()` 函数 290-291
- `devm_spi_register_master()` 函数 438, 442
- `device_tree`, 绑定 78
- `gpios` 143-144
- `i2C` 控制器和设备 212-213
- 中断、连接 268-271
- 中断、设备节点 269
- 引脚控制器 134-138
- `spi` 控制器 443
- `spi` 设备 444
- `device` 结构 73
- `device_create()` 函数 105
- `device_destroy()` 函数 105
- `device_driver` 结构 73
- `device_for_each_child_node()` 函数 243, 326
- `device_get_child_node_count()` 函数 241
- `device_register()` 函数 75-76
- `devm_gpiod_from_child()` 函数 326

# 直接内存访问 (DMA)

关于 373

缓存一致性 372-374

`dma_map_ops` 结构 374

# DMA 引擎 Linux API

关于 375

连续内存分配器 (CMA) 377-378

传输的描述符 (Descriptor), 375-376

`dmaengine_prep_slave_sg()` 函数 376

`dmaengine_slave_config()` 函数 375

`dma_async_isync_pending()` 函数 376

`dma_request_chan()` 函数 375

# 从用户空间进行 DMA

关于 407-409

`mmap()` 函数 407-409

`remap_pfn_range()` 函数 409

# DMA 映射，一致

关于 378-380

`dma_alloc_coherent()` 函数 378-380

`dma_free_coherent()` 函数 380

# DMA 映射，散列/聚集

关于 396-397

`dma_map_sg()` 函数 397

`dma_unmap_sg()` 函数 397

`scatter_table` 函数 396

`sig_init_table()` 函数 396

`sg_set_buf()` 函数 396

# DMA 映射，流式

关于 380-382

`dma_map_single()` 函数 380, 381

`dma_unmap_single()` 函数 380, 382

`dmaengine_prep_slave()` 函数 376

`dmaengine_slave_config()` 函数 375

`dmaengine_submit()` 函数 376

`dma_alloc_coherent()` 函数 378-380

`dma_async_issue_pending()` 函数 376

`dma_free_coherent()` 函数 380

`dma_ops_structures` 374

`dma_map_sg()` 函数 397

`dma_map_single()` 函数 380, 381

`dma_request_chan()` 函数 375

`dma_unmap_sg()` 函数 397

`dma_unmap_single()` 函数 380, 382

文档，针对处理器 123

`driver_register()` 函数 77

# E

## Eclipse

关于 55

针对内核源码的配置 56-66

针对 Linux 驱动程序的配置 67-72

安装 56

URL，用于安装 56

## 环境变量

U-Boot，在 i.MX7D 处理器上 42-43

U-Boot，在 SAMA5D2 处理器上 55

Yocto SDK 36-67

以太网，设置 31-32

`exit()` 函数 83

# F

`file_operations` 结构 92

`flushed_scheduled_work()` 函数 294, 295

`flush_workqueue()` 函数 296

`for_each_child_of_node()` 函数 177, 181

`free_irq()` 函数 272

`fsl,pins`, 设备树 136-137

`fnode_handle` 结构 241

# G

`get_user()` 函数 144

`gibc` 26

## GPIO 控制器驱动

关于 138-140

`gpio_chip` 结构 138-139

## GPIO 接口，基于描述符

`devm_get_gpiod_from_child()` 函数 326

`devm_gpiod_get()` 函数 141

`devm_gpiod_get_index()` 函数 141

`devm_gpiod_put()` 函数 141

`gpiod_direction_input()` 函数 141

`gpiod_direction_output()` 函数 141

`gpiod_to_irq()` 函数 143

GPIO 到 IRQ 的映射 143

获取 GPIOS 141-142

## GPIO 接口，基于整数 140

GPIO irqchips，分类 139-140, 264-268

GPIO Linux 编号 127

`gpiod_direction_input()` 函数 141

`http://www.rejoiceblog.com/`

索引

`gpiod_direction_output()` 函数 141

`gpiod_to_irq()` 函数 143

`gpiod_chip_to_irq()` 函数 262

IIO 设备，sysfs 接口 481

## IIO 驱动

`devm_iio_device_alloc()` 函数 480

`devm_iio_device_register()` 函数 481

注册 480-481

# H

硬件中断 (`hwirq`) 257

# I

I2C，定义 205

## I2C 设备驱动

`i2c_add_driver()` 函数 210

`i2c_device_id` 结构 211

`i2c_driver` 结构 210

注册 210

## I2C 子系统

I2C 总线核心 206

I2C 控制器驱动 206-207

I2C 设备驱动 208-209

注册，I2C 控制器驱动 207

`i2c_detect`，应用 433, 516

`i2c_adapter` 结构 212

`i2c_add_driver()` 函数 210

`i2c_del_driver()` 函数 210

`i2c_set_clientdata()` 函数 222

`i2c_utils`, 应用 433, 516

## IIO 事件

关于 468

`iio_event_spec` 结构 490

`iio_push_event()` 函数 492

内核钩子 491

sysfs 属性 490

## IIO 触发缓冲区

关于 487-488

`devm_iio_triggered_buffer_setup()` 函数 488

`iio_triggered_buffer_cleanup()` 函数 488

`iio_triggered_buffer_setup()` 函数 487

`io` 实用 494

## iio_info

关于 484

内核钩子 484

`iio_priv(v)` 函数 499, 502, 521

`iio_push_event()` 函数 492

`iio_push_to_buffers_with_timestamp()` 函数 487

`iio_triggered_buffer_cleanup()` 函数 488

`iio_triggered_buffer_setup()` 函数 487

工业 I/O 框架 (IIO), 关于 479

`io` 进程 30

`io` 程序 30

`init_wait_queue_head()` 函数 299

`INIT_WORK()` 函数 294

## 输入系统

关于 419

驱动 420-421

`input_test`，应用 421

`input_event()` 函数 424
