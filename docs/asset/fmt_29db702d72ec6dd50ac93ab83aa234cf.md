
23. 重新连接主板和屏幕之间的电源和屏幕线。图 15-10 显示了一个示例。

24. 将主板、风扇和硬盘放在外壳中。

25. 将风扇、电源、以太网适配器（如果包含网卡）以及电源连接到数字相框。图 15-11 显示了最终组件就位的示例。

26. 再使用两根木条横跨主板、硬盘和电源并固定。

27. 为电源线和（可选的）网卡切出位置。Chuck 使用扎带让电缆保持整洁。

28. 切一个与笔记本电脑上孔大小类似的通风孔。最好，该孔应该在风扇上方以促进空气流通。安装背板（将其固定）。

29. 打开相框并查看它是否工作。如果是，你应该看到类似于图 15-11 中的框架的内容。

![](img/93c80330322e65d5105a6014afe2d85d_300_0.png)

图 15-10：从主板到 `LCD` 连接电源和屏幕线。

![](img/93c80330322e65d5105a6014afe2d85d_300_1.png)

图 15-11：将主板和最终组件放入相框中。

# 274 第五部分 — 趣味

## 使用你的数字相框

`Linux Toys` 数字相框被设计为独立运行。此时，你不需要做任何事情，只需开关即可。然而，通过重新连接键盘或使用网卡，你可以为数字相框添加和删除图像。

我们没有让数字相框访问串口、`USB` 以及除以太网以外的端口。然而，如果你开放了这些端口，你就可以将数码相机或其他设备连接到数字相框，然后通过以太网卡访问笔记本（如本章前面的“加载图像”部分所述）。

要关闭数字相框时，你通常可以直接拔掉电源。没有太多打开的文件，所以应该没问题。更干净的关机方法是以 `root` 用户登录（通过以太网连接使用 `ssh` 命令）。然后在拔掉电源前输入 `shutdown` 关闭数字相框。

### 总结

旧笔记本电脑可以很好地作为一个数字相框。如果你能小心地将笔记本组件从外壳中取出，然后在相框中重新组装所需的部件，你就能得到一个展示数字图片的漂亮配件。添加可选的网卡后，你可以从 `LAN` 访问数字相框，定期更新你的图片库。

## 获取软件

`Linux Toys` 项目中使用的所有软件都来自两个地方之一：`Red Hat Linux` 或 `Linux Toys CD`。第一个需要你自己获取；第二个则随本书附带。

## Red Hat Linux

完整的 `Red Hat Linux` 安装程序包含三张光盘。对于我们的项目，我们使用的是 `Red Hat Linux` 的 `i386` 版本（换句话说就是 `PC` 版本）。以下是获取 `Red Hat Linux` 的几种方法：

- 如果你想要全套 `Red Hat Linux` 安装光盘以及关于如何使用和管理 `Red Hat Linux` 的说明，可以购买《`Red Hat Bible`》（由 `Christopher Negus` 编写，`Wiley` 出版）。这些光盘的内容与 `Red Hat` 网站上下载的内容相同。
- 你可以从许多不同的 `Red Hat Linux` 镜像站点下载安装光盘的镜像。然后你可以将这些镜像刻录到 `CD` 中，或者从硬盘镜像或通过网络安装软件。

`Linux Toys` 项目在 `Red Hat Linux 9` 上进行过测试，但推测它们可以在更高版本的 `Red Hat Linux` 上运行。请访问 `LinuxToys.net` 网站获取有关 `Red Hat Linux` 后续版本可能出现任何兼容性信息。

# 附录

## A 本附录中

- ☑ 获取 `Red Hat Linux` 软件
- ☑ 使用 `Linux Toys CD`
- ☑ 理解 `Linux Toys` 软件包

`Red Hat Linux` 的安装说明见附录 `C`。

![](img/93c80330322e65d5105a6014afe2d85d_302_0.png)

## Linux Toys CD

随书附的 `Linux Toys CD` 包含了 `Red Hat` 包管理（`RPM`）格式、`tar/bzip2` 格式的软件包，甚至还有软磁盘镜像。

请参考每个章节了解需要哪些 `Linux Toys` 包。通常情况下，你可以通过挂载 `CD` 并使用包含的 `install.command` 来安装所需的 `Linux Toys` 包，命令如下：

```
#### mount /mnt/cdrom
# /mnt/cdrom/ch03-ltJukebox/install.me
```

