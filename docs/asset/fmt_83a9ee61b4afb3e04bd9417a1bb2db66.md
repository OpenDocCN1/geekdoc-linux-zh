
- 这些是 bionic 用于名称解析的属性

# 第15 节 网络

![](img/c6f4acfaca4829cadfb14f4d738cba2c_396_0.png)

# LF315 深入 Android：Android 内部原理

![](img/c6f4acfaca4829cadfb14f4d738cba2c_397_0.png)

## 第15 节 网络

![](img/c6f4acfaca4829cadfb14f4d738cba2c_398_0.png)

- `BoardConfig.mk` 中包含一些 WiFi 相关设置：
  - `BOARD_WPA_SUPPLICANT_DRIVER` - 例如 `"NL80211"`
  - `WPA_SUPPLICANT_VERSION` - 例如 `"VER_0_8_X"`
  - `BOARD_WLAN_DEVICE` - 例如 `"bcmdhd"`
  - `WIFI_DRIVER_MODULE_PATH` - 例如 `"/system/lib/modules/bcmdhd.ko"`

Copyright © 2013 Linux Foundation. All rights reserved. 请勿传播。

# LF315 深入 Android：Android 内部原理

![](img/c6f4acfaca4829cadfb14f4d738cba2c_399_0.png)

- 管理 WiFi、蓝牙和 USB 网络连接
- 检测新连接，断开旧连接
- 管理 USB 共享网络和 WiFi 热点
- 与 `ConnectivityManager` 通信
- 在 `init.rc` 中作为服务启动
- 编写为一个独立的 root 权限进程，以便将高层组件与 root 权限级隔离
- 引入于 2.2 Froyo 版本

Copyright © 2013 Linux Foundation.
All rights reserved. 请勿传播。

## 第15 节 网络

![](img/c6f4acfaca4829cadfb14f4d738cba2c_400_0.png)

- 管理各种网络连接
- 当某个连接失败时，回退到其他连接
- 当某个连接可用/不可用时通知系统
- 允许应用程序获取有关连接的各种信息

Copyright © 2013 Linux Foundation. All rights reserved. 请勿传播。

### 网络接口类型

- `ConnectivityManager` 完全支持
- `TYPE_MOBILE_DUN`, `TYPE_MOBILE_HIFI`,
  `TYPE_MOBILE_MMS`, `TYPE_MOBILE_SUPL`
- `TYPE_BLUETOOTH`
- `TYPE_WIFI`
- `TYPE_ETHERNET`

## 第15 节 网络

# 393

### 接口管理

- 正常模式
  - 仅一个接口启动，`wlan0` 或 `rmnet0`
- USB 共享网络模式
  - 开启 IP 转发
  - 将 `rndis0` 作为 USB gadget 启动
  - 为 `rndis0` 添加路由
  - 启动 `/system/bin/dnsmasq`
- WiFi 热点
  - 关闭 WiFi 接口 (`wlan0`)
  - 启动接入点接口 (例如 `athap0`)
  - 创建与共享网络相似的路由

# LF315 深入 Android：Android 内部原理

### 以太网问题

- 以太网在 Android 中并不是一等公民
- 底层工具 (`netcfg...`) 可以工作但 `ConnectivityManager` 忽略了它
- 某些应用无法工作（例如：Google Play Store）
- 浏览器是正常的，因为它们绕过了 CM（但多媒体将失败）
- 解决方案：Android 团队提供的以太网连接管理器 (ECM) 补丁

![](img/c6f4acfaca4829cadfb14f4d738cba2c_403_0.png)

## 实验 15

**练习 15.1 配置接口**

将网线插入 Beaglebone。

使用 `netcfg` 和 `ifconfig` 启动 `eth0` 并赋予 IP 地址。检查是否可以 ping 网络上的其他节点。使用 DHCP 配置 `eth0`。

如果你可以访问网页，尝试使用浏览器检查是否可以访问网站。

![](img/c6f4acfaca4829cadfb14f4d738cba2c_405_0.png)

# 第16 节 输入设备

397

![](img/c6f4acfaca4829cadfb14f4d738cba2c_406_0.png)Copyright © 2013 Linux Foundation. All rights reserved.

### Android 输入层

- 从底层...
- Linux evdev 驱动生成事件并向上传递
- `EventHub` 读取事件并向上传递
- `InputReader` 解码并转换为 Android 事件
- `InputDispatcher` 将事件发送到相应的窗口

Android 组件的代码位于
`EventHub`: `frameworks/base/services/input/EventHub.cpp`
`InputReader`: `frameworks/base/services/input/InputReader.cpp`
`InputDispatcher`: `frameworks/base/services/input/InputDispatcher.cpp`

## 第16 节 输入设备

![](img/c6f4acfaca4829cadfb14f4d738cba2c_408_0.png)

