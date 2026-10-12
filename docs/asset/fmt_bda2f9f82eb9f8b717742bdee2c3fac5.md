
```bash
# digitemp -q -a -d 3 -n 2
Jun 11 00:26:34 Sensor 0 C: 24.00 F: 75.20
Jun 11 00:26:35 Sensor 1 C: 25.12 F: 77.22
Jun 11 00:26:37 Sensor 0 C: 24.06 F: 75.31
Jun 11 00:26:38 Sensor 1 C: 25.19 F: 77.34
```

现在你已经从 `Linux` 系统中读取了温度信息，可以尝试一些使用这些信息的有趣方法。

### 持续记录温度

如果你想随时间跟踪温度变化，可以使用 `Linux` 的 `cron` 功能按照设定的间隔持续运行 `digitemp` 并写入日志文件。你可以从该日志文件中提取数据并读取到 Web 页面、电子邮件或图表中。以下是该操作的步骤。

1. 以 `root` 用户身份从终端窗口输入以下内容：

```bash
crontab -e
```

这会在 `vi` 编辑器打开 `root` 用户的 `crontab` 文件。

2. 假设你已经在 `/usr/local/bin` 目录下创建了 `.digitemp-file`（如前所述），在你创建的 `crontab` 文件中添加以下行：

```bash
*/30 * * * * /usr/local/bin/digitemp -a > /var/log/temperature
```

如果你不知道如何使用 `vi` 编辑器，输入 `i` 打开新行；输入显示的行（你可以使用退格键），然后按 `Esc` 键。输入 `:ZZ` 保存并关闭文件。如果卡住了，只需输入 `:q!` 即可不保存任何更改退出文件。确保你获取的内容与所示完全一致。这将每 30 分钟将所有传感器的温度记录到 `/var/log/temperature`。你可以将 `30` 改为任何数字。

3. 如果一切看起来运行正常，你可以尝试几条 `digitemp` 命令。

# 164 第三部分 — 家庭项目

## 搜索 1-Wire 局域网

```
1025042E000800AA : DS1820 温度传感器
107FC04800800EF : DS1820 温度传感器

ROM #0 : 1025042E000800AA
ROM #1 : 107FC04800800EF

已写入 .digitemp-prc
```

`ROM` 编号是每个传感器唯一的，它们按照在总线上被发现的顺序列出。当 `digitemp` 命令执行完成后，它会在当前目录（`/usr/local/bin/`）写入 `.digitemp-file`。

无论 `digitemp` 命令位于什么位置，在运行该命令时，它会在当前目录查找 `.digitemp-file`。如果你在像 `/var/www/html/index.php` 的 Web 页面中运行 `digitemp`，则会在 `/var/www/html/` 下创建一个 `.digitemp-file`。

2. 运行 `digitemp` 命令读取所有（`-a`）传感器的温度：

```bash
digitemp -a
Digitemp v3.2.0 Copyright 1996-2003 by Brian Lane
GNU Public License v2.0 - http://www.brianlane.com
Jun 10 23:50:26 Sensor 0 C: 24.00 F: 75.20
Jun 10 23:50:28 Sensor 1 C: 25.19 F: 77.34
```

这个示例显示了两个传感器：一个在小板（`DT1A`）上，另一个在电线的末端（`SOA`）。

如果你在运行 `digitemp` 命令时遇到错误，有几种尝试的方法：

- 检查当前目录下是否存在 `.digitemp-file`。（如果不存在该文件，你可能会收到读/写错误。）
- 检查你的 `COM` 端口（`COM1, COM2, COM3`）是否与初始化设备时使用的设备名称（`ttyS0, ttyS1, ttyS2`）匹配。
- 检查端口权限是否打开（`ls -l /dev/ttyS0`）。要允许广泛访问，请使用 `root` 用户：`chmod 666 /ttyS0`

3. 如果一切看起来运行正常，你可以尝试几条 `digitemp` 命令。

