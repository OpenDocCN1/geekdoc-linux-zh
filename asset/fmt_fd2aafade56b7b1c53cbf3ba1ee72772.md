
$ sudo apt-get install linux-image-4.3.0303-generic-v4.3-1

$ sudo apt-get install linux-headers-4.3.0303-5150-amd64

$ sudo apt-get install linux-headers-4.3.0303-generic-v4.3-1

你展示了触摸屏在横屏模式下工作正常。目前，你每次登录 Ubuntu 都需要手动更新此项，而且当你将背部旋转到竖屏时，触摸屏将无法正常工作。

```
$ sudo apt-get install --linux-4.7 image*"
```

$ sudo apt-get install linux-headers-4.3.0303-5150-amd64

$ sudo apt-get install linux-headers-4.3.0303-generic-v4.3-1

重启后，你会发现现在屏幕上可以触摸了（而不只是多点触控），而且你可以登录且设置将不再报错。我们已经修复了这个问题。
现在，如果你想旋转屏幕或触摸，可以使用我们编写的以下脚本。

如果你想将 de-screen 脚本适配到触摸视图，右键点击并选择“将页面另存为平板电脑”。然后用 Gedit 或 nano 打开它并修改以下行：

```
TOUCHSCREEN="Capacitive Touchscreen";
```

保存并使用该脚本：

```
$ ./install_derotate.sh
```

将 `+` 替换为 `normal` 正常）、`inverted` 反转）、`left` 左）或 `right` 右），以旋转屏幕和触摸屏矩阵。当你需要旋转屏幕时，先使用该脚本。当你需要恢复到平板视图时，运行 `./install_derotate.sh` 来恢复触摸屏和触摸功能。

为了支持 SD 卡，我们不得不使用 USB Wi-Fi 适配器连接网络，且声音不再工作。可能还存在一些问题，你可以通过配置一个简易驱动程序来修复。

寻找我们在 `GRUB_CMDLINE_DEFAULT` 中创建的该行。将 `GRUB_CMDLINE_DEFAULT="quiet splash"` 改为添加 `video=0`。

保存、退出并重启：

```
$ sudo update-grub
```
