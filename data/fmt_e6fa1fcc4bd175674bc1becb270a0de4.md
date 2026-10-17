
### 13.1.2 Android 调试桥接 (ADB) 命令

#### 查询设备

在发布 `adb` 命令之前，了解哪些设备实例连接到了 `adb` 服务器是有帮助的。你可以使用 `devices` 命令生成一个已连接设备列表。

```
adb devices -l
```

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_307_0.png)

### 13.1.3 向特定设备发送命令

如果有多个设备在运行，在发布 `adb` 命令时必须指定目标设备。要指定目标，使用 `adb` 命令获取目标的序列号。

一旦获取了序列号，使用 `adb` 命令的 `-s` 选项来指定序列号。如果你同时使用 `-s` 和 `$ANDROID_SERIAL`，

`-s` 将覆盖 `$ANDROID_SERIAL`。

在以下示例中，获取已连接的设备列表，然后使用其中一个设备的序列号在该设备上安装 `helloWorld.apk`。

```
$ adb devices
List of devices attached
emulator-5554 device
emulator-5555 device
$ adb -s emulator-5555 install helloWorld.apk
```

```
h2smedia@h2media-VirtualBox:~/Downloads$ ls
playstore.apk
h2smedia@h2media-VirtualBox:~/Downloads$ abd install playstore.apk
 * daemon not running. starting it now on port 5037 *
 * daemon started successfully *
15405 KB/s (16667685 bytes in 1.056s)
Success
h2smedia@h2media-VirtualBox:~/Downloads$ 
```

## 13.2 在不同平台上的 ADB 安装过程

### 13.2.1 如何启用 USB 调试

1. 启动手机上的“设置”选项。
2. 点击“关于手机”，它应该位于列表底部。
3. 然后，要启用“开发者模式”，请连续点击 7 次“版本号”（`Build Number`）。完成后，你将收到一个提示消息（`toast message`）。
4. 返回到设置主页，你应该看到一个新的可以访问的“开发者选项”选项。
5. 进入并选择“USB 调试”模式。
6. 你已完成手机设置程序的一部分。然后，向下滚动并按照你操作系统的剩余步骤进行操作。

### 13.2.2 如何在 Microsoft Windows 上设置 ADB

1. 下载包含 Windows 版 Android SDK Platform Tools 的 ZIP 文件。
2. 将 ZIP 文件解压到方便的位置（例如 `C:\platform-tools`）。
3. 导航到你解压 ZIP 文件的目录。
4. 使用 Windows 资源管理器启动命令提示符（`Command Prompt`）。
5. 将你的智能手机或平板电脑连接到电脑。将 USB 模式设置为文件传输 (`MTP`)。这并非每个设备都必须的；但建议这样做以避免问题。
6. 一旦终端位于与 ADB 工具相同的位置，运行以下行命令：`adb devices`
7. 当你回到智能手机或平板电脑时，你会注意到一个弹窗请求你接受调试。请点击允许。

最后，输入第 6 步中的命令。如果一切顺利，你应该能够在 PowerShell 中看到你的设备序列号。

```
PS C:\platform-tools> adb devices
```

```
$ last login: Tue Feb 6 16:27:30 on ttyS0

List of devices attached to adb:

* daemon not running; starting now at tcp:5037

  * daemon started successfully

9a398aa8902 device
```

### 13.2.3 如何在 macOS 上设置 ADB

1. 下载包含 macOS 版 Android SDK Platform Tools 的 ZIP 文件。
2. 将 ZIP 文件解压到方便的位置（如桌面）。
3. 启动终端（`Terminal`）。
4. 输入以下命令进入目标目录：`cd /path/to/extracted/`
5. 示例：`/Users/Doug/Desktop/platform-tools/`
6. 通过 USB 连接将你的设备连接到 Mac。将连接模式设置为文件传输 (`MTP`)。这并非每个设备都必须的；但建议这样做以避免问题。
7. 一旦终端位于与 ADB 工具相同的位置，运行以下行命令：`adb devices`
8. 你的设备上会提示“允许调试”。请允许连接继续。

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_310_0.png)

```
$ last login: Tue Feb 6 16:27:30 on ttyS0

List of devices attached to adb:

* daemon not running; starting now at tcp:5037

  * daemon started successfully

9a398aa8902 device
```
