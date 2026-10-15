
我们的 Weket Rocket Rocket 打印了八小时 59 分钟。12K Ele Saturn 4 能够在三小时 13 分钟内完成，但 Formlabs 4 看起来更精细，特别是如果你喜欢细节的话。在 Great 以及 Rocket 宇宙的细节中。

### 结论

开发者：Formlabs

网站：https://www.formlabs.com/uk/

价格：£4,439

| 特性 | 9/10 | 易用性 | 9/10 |
| :--- | :--- | :--- | :--- |
| 性能 | 6/10 | 价值 | 6/10 |

完美的打印不需要工程或化学背景，但请注意你正自己投入到什么样的环境。

![](img/e610c7a095fcd2c0c411ff707edde0b3_43_0.png)

![](img/e610c7a095fcd2c0c411ff707edde0b3_43_1.png)

![](img/e610c7a095fcd2c0c411ff707edde0b3_43_2.png)

![](img/e610c7a095fcd2c0c411ff707edde0b3_43_3.png)

## Raspberry Pi SSD

另一款 Pi 配件以 Linux 格式出现，紧接着 Les Pounder 就来来赞美它！

- 规格
- 尺寸：256GB, 512GB
- 类型：M.2 2230
- 接口：PCIe Gen 3
- 随机读写：40K/70K IOPS
- 256GB：50K/90K IOPS
- 512GB

Pi 5 为这款旗舰 Pi 引入了专用的 PCIe 连接，现在它有许多快速存储选项。在光谱的最顶端，另一端的 microSD 对应的是 NVMe SSD，它们在低功耗桌面电脑中极大提升了 Raspberry Pi 5。为了为此，你需要 M.2 HAT 来使用 Raspberry Pi SSD，当然，Raspberry Pi 有它自己的 M.2 HAT+，并与 SSD 本身一起提供。

![](img/e610c7a095fcd2c0c411ff707edde0b3_44_0.png)

要将 Pi OS 安装到 NVMe SSD，我们从 microSD 开始，连接所有外设，并重启操作系统。加载的软件是完全自动且简单的。我们启动 Raspberry Pi 5 并使用工具从卡复制安装到 SSD。五分钟后，Raspberry Pi 从 NVMe 启动并达到了速度 Gen 3。快速重启并准备好测试：Raspberry Pi SSD 提供两种规格——256GB 和 512GB——作为独立驱动器或套件（SSD Kit），包含了 Raspberry Pi M.2 HAT+。开始，256GB Raspberry Pi 启动到 OS 需 19 秒。这比 microSD 快，我们的 microSD 卡花了 22 秒。两者之间没有太大区别。由于 Raspberry Pi 正式支持 Gen 3，我们将关注对于那些使用 Geekworm 等板子的 Gen 2 性能。驱动器写入有多快？使用 `dd` 读取数据到 `/dev/nvme`，Gen 3 达到 443MB/s，对于 Raspberry Pi 来说速度足够。Gen 2 为 348MB/s，对于大多数用例也足够。我们测试了驱动器有多热？使用智能设备测试温度。空闲温度为 31°C。使用 15 分钟后，SSD 为 38°C。在压力测试下，Gen 3 达到 78°C，而 Gen 2 保持在 61°C。NVMe 存储为通用任务提供了明显的提升。

### 结论

开发者：Raspberry Pi Foundation

网站：www.raspberrypi.com/products/ssd/

价格：£27.70 (£41.50 SSD)

| 性能 | 易用性 | 价值 |
| :--- | :--- | :--- |
| 8/10 | 8/10 | 8 |

它与其他 SSD 一样工作，但你得到了 Raspberry Pi 的保证，如果你愿意多付一点钱，这是 Raspberry Pi 5 的 SSD。评分 8/10

## PI CAMERA

### 使用 BlueSky API 构建相机陷阱

仍然是温暖的，Les Pounder 使用 Pi 5 和 Camera Module 3 将图像发送到 BlueSky。

## 我们的专家

Les Pounder 是 Hartford 的副编辑，一位自由职业制作者。他关于功能和项目的博客见：http://blog.es/lt325

