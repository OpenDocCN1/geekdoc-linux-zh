
`ls -1 /root/anaconda-ks.cfg`

```
- 2. 接下来，物理插上 USB 设备，然后输入以下命令，这将为您提供当前连接到计算机的所有硬盘设备列表：
```

`fdisk -l`

```
- 3. 尝试通过比较其大小、分区和识别的文件系统与您的 USB 设备来识别设备名称。通常为 `/dev/sdx`，其中 x 是字母，如 b, c, d ... 等。如果您无法使用 `fdisk` 找到 USB 介质的正确设备名称，请尝试以下技巧：运行两次 `fdisk`——一次在未拔出运行时，另在拔出运行时，第二次输出比第一次输出多出一个设备名称；那这就是您的设备名称！
- 4. 如果您在列表中找到了设备名称，请创建一个目录将其挂载到当前文件系统：
```

`mkdir /mnt/kickstart-usb`

```
- 5. 接下来，将 USB 设备实际挂载（假设您的 USB 设备是 `/dev/sdcl`）：
```

`mount /dev/sdcl /mnt/kickstart-usb`

```
- 6. 现在我们在 USB 设备上创建 kickstart 文件的副本：
```

`cp /root/anaconda-ks.cfg /mnt/kickstart-usb`

```
- 7. 接下来，使用您喜欢的文本编辑器打开 USB 设备上的副本（此处使用 nano，如果尚未安装，请运行 `yum install nano`）：
```

`nano /mnt/kickstart-usb/anaconda-ks.cfg`

```
- 8. 我们现在修改文件以安装 CentOS。在 nano 中，使用上下方向键移动到 `<your_hostname>` 行，这将是您在安装期间指定的主机名：
```

`network --hostname=<your_hostname>`

```

- 9. 现在编辑 `<your_hostname>` 字符串以赋予唯一主机名。例如，在末尾添加 -2，所示：
```

`network --hostname=minimal-2`

```

- 10. 使用上下方向键移动光标直到到达 `packages` 行。在其下方添加以下行（您可以进一步自定义并提供想要安装的软件包）：
```

`mariadb-server`

`httpd`

`sync`

`net-tools`

```
- 11. 现在保存并关闭文件，在 nano 编辑器中，使用键组合 Ctrl+O（这意味着按住键盘上的 Ctrl 键然后按 o）来写入更改。按 Return 确认文件名并按 Ctrl+x 退出编辑器。
- 12. 接下来，安装 CentOS 包：
```

`yum install --config-kickstart`

```
- 13. 现在使用 validator 程序验证 kickstart 文件，它包含在刚刚安装的软件包中：
```

`validator /mnt/kickstart-usb/anaconda-ks.cfg`

```
- 14. 如果配置文件无误，使用以下命令取消挂载 USB 设备：
```

`cd`

`umount /mnt/kickstart-usb`

```
- 15. 当再次获得新的命令提示符时，拔掉带有 kickstart 文件的 USB 设备，供目标机器物理使用。
- 16. 现在您需要物理访问目标机器以插入您的 CentOS 安装介质（必须是在 CD/DVD 光盘或 USB 安装设备上准备的 CentOS DVD 或 Everything 安装磁盘镜像）。
- 17. 接下来，启动服务器并在初始启动屏幕上按下正确的键，与启动刚刚连接的 CentOS 安装介质相关。
```

## 安装 CentOS

19. 在 CentOS 安装程序开始加载后，将显示标准的 CentOS 7 安装欢迎界面，光标将预选“Test this media & install CentOS 7”（测试此媒体并安装 CentOS 7）选项。

20. 接下来，按下键盘上的 `Esc` 键切换到启动提示符（`boot: prompt`）。

21. 我们已准备好开始 kickstart 安装。要执行此操作，您需要知道存放 kickstart 文件的 USB 设备上的确切分区名称。输入以下命令，假设您的分区位于 `/dev/sdc1`（根据需要进行更改），并按回车键启动 kickstart 安装过程：

```
linux ks=hd=sdc1:anaconda/ks.cfg
```
