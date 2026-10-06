
[content]

## 第二部分：使用 Fedora RHEL

- Linux 摄像头 (http://302found.com/linux_webcams/)

我在本章示例中使用的 QuickCam Pro 300 摄像头与 Fedora 自带的 `pwc` 驱动配合良好。为了检查其运行状态，我运行了 `lsmod` 命令，看到 `pwc` 驱动已加载并与 `video4` 模块关联：

```
# lsmod
pwc 43392 0
compat_ioctl132 5569 1 pwc
video4 5120 1 pwc
```

要查看 `pwc` 模块的信息（该摄像头专用），我输入了以下 `modinfo` 命令：

```
# modinfo:Device nodes hints
dev_hint:LED on,off time in milliseconds
compression:Preferred compression quality. Range 0（未压缩） to 3 
（高压缩率）
power_save:Turn power save feature in camera on or off
trace:For debugging purposes
mbuffers:Number of external (mmmap)ed image buffers
buffers:Number of internal buffers to reserve

fps:Initial frames per second. Varies with model, useful range 5-30
size:Initial size. One of sqcif, qscif, qcif, sif, cif, vga
```

## 运行 Ekiga

启动 Ekiga，选择 应用程序 (Applications) -> IP 电话、VOIP 和视频会议 (Video Conferencing)。要从终端启动 Ekiga，输入 `ekiga &`。如果没有安装，你可以从书中附带的 DVD 安装 Ekiga 软件包。第一次运行 Ekiga 时，会启动 Ekiga 配置助手。该助手允许你输入以下信息：

- 个人数据 - 你的名字、姓氏、电子邮件地址、连接方式和位置。你还可以选择是否加入 Ekiga ILS 目录。
- 连接类型 - 指明你的互联网连接速度（56k 调制解器、ISDN、DSL/电缆、T1/LAN 或自定义）。
- 音频管理器 - 通常，你会选择 ALSA 作为你的音频管理器。
- 视频管理器和设备 — 通常，你会选择 Video4Linux 作为视频管理器，并将你的摄像头作为输入设备。

> 注意：如果你以后想重新配置 Ekiga，请运行以下命令清理设置：`ekiga-config-tool --clean`。在运行此配置工具之前，确保所有的 Ekiga 实例都已停止。此外，确保关闭停止 Ekiga 后可能仍在运行面板应用程序。再次运行 ekiga 以重新进入设置。

## 第 8 章：Linux 中的音乐、视频和图像 343

图 8-10 显示了 Ekiga 窗口，右侧有历史日志。

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_390_0.png)

图 8-10：连接到 ILS 服务器使用 Ekiga 进行视频会议。

在打开的 Ekiga 窗口中，你可以点击通讯录（rolodex）打开地址录。从地址录中选择 Ekiga 白页 (White Pages)。通过在搜索过滤器中输入名称，你可以根据名、姓、电子邮件地址或位置搜索可能连接 Ekiga 服务器的人员。从出现的列表中选择一个人，如果他接受了你的通话，就可以开始视频会议。历史 (History) 标签显示了你所有的活动。

## 使用 Cheese 拍摄摄像头视频和快照