将 `ch03-ltJukebox` 修改为你正尝试安装的章节。偶尔会有额外的安装说明，这些说明将在各自的章节中详细描述。

## Linux Toys 软件包

### 第 3 章节 (`/mnt/cdrom/ch03-ltJukebox`):

- `install.me`: 项目安装脚本
- `COPYRIGHT`: 包含音乐的版权信息
- `Listen.org`: `Bill Broomall` 和 `Richard Williams` 的音乐
- `On_the_Porch.org`: `Bill Broomall` 的音乐
- `ltJukebox-1.2-3.noarch.rpm`: 主要项目包文件
- `cdddb-1.4-0.i386.rpm`: `CD` 数据库进程包
- `freedb-complete-20035071.tar.bz2`: `CD` 信息数据库
- `perl-MP3-Info-1.0-0.i386.rpm`: `CD` 命名 `PERL` 库

### 第 4 章节 (`/mnt/cdrom/ch04-VideoArchive`):

- `install.me`: 项目安装脚本
- `a52dec-0.7.4-0.i386.rpm`: 解码 `AC-3` 流的库
- `aalib-1.4rc5-fr2.i386.rpm`: `ASCII art` 低底层库
- `alsa-lib-0.9-4-fr2.i386.rpm`: 高级 `Linux` 音频架构
- `avi2vcd-1.0-0.noarch.rpm`: `Linux Toys AVI2VCD` 转换脚本
- `datafile-0.75-13.i386.rpm`: `AVI` 文件库
- `datafile-codecs-20025016-1.i386.rpm`: 二进制 `win32` 视频编码
- `div4linux-5.0.1-dag.rh73.i386.rpm`: `DivX Code 5.01`
- `faad2-1.1-fr2.20030409.i386.rpm`: 解码 `MPEG/4 AAC`
- `ffmpeg-0.4.6-0.i386.rpm`: 音频/视频瑞士军刀
- `libdv-0.99-fr2.i386.rpm`: `IEEE 1394` 视频编码
- `libdvdread-0.9.4-fr3.i386.rpm`: 读取 `DVD` 光盘的基础
- `libpostproc-0.90-fr2.i386.rpm`: `mplayer` 后处理组件
- `libquicktime-0.9.0-1.i386.rpm`: `QuickTime` 操作库
- `lirc-0.6-6-fr1.i386.rpm`: `Linux` 红外遥控器包
- `lzo-1.08-0.i386.rpm`: 无损数据压缩
- `mjpegtools-1.6.1-1.i386.rpm`: `MPEG` 音频和视频工具
- `mplayer-0.90-fr2.i386.rpm`: `Linux` 下最好的电影播放器
- `mplayer-fonts-1.0-fr1.noarch.rpm`: `mplayer` 的字体文件
- `nvrec-20030316-3.i386.rpm`: 视频采集核心
- `vcd-imager-0.6-2.i386.rpm`: `VCD-master` 和刻录工具
- `xvidcode-0.9.1-fr2.i386.rpm`: `DivX` 编码的开放实现

### 第 5 章节 (`/mnt/cdrom/cdVCR`):

- `install.me`: 项目安装脚本
- `aalib-1.45-fr2.i386.rpm`: `ASCII art` 低底层库
- `alsa-lib-0.9-3-fr2.i386.rpm`: 高级 `Linux` 音频架构
- `avifile-0.75-31.i386.rpm`: `AVI` 文件库
- `avifile-codecs-2003016-1.i386.rpm`: 二进制 `win32` 视频编码
- `div4linux-5.01-dag.rh73.i386.rpm`: `DivX Code 5.01`
- `faad2-1.1-fr2.20030409.i386.rpm`: 解码 `MPEG/4 AAC`
- `ffmpeg-0.4.6-0.i386.rpm`: 音频/视频瑞士军刀
- `libdv-0.99-fr2.i386.rpm`: `IEEE 1394` 视频编码
- `libdvdread-0.9.4-fr3.i386.rpm`: 读取 `DVD` 光盘的基础
- `libpostproc-0.90-fr2.i386.rpm`: `mplayer` 后处理组件
- `libquicktime-0.9.0-1.i386.rpm`: `QuickTime` 操作库
- `lirc-0.6-6-fr1.i386.rpm`: `Linux` 红外遥控器包
- `lzo-1.08-0.i386.rpm`: 无损数据压缩
- `mplayer-0.90-fr2.i386.rpm`: `Linux` 下最好的电影播放器
