

- **IO Port**—与你在 `/etc/isapnp.conf` 中设置的相同 I/O 端口。检查 `isapnp.conf` 中表示 `(IO 0 (BASE 0x0220))` 的行，其指示值为 220。
- **MPU IO Port**—声卡的 MPU IO 端口。你可以通过检查 `isapnp.conf` 中表示 `(IO 1 (BASE 0x0330))` 的行来获取，其指示值为 330。如果你的声卡不支持 MPU，使用 -1。
- **IRQ**—声卡的 IRQ。检查 `isapnp.conf` 中表示 `(INT 0 (IRQ 5 (MODE +E)))` 的行，其指示值为 5。
- **8-Bit DMA**—在 DOS 和 Windows 中称为 *low DMA*。检查 `isapnp.conf` 中表示 `(DMA 0 (CHANNEL 1))` 的行，其指示值为 1。
- **Max 8-Bit DMA size in KB**—如果你没有 PnP 声卡，应从声卡手册中获取此信息。如果你有 PnP 声卡，检查你的 `/etc/isapnp.conf` 文件。如果在手册或 `/etc/isapnp.conf` 中找不到此信息，尝试在给定的范围内选择一个值并使用试错法。
- **16-Bit DMA**—在 DOS 和 Windows 中称为 *high DMA*。检查 `isapnp.conf` 中表示 `(DMA 1 (CHANNEL 5))` 的行，其指示值为 5。
- **Max 16-Bit DMA**—使用与 Max 8-Bit DMA Size in KB 相同的步骤。
- **Mic Auto Gain Control**—如果想要麦克风增益控制，请启用此项。

按下 Enter 会返回主屏幕（参见图 10.6）。如果你已完成设置系统中所有声卡，选择 no more sound cards。你将被询问是否要修改你的 `/etc/modules.conf`。回答 Yes。配置已保存，第一步完成。最后，通过发出以下命令启动 ALSA 驱动程序：

```
#/sbin/init.d/alsasound start
```

## FIGURE 10.6

你可以直接从 alsaconf 脚本菜单设置更多声卡和非 PnP 声卡。

![](img/659f91d9da7b29976c0625e2e9628511_245_0.png)

## Checking if ALSA Works

ALSA 使用 proc 文件系统与用户通信。你可以检查哪些声卡已初始化以及它们当前的状态。ALSA 在你配置它时创建了 /proc/asound/card# 接口。

以下命令将打印你的 pcm 设备的状态：

```
#cat /proc/asound/0/pcm0
```

以下命令将打印你的 Sound Blaster 16 的状态：

```
#cat /proc/asound/0/sb16
```

## Configuring ALSA to Start on System Boot Up

此过程将使 ALSA 在系统启动时启动。将符号链接添加到运行级别 2 和 3，以便系统在启动时运行 alsasound init 脚本并显示启动消息。它在关闭时也会再次运行并显示停止（kill）消息：

```
#cd /sbin/init.d/rc2.d
#ln -s ../../alsasound S70alsasound
#ln -s ../alsasound K70alsasound
#cd ../../rc3.d
#ln -s ../alsasound S70alsasound
#ln -s ../alsasound K70alsasound
```

## Some Useful ALSA Utilities

ALSA 包附带了一些有用的实用程序。它们主要用于高级功能和声音混音功能。以下实用程序随 alsautil 包提供：

- alsactl（一个混音器电平控制实用程序）
- alsamixer（一个 ncurses—基于控制台的—混音器）
- amixer（一个命令行混音器）
- aplay（一个命令行播放器和录音机）
- gmix（一个基于 GTK 的混音器）
- xamixer2（另一个高级基于 GTK 的混音器）

请注意，alsactl 用于存储声卡音量电平的当前配置然后再恢复它。每次关闭系统时，alsasound init 脚本都会使用 store 选项执行 alsactl，将当前混音器设置存储到 /etc/asound.conf。当你启动系统时，脚本会使用 restore 选项调用 alsactl，将混音器设置恢复到保存在 /etc/asound.conf 中的设置。这确保了当你返回系统时，你会发现相同的声音设置。

