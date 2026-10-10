

# 安装 Guest Additions

为了让你的虚拟机能够使用 USB 设备和其他系统工具，你需要在 Kali 虚拟机中安装 VBox Guest Additions。（请在开始之前确保已按照上述步骤更新了系统）。没有可选步骤，因此在继续之前，请确保你能成功完成这些操作。

要检查 Linux 内核头文件，你需要找到当前以 -kali-all-amd64 结尾的 linux-headers。版本会随时间变化。

![](img/5481504809e843668406e46c502c72ab_39_0.png)

当你输入 `apt-cache search header | grep -i linux` 时，这将生成一个列表（如果已正确更新）。寻找那个以 -kali-all-amd64 结尾的项目。

![](img/5481504809e843668406e46c502c72ab_39_1.png)

![](img/5481504809e843668406e46c502c72ab_39_2.png)

安装 Linux 内核头文件。撰写本文时，版本为 4.5，但这会发生变化，因此请输入你在执行 `apt-cache search header | grep -I linux` 时看到的版本，并使用 **apt-get install linux-headers-4.5.0-kali-all-amd64** 进行安装。

完成后（以防万一），运行 **apt-get update && apt-get upgrade -y**（可能没有可更新的内容，但检查总是好的），然后在终端中输入 **reboot**。

重新登录到 Kali，点击“设备”（Devices），点击“插入 Guest Additions CD 镜像”（Insert Guest Additions CD image）。

![](img/5481504809e843668406e46c502c72ab_40_0.png)

你应该会看到一个 CD 图形和一个“运行”选项。当你点击“运行”时，它会失败。

![](img/5481504809e843668406e46c502c72ab_40_1.png)

![](img/5481504809e843668406e46c502c72ab_41_0.png)

只需点击确定即可。

然后返回终端，导航到你刚刚挂载的介质。输入 `cd /media/cdrom0`，然后输入 `ls` 以验证文件 `VBoxLinuxAdditions.run`。

![](img/5481504809e843668406e46c502c72ab_41_1.png)

你需要将此文件复制到桌面以便运行它。输入 `cp VBoxLinuxAdditions.run /root/Desktop`（请记住这是区分大小写的）。

![](img/5481504809e843668406e46c502c72ab_42_0.png)

![](img/5481504809e843668406e46c502c72ab_42_1.png)

![](img/5481504809e843668406e46c502c72ab_42_2.png)

导航回根目录并输入 `cd Desktop`（记住大写 D），然后输入 `ls` 以验证你看到了它。现在通过输入 `./VBoxLinuxAdditions.run` 来运行该文件（你可以复制 & 粘贴）。

![](img/5481504809e843668406e46c502c72ab_43_0.png)

你的 Kali 虚拟机已准备就绪，祝使用愉快！

# 资源

- [VBOX & Guest Additions](https://www.virtualbox.org/wiki/Downloads)
- [Kali ISO](https://www.kali.org/downloads/)
- [TOR 浏览器](https://www.torproject.org/)
- [用于你源文件的 Kali 软件库](http://docs.kali.org/general-use/kali-linux-sources-list-repositories)
- [Kali 文档](http://docs.kali.org/)
- [什么是 BIOS](https://en.wikipedia.org/wiki/BIOS)

## 建议具备的条件：

- 家用路由器，或邻居的许可，以便你研究它们
- 旧版 Windows PC 用于攻击，或带有 Windows（未打补丁以查看丑陋部分）的虚拟机

# 更多课程书籍

![](img/5481504809e843668406e46c502c72ab_45_0.png)

https://www.amazon.com/dp/B013JB351K/

![](img/5481504809e843668406e46c502c72ab_45_1.png)

https://www.amazon.com/dp/B01M15T2GG/