> “除非你住在山洞里，否则你不会错过这个故事：从 Pi 到 BlueSky 的摄像头。这让我们思考 BlueSky API（应用程序接口）；它有一个吗？结果显示它带我们进入钻研 API 和 Python 的兔子洞。”

![](img/e610c7a095fcd2c0c411ff707edde0b3_45_0.png)

钻研的结果是这个项目，我们使用 Raspberry Pi 和传感器触发一段代码，使用 BlueSky 拍摄入侵者的照片，并将当前日期作为消息的头部和正文。这是一个简单的项目，但我们建议不要用你的主账户使用，否则可能会产生垃圾信息并导致账户被封。如果你想设置更好的触发器，请考虑适配 Raspberry Pi。

障碍物（L）是测试代码的极佳选择。金球（R）是检测房间移动的更好选择。

### 相机设置

Raspberry Pi 连接到 Raspberry Pi 模块上的 CSI（摄像头）端口。对于 Pi，它连接到 MQTT 并需要不同的线。在关闭 Pi 的情况下，小心地从 Pi 的以太网/USB 端口拔下电缆。然后将电缆插入右侧。电缆端应该连接：如果没有，是否有损坏？确保电缆方向正确，然后锁定到位。一旦你的外设连接到 Pi 并进入桌面，我们打开终端并运行命令检查摄像头是否工作：

```
$ vlc2-ctl-list
```

摄像头工作正常。当你看不到预览时关闭预览窗口，关机并检查我们选择使用的 Raspberry Pi Camera Module 3，它具有自动对焦——有助于捕捉图像。

### BlueSky 密码

因为它不像“金球”那样敏感。如果我们在大房间里部署这个项目，“金球”会更好，因为它有三个连接——到 5v 引脚、GPIO 和 GPIO 17。请看下图说明。

BlueSky 像 Twitter 一样允许任何应用作为连接 API 的手段。对于我们来说，BlueSky 让我们轻松创建一个应用。在浏览器中，点击屏幕左侧的齿轮（设置）。选择密码。点击添加 App 按钮，然后在下一个屏幕中，将 App 密码命名为 Bot，并点击创建 App 密码。App 密码说明了这是一次性详情。就此，我们开始创建密码。

### 创建项目

### Pi 传感器触发

触发陷阱的是 PIR 传感器，你可以使用“金球” PIR 传感器，但我们选择使用 PIR 障碍物，它通常用于机器人。只需：

打开终端，运行软件系统，这允许我们安装合适的 Python，它与 BlueSky 的 API 交互。使用：`sudo apt install break-system-packages` 将模块安装到 Raspberry Pi 的 OS 系统中：

```
$ sudo apt update && sudo apt install break-system-packages
```

打开 Thorn 并创建一个新文件。在该文件中，创建两个对象：`username` 和 `password`。

`username` 是你的 BlueSky 用户名，biglesp-test.bsky。

社交功能，例如。你的 `app_password` 之前已经创建了：

```
username='YOUR BLUESKY USERNAME'
app_password='YOUR APP PASSWORD'
```

将该文件保存为 `secret.py` 并创建它以切换到新文件。

在此文件中，导入了一系列用于 BlueSky 的模块：访问我们的 `secret_file`、`time`（用于控制代码速度）、`Picamera2`（用于相机）、`libcamera`（用于自动对焦）、`datetime`（用于日期和时间）以及 GPIO Zeros 的 motionsensor（用于 PIR）：

```
from os import Client
import secret_file
import time
from picamera2 import Picamera2, Preview
from libcamera import controls
import datetime
```

![](img/e610c7a095fcd2c0c411ff707edde0b3_46_0.png)

创建一个告警，将 GPIO 连接到你的运动传感器类连接到 GPIO017 上的 PIR：

创建一个函数 `capture_and_post()`，它将捕捉入侵者的图像并将其发布到 BlueSky：

```
def capture_and_post():
```

在函数中，创建一个事件，并使用它来存储日期时间。使用 JPEG 文件用 `Picamera2` 创建对象：