## Troubleshooting ALSA

ALSA 易于故障排除。要正确故障排除 ALSA，你应使用源代码包并使用 ./configure --with-debug=detect 编译它。安装驱动程序并在终端或另一个控制台中发出以下命令：

```
#tail -s /var/log/messages
```

继续安装过程并观察 tail 窗口/控制台。检查你得到的错误类型并尝试修复它们。

如果声卡支持已内置在内核中，ALSA 将无法工作。如果无法加载 ALSA 模块，请检查你的内核配置。

如果 OSS 已加载，ALSA 也无法工作。同一张卡一次只能加载其中一个。

## Enlightenment Sound Daemon (ESD)

Enlightenment Sound Daemon (ESD) 本身并不是声卡驱动程序。正如名称所示，ESD 是一个普通守护进程。为什么需要 ESD 是另一个故事。正如你可能注意到的，声卡一次只能支持一个 wav 文件。Windows 游戏的一个令人惊叹的事情是能够同时听到多个声音。这实际上是 DirectX 赋予 Windows 的功能。Linux 程序员不喜欢错过这样的优秀功能。所以，他们想出了 ESD。ESD 位于声卡驱动程序之上并控制输入的内容。因此，对于使用 ESD API 的程序，两个程序可以同时输出声音（wav）。

不涉及技术细节，ESD 等待需要声音输出的程序。它处理发送给它的流并设法将它们混合成一个流并输出到声卡。用非常简单的话来说，这就是 ESD 的工作原理。

请记住，你只能通过编写为支持 ESD 的程序播放声音。其他为 OSS 和 ALSA 编写的程序，在 ESD 终止之前将无法工作。当 ESD 运行时，只有 ESD 程序会播放。

如果不运行 ESD，Enlightenment 中的声音将无法工作。ESD 对 Enlightenment 至关重要，如果你想听到声音。

以下是一些使用 ESD 的程序：

- Enlightenment
- X Multimedia System (xmms)，它有一个 ESD 插件
- mpg123
- E-music
- ALSA player

要运行 ESD，你只需要能够使用 OSS 或 ALSA 访问你的声卡。ESD 不是低级驱动程序，也不是为此设计的。它将使用你正在使用的现有声卡驱动程序并实现额外的功能。

## Installing ESD

安装 ESD 的过程很简单。你只需按照本章所述设置你的声卡，然后安装包（esd, esound）。

安装包完成后，只需以普通用户身份运行 ESD：

```
$esd
```

ESD 将自动获取系统上的声音设备。你会听到类似太空的声音，表示 ESD 已启动。你完成了！打开 XMMS 或任何其他使用 ESD 的应用程序并播放声音。

## Other Programs to Control ESD

ESD 包配备了一些额外的程序来帮助用户控制 ESD。如果你的系统有多个用户，你可能希望在你使用声卡时阻止他们使用。否则，他们会与你共享。记住，由于它能够同时播放两个声音，当你在播放声音时，其他用户也可以播放。输出都会到你的扬声器。可以控制此功能的实用程序称为 esdctl。以下示例显示了此强大实用程序的使用方法：

- $esd$（启动 ESD）
- $esdctl lock (只有启动 esd 的用户才能播放声音)
- $esdctl unlock (每个人都可以播放声音)
- $esdctl standby (不播放，守护进程释放音频设备。需要 OSS 或 ALSA 驱动程序的程序可以在不杀死 esd 的情况下工作)
- $esdctl resume (在待机后，音频重新接管声卡设备并准备播放)

> **CAUTION**
> ESD 不仅赋予你一次播放多个声音文件的能力；它还赋予所有可以访问系统的用户这种能力。如果你不想让其他人在你使用时使用 ESD，只需锁定它。

