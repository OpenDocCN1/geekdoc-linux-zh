
```python
import asyncio

from bleak import BleakScanner
from bleak.backends.device import BLEDevice
from bleak.backends.scanner import AdvertisementData


def find_found(device: BLEDevice, advertisement_data: AdvertisementData):
    devices.add(device)


async def main():
    scanner = BleakScanner(discovery_callback=find_found)

    print("Scanning for devices...")
    await scanner.start()
    await asyncio.sleep(5)
    await scanner.stop()

for device in devices:
    print(f"{device.name} : {device.address}")

if __name__ == "__main__":
    devices = set()
```

对于这种通过名称过滤 `TP358` 的蓝牙钟，你只需要更改脚本`find_clocks.py`中的回调函数：

```python
def find_found(device: BLEDevice, advertisement_data):
    if device.name.startswith("TP358"):
        devices.add(device)
```

## 发送时间

现在你知道了蓝牙地址，可以写另一个脚本`sync_clock.py`（列表 3），它接收此地址作为参数并设置钟的时间。根据你之前的知识，这个逻辑非常直观。脚本定义了发送命令的特征，然后是一个函数`get_bytes_from_time`将 Unix 时间戳转换为需要发送到钟的字节。`main`函数连接到设备并写入正确的特征。如果你运行此命令，例如：

```bash
python sync_clock.py 12:58
```

它应该设置你钟的时间。

### 列表 3：`sync_clock.py`

```python
import asyncio
from datetime import datetime
import sys
from time import time

from bleak import BleakClient

COMMAND_CHAR = "00010203-0405-0607-0809-a0b1cd0b2"

def get_bytes_from_time(timestamp: float) -> bytes:
    """
    在 TP358 上设置时间所需的字节

    Args:
        timestamp (float): 编码为 Unix 时间戳

    Returns:
        bytes: 设置设备时间为 'timestamp' 的字节
    """
    date_time = datetime.fromtimestamp(timestamp)
    return get_bytes([
        date_time.year % 1000,
        date_time.month,
        date_time.day,
        date_time.hour,
        date_time.minute,
        date_time.second,
        date_time.weekday() + 1, # 周一到周日 -> 0-6
        # 使用 24 小时制
    ])

async def main(address: str):
    print(f"Connecting to {address}...")

    async with BleakClient(address) as client:
        command = get_bytes_from_time(time())
        await client.write_char(COMMAND_CHAR, command)

    print("time synchronized")

if __name__ == "__main__":
    try:
        asyncio.run(main(sys.argv[1]))
    except IndexError:
        print("Please provide the Bluetooth address of the device")
```

![](img/4dce49e5b3f3b719f67be60db9a2a5ec_49_0.png)

## 列表 4：发现蓝牙钟

```bash
$ bluetooth-clocks discover
$ Scanning for supported clocks...
$ Found a ThermoTP958 address BC:C7:DA:6A:C6, name TP958 (SSC)
$ Found a Xiaomi LWWD05 address EE:57:00:B1:38:96 LWWD05
$ Found a ThermoTP959 address: 10:76:34, name TP959 (SAAD)
$ Found a Qingping BT Clock address: 58:3D:94:53:DC, name Qingping BT Clock Lite
```

如果你家里有一个`bluetooth-clocks`不支持的蓝牙钟，尝试这里演示的逆向工程方法并贡献知识。我将结果`bluetooth-clocks`发布在 Python 仓库 (PyPI) 上 [7]。如果你想了解更多关于蓝牙以及如何在你的程序中使用它，请阅读这本书 [8]。

# 深度：编程快照 – 远程备份

## 从桌面控制你的备份

### 魔术包

能够启动和关闭 NAS 并检查当前状态而无需离开椅子，Mike Schilli 在本月的专栏编写了一个图形界面来发送魔术包（Magic Packet）。

![](img/4dce49e5b3f3b719f67be60db9a2a5ec_51_0.png)

作为备份，我使用了 `Synology` 以及一些大容量硬盘。但由于严格的规定和保护协议，我只有在需要时才会使用它（例如，备份正在运行）。为了开启它，我更倾向于偶尔点击图形界面（`GUI`），而不是离开椅子。

### 开启它

它是如何工作的？当它处于关闭状态时，NAS 会积极等待局域网唤醒（WoL）信号。它检测到网络处于低功耗模式。如果广播包到达局域网，设备的电源或主板将开启。

这里提供的 `Synology` 应用程序（图 1）通过本地网络启动 NAS 并显示启动过程的进度条。一旦系统启动并准备就绪，它就会通知用户。

魔术包包含了目标 `MAC` 地址，传输器可以独立通知不同的节点。

作者：Mike Schilli，一名位于旧金山湾区的软件工程师。自 1997 年以来，他在专栏中研究各种编程语言的实际应用。如果你通过邮件 `mschilli@perlitem.com` 联系他，他会回答任何问题。工作完成后，点击 `GUI` 上的按钮，NAS 将不再响应 `ping` 并最终进入睡眠（图 2）。

图 3 显示了魔术包格式的一个示例。包头的前 6 个字节包含固定值`0xFF`。后面是：

![](img/4dce49e5b3f3b719f67be60db9a2a5ec_51_1.png)

![](img/4dce49e5b3f3b719f67be60db9a2a5ec_51_2.png)

图 1：通过桌面应用启动 `Synology`。
图 2：按下按钮时，网络驱动再次关闭。

```
5 /magic header
0000000 ef ff ff 00 11 32 6c ab cd 32
0000010 32 6c ab cd 00 11 32 6c ab cd 32
0000020 32 6c ab cd 00 11 32 6c ab cd 32
0000030 32 6c ab cd 00 11 32 6c ab cd 32
0000040 32 6c ab cd 00 11 32 6c ab cd 32
0000050 32 6c ab cd 00 11 32 6c ab cd 32
0000060 32 6c ab cd 00 11 32 6c
```
