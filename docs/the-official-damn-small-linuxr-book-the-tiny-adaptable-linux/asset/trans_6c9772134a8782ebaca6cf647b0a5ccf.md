

## 在 DSL 中设置 ALSA 声音

要确保你的声音系统在 DSL 中正常工作并设置音量级别，你可以使用随 DSL 提供的多个应用程序，或使用 MyDSL 轻松添加。在 DSL 中使用 Skype 时，特别需要高级 Linux 声音架构（ALSA）声音系统，以及 gnu-utils 包（ALSA 所需）。

开始此操作前，启动 DSL。你可以直接从 DSL live CD 启动，或从你偏好的任何介质启动（U盘、硬盘等）。

由于我假设你希望在 DSL 中持久地设置 Skype 以使其工作（而不是在重启后消失），以下流程描述了如何获取 Skype 声音所需的扩展，并在重启时重新加载它们。具体操作如下：

- 1. 在开始下载 DSL 扩展之前，先确定要将它们保存到何处以供将来使用。例如，挂载一个硬盘分区或插入的 USB 闪存驱动器（U盘），使其准备好保存你的扩展。然后，在该设备的根目录下创建一个 mydsl 目录。以U盘为例，你可能需要在具有 root 权限的终端窗口中输入以下内容：
  
      `# mkdir /mnt/sda1/mydsl`

> **注意**
> 
> 如果你的电脑是 Windows 系统，那么你的硬盘分区很可能格式化为 NTFS 文件系统。如果你的电脑就是这种情况，你需要使用 USB U盘，创建一个其他类型的硬盘分区（如 FAT32 或 ext3），或重新制作 CD（见第 4 章“配置和保存 DSL 设置”所述）来保存所需的软件包。DSL 不支持写入 NTFS 文件系统。

- 2. 从 DSL 桌面选择 MyDSL 图标。
- 3. 选择 UNC 并选择 ALSA 软件包。
- 4. 阅读 ALSA 软件包的描述。请注意，ALSA 软件包需要安装 gnu-utils 软件包（我们接下来会获取）并且需要一个 ALSA 启动选项才能工作。
- 5. 选择下载。弹出窗口会询问要将软件包安装到何处。
- 6. 在提示时，指定你希望 ALSA 软件包下载到的位置。默认使用 `/tmp` 目录。如果你想保存到U盘，则可以输入 /mnt/sda1/mydsl 代替。选择下载，你可以观看进度，软件包将被下载并安装。
- 7. 选择 UNC 并选择 gnu-utils 软件包。
- 8. 阅读 gnu-utils 软件包的描述。
- 9. 选择下载。弹出窗口会询问要将软件包安装到何处。
- 10. 在提示时，指定你希望 gnu-utils 软件包下载到的位置。默认使用 /tmp 目录。相反，你应该输入 /mnt/sda1/mydsl 以将扩展保存到U盘。选择下载，你可以观看进度，软件包将被下载并安装。
- 11. 打开一个终端窗口（右键单击桌面并选择 XShells, Root Access, Dark）并输入以下命令以启动 ALSA 声音系统：

```
# alsa_snddevices
# alsa_init
```

alsa_snddevices 命令创建 ALSA 工作所需的音频组和声音设备（在 /dev 中）。alsa_init 命令启动 ALSA 服务。你的 ALSA 声音系统现在应该正在运行。

接下来，你可以尝试在 DSL 中调整音频：

- 1. 启动音频混音器—通过右键单击桌面并选择 Apps→ Sound/MPEG/VoIP→ Dmix Sound Mixer 来启动 DMix 以调整音量级别。
- 2. 调整音频输出—在 DMix 窗口中，选择 Master Volume。然后，移动滑块以调整左右声道的音频级别。
- 3. 调整音频输入—在 DMix 窗口中，选择你的输入设备名称（可能是 Microphone、Phone Input 或 Line In）。点击 Rec 按钮（使按钮打开），以将麦克风选为录音设备。向上移动滑块以调整音频输入级别。
- 4. 播放声音—你可以在测试声音输出的同时检查你的 Internet 连接，通过启动 XMMS 播放流媒体电台。右键单击桌面并选择 Apps→ Sound/MPEG/VoIP→ XMMS→ Xmms News Feeds→ Xmms “KCPW NPR NEWS”。流媒体音频应该在你的耳机中播放。

此时，你可以关闭 DMix 和 XMMS 窗口。如果你的声音系统仍然无法工作，请参阅本章末尾附近的 Troubleshooting Skype 部分，了解调试问题的建议。