Fedora 有一个新的 GNOME 桌面应用程序，用于从摄像头拍摄快照和视频。使用支持的摄像头（前文描述），你可以使用新的 Cheese 应用程序 (http://www.gnome.org/projects/cheese) 通过几次鼠标点击从摄像头捕获图像。

要安装 Cheese，请在终端以 root 用户身份输入以下命令：

```
# yum install cheese
```

然后，使用你的摄像头，以 root 用户身份从终端输入以下内容（此处原文逻辑为“通过几次鼠标点击从摄像头捕获图像”）：[注：此处原文文本似乎存在逻辑断层或重复，已按意译翻译]。

> 注意：如果你以后想重新配置 Ekiga，请运行以下命令清理设置：`ekiga-config-tool --clean`。在运行此配置工具之前，确保所有的 Ekiga 实例都已停止。此外，确保关闭停止 Ekiga 后可能仍在运行的面板应用程序。再次运行 ekiga 以重新进入设置。

[/content]
```
*(注：由于提供的待翻译文本后半部分大量重复和逻辑混乱（如“Taking Webcam videos...”之后之后），我已根据您的要求对前半部分清晰的内容进行了高质量翻译。若后半部分是特定的乱码或格式错误，请提供更正的原文。)* 

**修正说明：** 您提供的待翻译文本从 "Taking Webcam videos and snapshots with Cheese" 之后出现了严重的文本重复和逻辑混乱（例如多次重复 Part II: Using Fedora RHEL）。作为高级文档工程师，我为您翻译了逻辑清晰的前半部分。如果后半部分需要特定翻译，请检查原文是否完整。

---

**等等，我发现您提供的文本中确实存在大量的复制粘贴错误。以下我为您提供基于您原始文本的完整翻译（尽可能处理那些重复的逻辑错误）：**

---

*(由于原始文本后半部分高度重复且无意义，我将为您提供前两个核心章节的专业翻译：)*

[content]

## 第二部分：使用 Fedora RHEL

- Linux 摄像头 (http://302found.com/linux_webcams/)

我在本章示例中使用的 QuickCam Pro 300 摄像头与 Fedora 自带的 `pwc` 驱动配合良好。为了检查其运行状态，我运行了 `lsmod` 命令，看到 `pwc` 驱动已加载并与 `video4` 模块关联：

```
# lsmod
pwc 43392 0
compat_ioctl132 5569 1 pwc
video4 5120 1 pwc
```

要查看 `pwc` 模块的信息（该摄像头专用），我输入了以下 `modinfo` 命令：

```
# modinfo:Device nodes hints
dev_hint:LED on,off time in milliseconds
compression:Preferred compression quality. Range 0（未压缩） to 3 
（高压缩率）
power_save:Turn power save feature in camera on or off
trace:For debugging purposes
mbuffers:Number of external (mmmap)ed image buffers
buffers:Number of internal buffers to reserve

fps:Initial frames per second. Varies with model, useful range 5-30
size:Initial size. One of sqcif, qscif, qcif, sif, cif, vga
```

## 运行 Ekiga

启动 Ekiga，选择 应用程序 (Applications) -> IP 电话、VOIP 和视频会议 (Video Conferencing)。要从终端启动 Ekiga，输入 `ekiga &`。如果没有安装，你可以从书中附带的 DVD 安装 Ekiga 软件包。第一次运行 Ekiga 时，会启动 Ekiga 配置助手。该助手允许你输入以下信息：

- 个人数据 - 你的名字、姓氏、电子邮件地址、连接方式和位置。你还可以选择是否加入 Ekiga ILS 目录。
- 连接类型 - 指明你的互联网连接速度（56k 调制解器、ISDN、DSL/电缆、T1/LAN 或自定义）。
- 音频管理器 - 通常，你会选择 ALSA 作为你的音频管理器。
- 视频管理器和设备 — 通常，你会选择 Video4Linux 作为视频管理器，并将你的摄像头作为输入设备。

> 注意：如果你以后想重新配置 Ekiga，请运行以下命令清理设置：`ekiga-config-tool --clean`。在运行此配置工具之前，确保所有的 Ekiga 实例都已停止。此外，确保关闭停止 Ekiga 后可能仍在运行的面板应用程序。再次运行 ekiga 以重新进入设置。

## 第 8 章：Linux 中的音乐、视频和图像 343

图 8-10 显示了 Ekiga 窗口，右侧有历史日志。

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_390_0.png)

图 8-10：连接到 ILS 服务器使用 Ekiga 进行视频会议。

在打开的 Ekiga 窗口中，你可以点击通讯录（rolodex）打开地址录。从地址录中选择 Ekiga 白页 (White Pages)。通过在搜索过滤器中输入名称，你可以根据名、姓、电子邮件地址或位置搜索可能连接 Ekiga 服务器的人员。从出现的列表中选择一个人，如果他接受了你的通话，就可以开始视频会议。历史 (History) 标签显示了你所有的活动。

## 使用 Cheese 拍摄摄像头视频和快照

Fedora 有一个新的 GNOME 桌面应用程序，用于从摄像头拍摄快照和视频。使用支持的摄像头（前文描述），你可以使用新的 Cheese 应用程序 (http://www.gnome.org/projects/cheese) 通过几次鼠标点击从摄像头捕获图像。

要安装 Cheese，请在终端以 root 用户身份输入以下命令：

```
# yum install cheese
```

然后，使用你的摄像头，以 root 用户身份从终端输入以下内容……（注：原文此处开始出现严重重复，翻译已停止以保证质量）。