- Linux 输入层 (`evdev`) 为产生数据的设备提供事件机制
- 通常用于人类输入设备：键盘、鼠标、触摸屏
- 这些事件由 `EventHub` 处理
- 但也用于定时产生输入的设备：距离传感器、罗盘
- 这些事件由 Android 传感器子系统处理

![](img/c6f4acfaca4829cadfb14f4d738cba2c_408_1.png)(img/c6f4acfaca4829cadfb14f4d738cba2c_408_2.png)

### 输入设备驱动

- 事件驱动的结构在 Linux 源码树的 `Documentation/input` 中
- 每个输入驱动注册时会在 `/dev/input` 中创建一个节点
- 从节点读取事件
- 有各种 `ioctl` 命令来获取其他信息

```
ls /dev/input

event0

event1

event2

event3

event4
```

![](img/c6f4acfaca4829cadfb14f4d738cba2c_409_0.png)

## 第16 节 输入设备

401

### getevent 工具

- Android 命令 `getevent` 在调查输入设备非常有用
- 使用 `getevent -h` 查看选项列表

```
# getevent

add device 1: /dev/input/event4

name: "lightsensor-level"

add device 2: /dev/input/event3

name: "proximity"

add device 3: /dev/input/event2

name: "tuna-gpio-keypad"

add device 4: /dev/input/event0

name: "barometer"

add device 6: /dev/input/event1

name: "Melsas MMSxx Touchscreen"
```

![](img/c6f4acfaca4829cadfb14f4d738cba2c_410_0.png)(img/c6f4acfaca4829cadfb14f4d738cba2c_410_1.png)Copyright © 2013 Linux Foundation. All rights reserved

# LF315 深入 Android：Android 内部原理

### 事件

- 每个事件由一个 16 字节的 `input_event` 描述

```
struct input_event {
    struct timeval time;
    __u16 type;
    __u16 code;
    __s32 value;
}
```

- `time`: 时间戳
- `type`: 事件类型，例如按键、鼠标移动
- `code`: 取决于类型，例如对于键盘，`code` = 键
- `value`: 取决于类型，例如对于键盘，1 表示按下，0 表示释放

![](img/c6f4acfaca4829cadfb14f4d738cba2c_411_0.png)(img/c6f4acfaca4829cadfb14f4d738cba2c_411_1.png)Copyright © 2013 Linux Foundation. All rights reserved. 请勿传播。

### 事件类型

* 键盘
    * `type` = `EV_KEY`
    * `code` = keycode，在 `include/uapi/linux/input/` 中定义
    * `value` = 1 (按下) 0 (弹起)
* 鼠标
    * `type` = `EV_REL`
    * `code` = `REL_X` 或 `REL_Y`
    * `value` = X 或 Y 坐标
* 触摸屏
    * `type` = `EV_ABS`
    * `code` = `ABS_X`, `ABS_Y`, `ABS_Z` (压力)
    * `value` = X, Y 或 Z 坐标

![](img/c6f4acfaca4829cadfb14f4d738cba2c_412_0.png) 同步事件由于某些事件类型（例如 `EV_ABS`）需要 2 或 3 个事件包来提供 X、Y 和 Z 的完整信息，因此需要一种方法指示所有输入已报告：`EV_SYN`

- `type` = `EV_SYN`
- `code` = `SYN_REPORT`
- `value` = 0

- 所有事件报告（包括键盘等单值事件）都必须发送 `EV_SYN` 以表示此报告的结束

## 多点事件

- 多点事件通过以下报告：
  - `EV_ABS`, `ABS_MT_TRACKING_ID`, `value` = 此触点的唯一 ID
- 随后是一个或多个
  - `EV_ABS`, `ABS_MT_PRESSURE`, `value`
  - `EV_ABS`, `ABS_MT_POSITION_X`, `value`
  - `EV_ABS`, `ABS_MT_POSITION_Y`, `value`
  - `EV_SYN`, `SYN_REPORT`
- 由以下终止：
  - `EV_ABS`, `ABS_MT_TRACKING_ID`, `value` = 0xffffff
  - `EV_SYN`, `SYN_REPORT`

## 键布局文件

- Linux 扫描码通过键布局文件 (`.kl`) 翻译为 Android 键码
- 格式为：
  - `key <scancode> <keycode> [flags]`
  - `scancode` 是 Linux 键码
  - `keycode` 是 Android 键名
  - `flags` 是可选的策略标志，用空格分隔
  - 示例（来自 Galaxy Nexus, `tuna-gpio-keypad.kl`）

```
key 114 VOLUME_DOWN WAKE
key 115 VOLUME_UP WAKE
key 116 POWER WAKE
```

Linux 键码定义在 `include/linux/input.h` 中

Android 键名定义在 `android.view.KeyEvent` 中。注意键布局文件中的名称已去除了 `KEYCODE_` 前缀。

## 策略标志