第一个示例带有 `-w` 选项，它会“遍历”总线上的所有设备，你可以检查总线上连接哪些传感器：

```bash
digitemp -w
Devices on the Main LAN
1025042E000800AA : DS1820 Temperature Sensor
107FC04800800EF : DS1820 Temperature Sensor
```

这是一个如何输出带有时间和温度信息的一行的示例。以下示例抑制了表头（`-q`），读取温度（`-t`）并输出（`-c`）我输入的日期（`%b %d`）、时间（`%H:%M:%S`）、华氏度（`%8.2F`）和摄氏度（`%2.2C`）。屏幕上应该显示这两条命令。

```bash
digitemp -t 0 -c "-On %b %d %H:%M:%S in NYC temperature is %.2F (F), %2.2C (C)"
```

`Jun 11 at 12:33:41 in NYC the temperature is 75.20 (24.00 (C))`

# 第 9 章 — 构建温度监控器

下一个示例采样了表头（`-q`）并每隔三秒（`-d 3`）收集两次（`-n 2`）数据。你可以增加间隔和收集数据的次数，以测试更长时间范围内的温度。

```bash
# digitemp -q -a -d 3 -n 2
Jun 11 00:26:34 Sensor 0 C: 24.00 F: 75.20
Jun 11 00:26:35 Sensor 1 C: 25.12 F: 77.22
Jun 11 00:26:37 Sensor 0 C: 24.06 F: 75.31
Jun 11 00:26:38 Sensor 1 C: 25.19 F: 77.34
```

现在你已经从 `Linux` 系统中读取了温度信息，可以尝试一些使用这些信息的有趣方法。

### 持续记录温度

如果你想随时间跟踪温度变化，可以使用 `Linux` 的 `cron` 功能按照设定的间隔持续运行 `digitemp` 并写入日志文件。你可以从该日志文件中提取数据并读取到 Web 页面、电子邮件或图表中。以下是该操作的步骤。

1. 以 `root` 用户身份从终端窗口输入以下内容：

```bash
crontab -e
```

这会在 `vi` 编辑器打开 `root` 用户的 `crontab` 文件。

2. 假设你已经在 `/usr/local/bin` 目录下创建了 `.digitemp-file`（如前所述），在你创建的 `crontab` 文件中添加以下行：

```bash
*/30 * * * * /usr/local/bin/digitemp -a > /var/log/temperature
```

如果你不知道如何使用 `vi` 编辑器，输入 `i` 打开新行；输入显示的行（你可以使用退格键），然后按 `Esc` 键。输入 `:ZZ` 保存并关闭文件。如果卡住了，只需输入 `:q!` 即可不保存任何更改退出文件。确保你获取的内容与所示完全一致。这将每 30 分钟将所有传感器的温度记录到 `/var/log/temperature`。你可以将 `30` 改为任何数字。

3. 如果一切看起来运行正常，你可以尝试几条 `digitemp` 命令。

# 168 第三部分 — 家庭项目

7. 你可以使用任何 Web 浏览器（如 `Mozilla`）打开 `index2.php` 文件。图 9-2 显示了该文件的示例：

![](img/93c80330322e65d5105a6014afe2d85d_195_0.png)

图 9-2：在网页上显示温度读数。

## 在邮件签名中添加温度

你可以将温度输出放置在签名文件中，这样它就会出现在所有发出的邮件的末尾。你可以使用 `my_sig_temp` 脚本创建签名文件。`my_sig_temp` 脚本：

- 从 `/var/log/temperatures` 读取当前温度
- 创建一个包含你的姓名和当前温度的签名文件

以下步骤允许你创建一个 `crontab` 条目，以自动创建并更新带有最新温度的签名文件：

1. 修改 `/usr/local/bin/my_sig_temp`，更改目录和文件名，以反映你的邮件读取器签名文件的位置。例如，如果你的主目录是 `/home/jjones` 且你在使用 `Evolution` 邮件，你可以按照如下所示更改值：

   - 要创建的签名文件的目录和文件名
