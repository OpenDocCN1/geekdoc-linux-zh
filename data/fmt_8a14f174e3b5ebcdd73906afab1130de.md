
08 将导线的另一端插入 6 号引脚，另一端插入面包板，根据电阻的大小确保为其留出足够的空间。接下来，准备好你的电阻。你可以使用高于或低于 270 欧姆的电阻，但完全不使用电阻可能会烧坏 LED。

假设我们想使用 GUI 而不是双击 SSH 进入 Pi，请通过 LXTerminal 打开新窗口。我们需要 root 权限来控制 LED，因此要么输入 `sudo`，要么在每个命令前加上 `sudo`。
- 输入 `su` 后接密码，或
- 在每个命令开头加上 `sudo`。

## 添加电阻

## 下载 GPIO 库

09 接下来添加电阻。将一端接到面包板上的地线，另一端在稍后后添加 LED 时连接到其旁边的 3V3 线上。注意，添加电阻没有所谓的正确或错误之分。

14 有一个非常实用的 Python 库可以让操作 GPIO 引脚变得轻而易举。在终端中，使用 `wget` 下载 tar 文件；使用 `tar` 将其解压。你将在新目录中获得所有文件。

```bash
wget https://python.org/packages/sources/RPI/RPI.GPIO-0.5.2a.tar.gz
tar xzf RPI.GPIO-0.5.2a.tar.gz
```

# 添加 LED

# 安装库

10 取出 LED，将“弯曲”的引脚端插入面包板上的 3V3 线路。将另一只引脚插入电阻旁边，位于地线的对侧。这完成了电路，我们准备好测试这个小项目了。

15 现在我们需要安装该库。这是一个 Python 安装方法的简单案例，因此我们需要 Python 的开发版本。在运行此命令之前，确保你处于库的目录。

```bash
sudo apt-get install python-dev
sudo python setup.py install
```

# 在脚本中导入库

## 接通电源

11 获取你的 micro-USB 脚本，并将电源插入墙上插座，或者插入电脑或笔记本电脑（并开启电源！）。你应该看到 LED 亮起。如果没有，请检查面包板或 Pi 上的连接，或者尝试不同的 LED。

16 创建一个新的 Python 脚本。紧接着编写主 GPIO 库，并将其放在一个 `try-except` 块中。使用 `Ctrl+X` 保存文件并选择 'yes'。

```python
cd /
cd Desktop
sudo python gpio.py
try:
    import RPi.GPIO as GPIO
except RuntimeError:
    print("Error importing GPIO lib")
```

![](img/4e995e1f4f2888a19b2d6bf0add45e32_61_0.png)

# 使用 GPIO 控制 LED 项目

## 你知道吗...

官方 Python 文档对于初学者和专业人士来说都是很好的资源。

http://python.org/doc.

## 使用 PWM

20 下一步是告诉引脚输出，然后提供一种退出程序的方法。在这里我们再次调用 `GPIO` 类，是 `PWM` 方法，传入引脚号；第二个值是频率（单位），在这种情况下是 0.5。

```python
p = GPIO.PWM(12, 0.5)
p.start(1)
input("Press enter to stop:")
p.stop()
GPIO.cleanup()
```

## 测试脚本

17 现在确保脚本导入成功，我们需要运行 python 命令并输入我们创建的脚本名称。如果一切顺利，你不应该看到任何错误信息。如果看到了，请返回之前的步骤检查所有操作是否正常。

- `python gpio.py`

## 调整 PWM

21 给 LED 添加一个定时器使其渐变，我们首先需要导入库，然后将 12 号引脚设置为 50Hz 频率并开始。

```python
import time
import RPi.GPIO as GPIO
GPIO.setmode(GPIO.BOARD)
GPIO.setup(12, GPIO.OUT)
p = GPIO.PWM(12, 50) # channel=1 frequency=50Hz
p.start(0)
```

## 设置 GPIO 模式

18 再次使用 nano 编辑脚本。我们将 GPIO 模式设置为 `BOARD`。对于初学者来说这是最安全的，无论你使用哪个版本的 Pi 都适用。最好选择一种 GPIO 规范并坚持下去，否则以后会产生混淆。