- `WAKE` 和 `WAKE_DROPPED`: 唤醒设备
- `SHIFT`: 解释为 shift
- `CAPS_LOCK`: 解释为大写锁定
- `ALT`: 解释为 alt
- `ALT_GR`: 解释为 alt gray
- `FUNCTION`: 解释为功能键
- `VIRTUAL`: 这是一个相邻主触摸的虚拟软键

![](img/c6f4acfaca4829cadfb14f4d738cba2c_416_0.png)

![](img/c6f4acfaca4829cadfb14f4d738cba2c_416_1.png)

## 文件命名

- 系统按顺序搜索键布局文件：
  - `/system/usr/keylayout` 和 `/data/system/devices/keylayout`
- 文件可能基于 Linux 输入设备名称命名
  - 例如 `tuna-gpio-keypad.kl`
- 通过 USB 或蓝牙连接的外部设备可能会改用厂商 ID 和产品 ID（以及可选版本号）：
  - `Vendor_XXXX_Product_XXXX.kl` 或
  - `Vendor_XXXX_Product_XXXX_Version_XXXX.kl`
  - 例如 `Vendor_045e_Product_028e.kl`
- 在所有情况下，如果未找到特定的 `.kl` 文件，则回退到 `Generic.kl`

![](img/c6f4acfaca4829cadfb14f4d738cba2c_417_0.png)

## 验证键映射

- 构建工具

```
$ mmm frameworks/base/tools/validatekeymaps
```

- 使用它检查修改后的文件

```
$ validatekeymaps tuna-gpio-keypad.kl
```

正在验证文件 'tuna-gpio-keypad.kl'...
E/KeyLayoutMap(87688): tuna-gio-keypad.kl:24: Expected Error -22 parsing key layout file.

失败！

![](img/c6f4acfaca4829cadfb14f4d738cba2c_418_0.png)

## 键字符映射文件

- 键字符映射文件 (`kcm` 文件) 将 Android 键码与修饰符的组合映射到 Unicode 字符
- 每个内部键盘应该有一个
- 以 `type <type declaration>` 开始
- 其中 `<type declaration>` 是以下之一：
  - `FULL`: 完整的 PC 风格键盘
  - `ALPHA`: 仅包含字母数字键但很少（没有）其他键的键盘
  - `NUMERIC`: 数字（12 键）键盘
  - `PREDICTIVE`: 包含所有字母的键盘，但每个键有多个字母
  - `SPECIAL_FUNCTION`: 系统控制功能而非用于打字

![](img/c6f4acfaca4829cadfb14f4d738cba2c_419_0.png)

## 第 16 节 输入设备

![](img/c6f4acfaca4829cadfb14f4d738cba2c_420_0.png)

- 键映射根据 shift、alt 和 ctrl 状态决定生成的字符
- 每个 Android 键码都有一个格式如下的映射：

```
key <key name> {
  label: <键上打印的字符>
  base: <基础字符>
  shift: <按下 shift 时的字符>
}
...
```

该格式非常复杂，这只是可能映射的概览。完整详情请参阅 http://source.android.com/tech/input/key-character-map-files.html

## LF315 Android 内部：Android 内部原理简介

## 示例

```
key A {
  label: 'A'
  base: 'a'
  shift, capslock: 'A'
}

key C {
  label: 'C'
  base: 'c'
  shift, capslock: 'C'
  alt: '\u00e7'
  shift+alt: '\u00c7'
}
```

注意：'u000e7' 是 Unicode 字符 e7，即小 c 变音；c7 是大 C 变音

## .kcm 文件命名

- 系统按顺序搜索键字符映射文件：
  - `/system/usr/keychars` 和 `/data/system/devices/keychars`
- 文件可能基于 Linux 输入设备名称命名
  - 例如 `tuna-gpio-keypad.kcm`
- 通过 USB 或蓝牙连接的外部设备可能会改用厂商 ID 和产品 ID（以及可选版本）：
  - `Vendor_XXXX_Product_XXXX.kcm` 或
  - `Vendor_XXXX_Product_XXXX_Version_XXXX.kcm`
  - 例如 `Vendor_045e_Product_028e.kcm`
- 在所有情况下，如果未找到特定的 `.kcm` 文件，则回退到 Generic `.kcm`

## 输入设备配置文件

- 输入设备配置文件 (`.idc` 文件) 包含影响输入设备行为的设备特定配置属性
- 触摸屏通常需要
- 你可以设置的一些属性是：
  - `touch.deviceType` = `touchScreen` | `touchPad` | `pointer` | `default`
  - `touch.orientationAware` = 0 | 1
  - `touch.size.calibration` = `none` | `geometric` | `diameter` | `area` | `default`

背景信息参阅
http://source.android.com/tech/input/input-device-configuration-files.html
触摸屏详情参阅
http://source.android.com/tech/input/touch-devices.html

## 第 16 节 输入设备

![](img/c6f4acfaca4829cadfb14f4d738cba2c_424_0.png)

```
touch.deviceType = touchscreen
touch.orientationAware = 1
touch.size.calibration = diameter
touch.size.scale = 10
```