- `sudo gpio.py`

`GPIO.setmode(GPIO.BOARD)`

## 添加渐变

22 然后我们将添加另一个 `try-except` 块来控制功率。

```python
while True:
    for dc in range(0, 100, 5):
        GPIO.changeDutyCycle(dc)
        time.sleep(0.1)
    for dc in range(100, -1, -5):
        GPIO.changeDutyCycle(dc)
        time.sleep(0.1)
except KeyboardInterrupt:
    GPIO.cleanup()
```

## 项目

## 极大提升 fstab 以获得快速性能

## 选择外部 USB 驱动器

重启后，虚拟文件系统将挂载，`/var/log` 将位于 RAM 磁盘上。其他可以放入 RAM 的目录包括：

- `tmpfs /tmp tmpfs defaults,noat,nodisid,size=100m 0`

- `tmpfs /var tmpfs defaults,noat,nodisid,size=30m 0`

- `tmpfs /log tmpfs defaults,noat,nodisid,mode=0755,size=100m 0`

- `tmpfs /run tmpfs defaults,noat,nodisid,mode=0755,size=20m 0`

- `tmpfs /spool/내가 tmpfs defaults,noat,nodisid,mode=0700,gid=12,size=0`

将每项添加到 `/etc/fstab`。

通过将根文件系统迁移到外部 USB 驱动器来提高你的树莓派速度是一个开始，但你应该使用哪种设备获得获得性能？使用 USB 驱动器可以在不出现任何重大问题的情况下增加高达 16GB 的闪存（越大，读取/写所需的电流就越大）。更大的设备是昂贵且没必要的，除非你计划使用 HDD，因为它有自己的电源，因此不会有电源问题。一如既往，你的选择应该适合你的项目。

## 将你的操作系统移动到 HDD

## 备份 SD 卡

如果你担心 SD 卡的寿命，为什么不减少对树莓派的依赖呢？与其将 SD 卡作为廉价 SSD 使用，不如改变它的角色，添加一个 HDD 或 USB 闪盘来运行操作系统，将 SD 卡留给启动引导。这可以为 SD 卡带来显著的性能提升。

```
sudo dd bs=4M if=/dev/sdb of=/backup.img
```

路径 `/dev/sdb` 代表 SD 卡。复制需要 5-10 分钟。完成后，拔掉 SD 卡并连接你的 USB 设备。

## 将 Raspian 复制到 USB

使用一个格式化为 Ext4 的空白 USB 驱动器（或外部 HDD）作为目标驱动，

```
sudo dd bs=4M if=/backup.img of=/dev/sdc
```

将备份留在你的电脑上，以防万一。当 SD 卡和 USB 存储共享相同的磁盘镜像时，是时候考虑你接下来要做什么了——创建一个更快的树莓派。

如下，将文件系统放在 USB 闪盘上对于备份以及性能提升都很有处

![](img/4e995e1f4f2888a19b2d6bf0add45e32_65_0.png)

## 极大提升你的 Pi

## 分割树莓派分区

理想情况下，启动分区应该留在 SD 卡上，而根文件系统从外部 HDD 或 USB 驱动器运行。使用你偏好的分区管理器（大多数发行版中都有磁盘实用程序），卸载并删除 SD 卡上的根文件系统，确保你保留了启动分区。移除 SD 卡后，连接你的 USB 设备并删除启动分区，注意保持根文件系统完好。然后在 USB 设备上调整根文件系统的大小，使其保留 10MB。

![](img/4e995e1f4f2888a19b2d6bf0add45e32_66_0.png)

Alpine 散热：

树莓派的散热器非常多，通常价格低于 10 美元

## 识别根文件系统

你要进入 SD 卡和外部 USB 存储，所以你需要告诉树莓派根文件系统在哪里。在插入了 SD 卡的桌面 Linux 电脑上，

```
sudo nano /boot/cmdline.txt
找到 root=/dev/mmcblkp2 (或类似的)
将其更改为 root=/dev/sda2，这是你的外部 USB 驱动器。
保存并退出。
```

## 让你的树莓派快速且可靠
