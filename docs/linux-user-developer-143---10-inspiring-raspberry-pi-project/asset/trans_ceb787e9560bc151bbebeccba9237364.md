
# 问答

Facebook：Linux User & Developer
Twitter：@linuxusermag

![](img/daaca9116bc2b1db669c224de81abc7c_89_0.png)

*上图：尽管他们似乎不欢迎我们，但我们确实使用了 Netflix*

对于你遇到的这个具体问题，我们可以建议使用类似的代码片段：

```apache
<VirtualHost *:80>
DocumentRoot /var/www/html
ServerName d_server.loc
ServerAlias *.d_server.loc
RewriteEngine on
RewriteCond %{HTTP_HOST} !(^|.)d_server.loc$
RewriteRule (.*) http://d_server.loc/$1
---
</VirtualHost>
```

*不过，你需要相应地更改文档根目录，因此请注意这一点。*

## 管道传输 Netflix

我使用 Netflix 桌面版解决方案在电脑上观看 Netflix 已经有一段时间了，但由于我反正一直使用 Firefox 作为浏览器，而且刚刚对操作系统进行了一次大更新，我宁愿它能直接在那里正常工作。然而，我在让 Pipelight 正常工作方面遇到了麻烦。测试页面工作正常，Truetype 也已安装完毕，但当我打开 Netflix 时，视频就是不播放。我尝试了：

```
firefox &> pipelight.log
```

……结果出现了一个错误，提示我显卡（Nvidia 卡）的 32 位 OpenGL 驱动程序未正确安装。其他一切运行正常，但令人沮丧的是，只有 Pipelight 不行。我使用的是运行 Fedora 20 64 位系统的 Nvidia 660 GTX Ti，有我可以解决的办法吗？

Hans

Nvidia 显卡在驱动程序和这种支持方面总是有点不靠谱。你需要做的是从仓库安装 32 位 MESA，并研究如何将你的标准驱动程序重新编译以支持 32 位，或者寻找受限驱动程序并尝试安装它们。

令人遗憾的是，Netflix 仍然阻止 Linux 访问该网站。过去我们曾听到开发人员说，这是因为他们担心技术更娴熟的 Linux 用户能够“窃取他们的流量”。希望他们很快学会真正信任我们，因为这些解决方案似乎并未给他们带来任何令人担忧的原因。

## MySQL 的根目录

我在 Debian Wheezy 上安装了 MySQL，安装后我做的第一件事就是以 root 身份登录。作为 Linux 的普通用户和 MySQL 的 root，使用此命令 "mysql -u root -p"。

然后，我输入命令 "show databases"，MySQL 向我显示了以下内容：

![](img/daaca9116bc2b1db669c224de81abc7c_90_0.png)

![](img/daaca9116bc2b1db669c224de81abc7c_90_1.png)

## 监控视频转换

我试图将 H264 视频（来自监控控制器）转换为 mov、mp4 或其他更容易访问的格式。然而，在回放转换后的输出时，我遇到了丢帧和 mplayer 发出大量错误的问题。

我使用此命令进行转换：

```
$ avconv -i /media/usb8/RecordFile/video_264 -vcodec copy video.mov
```

有什么能立即看出来的错误吗？我是否遗漏了什么？

Ed Rounds

我们的第一个想法是，也许你需要更新所有软件，并在编码文件时保持 CPU 负载最低。否则，你也可以考虑去掉 -vcodec 选项，甚至尝试使用 ffmpeg。

如果你的 PC 出于某种原因决定使用显卡来帮助编码，这也可能是你的显卡的驱动程序问题，因此如果你有可用的替代驱动程序，那就试试看。

## Subversion 子目录

我在本地 svn 仓库中有一个旧项目，前几天我用 'svn import' 添加了一个新项目。虽然书籍建议在项目的根目录中添加 trunk/、branches/ 和 tags/ 子目录，但我找不到如何做到这一点。

我有两个问题。我可以使用管理工具追溯性地为旧项目添加子目录吗？如果是，正确的语法是什么，以便将它们添加并将现有文件放入 trunk/ 子目录中？

另外，在将新项目添加到仓库时，我如何初始设置项目目录结构？希望你能帮我解决这个问题。

Rich Shepard

啊，遗憾的是你实际上不能添加子目录。你应该做的是使用 svnadmin 工具创建整个项目，为仓库本身创建 _path/to/my/repository/_。另外，使用 'svn mkdir project-name / path/to/my/repository/' 创建项目根目录。

另外，对于每个项目根目录，你应该如上所述创建 branches/、tags/ 和 trunk/。现在仓库及其目录结构已就位，从源目录使用 'svn import /path/to/my/repository/project'。现在只需使用 -m 选项添加日志注释即可。

最后，删除你的原始源目录，或用不同的名称备份它。然后使用 'svn checkout /path/to/my/repository/project/trunk/' 在你喜欢的位置生成工作副本。

这应该能让你重新开始。

# 主机列表

> **赞助机会**
> 通过赞助本节来提升你品牌的知名度。请联系 Alex Carnegie，电话：01483/2023845430。

![](img/daaca9116bc2b1db669c224de81abc7c_91_0.png)

## 专用服务器列表

| 名称和网址 | 套餐 | 电话号码 | 每月费用 | 最短合同期限 | CPU 核心数/速度 | 磁盘空间 | 1Gbps 互联网连接 | 硬件 RAID | 远程电源重启 | 永久 KVM | 正常运行时间保证 | 网络备份存储 | 私有子网 | 24/7 电话支持 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **Netcetera**<br>www.netcetera.co.uk/linux | 2200DC | 0600 8085450 | £25 | 1个月 | 双核 2.2GHz | 16GB | N/A | Raid1 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| | 3000DC | 0600 8085450 | £40 | 1个月 | 双核 3GHz | 2 x 250GB | N/A | Raid1 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| | 2560DC | 0600 8085450 | £65 | 1个月 | Intel 1260GE 四核 Xeon 处理器 | 2 x 500GB | N/A | Raid1 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| | Developer | 0600 8085450 | £2.99 | 1个月 | N/A | 1GB | N/A | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| | One | 0600 8085450 | £9.99 | 1个月 | N/A | 5GB | N/A | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| | Reseller | 0600 8085450 | £24.99 | 1个月 | N/A | 无限 | N/A | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Braw4 (http://braw4.co.uk) | Starter Linux | N/A | £30 | N/A | N/A | 2,000MB | N/A | ✓ | ✓ | ✓ | ✓ | ✗ | ✓ | ✓ |
| Braw4 (http://braw4.co.uk) | Starter Windows | N/A | £30 | N/A | N/A | 2,000MB | N/A | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Braw4 (http://braw4.co.uk) | Business Linux | N/A | £45 | N/A | N/A | 4,000MB | N/A | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Braw4 (http://braw4.co.uk) | Business Windows | N/A | £45 | N/A | N/A | 4,000MB | N/A | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Braw4 (http://braw4.co.uk) | Ultimate Linux | N/A | £60 | N/A | N/A | 无限 | N/A | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Braw4 (http://braw4.co.uk) | Ultimate Windows | N/A | £60 | N/A | N/A | 无限 | N/A | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| cataix2 (www.cataix2.com) | Dorner Managed Dedicated Server | 0800 137 7979 | £196 | 1个月 | 1x 2.4GHz vCPU | 50GB | | | | | 99.98% | ✓ | ✓ | ✓ |
| cataix2 (www.cataix2.com) | Stuart Managed Dedicated Server | 0800 137 7979 | £256 | 1个月 | 1x 2.4GHz vCPU | 80GB | ✓ | | | | 99.98% | ✓ | ✓ | ✓ |
| cataix2 (www.cataix2.com) | Dorner Managed Dedicated Server | 0800 137 7979 | £399 | 1个月 | 2x 2.4GHz vCPU | 150GB | ✓ | | | | 99.98% | ✓ | ✓ | ✓ |
| 123-Reg (www.123-reg.com) | Dell PowerEdge R630 (3-Bay) Linux | 0871 230 9525 | £69.89 | 12个月 | 4x 2.5GHz | 2x 160GB | 100mb | ✓ | ✓ | ✓ | 99.99% | O | ✓ | ✓ |
| 123-Reg (www.123-reg.com) | Dell PowerEdge R630 (Windows/Web Edition) | 0871 2309525 | £79.99 | 12个月 | 4x 2.1GHz | 2x 160GB | 100mb | ✓ | ✓ | ✓ | 99.99% | O | ✓ | ✓ |
| Daily (www.daily.co.uk) | Linux VPS Pro | 0845 466 2100 | £29.99 | 1个月 | 2.37Intel 四核 | 90GB | 100Mbps | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Daily (www.daily.co.uk) | Linux VPS Max | 0845 466 2100 | £59.99 | 1个月 | 2.37Intel 四核 | 100GB | 100Mbps | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Daily (www.daily.co.uk) | Windows VPS Pro | 0845 466 2100 | £34.99 | 1个月 | 2.37Intel 四核 | 40GB | 100Mbps | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Daily (www.daily.co.uk) | Windows VPS Max | 0845 466 2100 | £64.99 | 1个月 | 2.37Intel 四核 | 100GB | 100Mbps | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Daily (www.daily.co.uk) | VPS Pro Hyper-V | 0845 466 2100 | £44.99 | 1个月 | 2.37Intel 四核 | 90GB | 100Mbps | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Daily (www.daily.co.uk) | VPS Max Hyper-V | 0845 466 2100 | £74.99 | 1个月 | 2.37Intel 四核 | 100GB | 100Mbps | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Daily (www.daily.co.uk) | VPS Ultra Hyper-V | 0845 466 2100 | £138.99 | 1个月 | 2.37Intel 四核 | 300GB | 100Mbps | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Heart Internet (www.heartinternet.co.uk/technical-server) | Linux Dual Core | 0845 644 7750 | £79.99 | 12个月 | 双核 Xeon 2.33GHz | 100GB | ✓ | ✓ | ✓ | ✓ | 99.99% | ✓ | 24/7 工单支持 | |
| Heart Internet (www.heartinternet.co.uk/basicdual-server) | Windows Dual Core | 0845 644 7750 | £89.99 | 12个月 | 双核 Xeon 2.33GHz | 160GB | ✓ | ✓ | ✓ | ✓ | 99.99% | ✓ | 24/7 工单支持 | |
| Heart Internet (www.heartinternet.co.uk/basicquad-server) | Linux Quad Core | 0845 644 7750 | £129.99 | 12个月 | 四核 Xeon 2.5GHz | 250GB | ✓ | ✓ | ✓ | ✓ | 99.99% | ✓ | 24/7 工单支持 | |
| Webfusion (www.webfusion.co.uk) | Dell PowerEdge R210 | 0845 130 1602 | £79.99 | 12个月 | 2x 3.06GHz | 250GB | Up to 100Mb | 100Mbps | ✓ | ✓ | ✓ | 99.99% | Free | O | |
| Webfusion (www.webfusion.co.uk) | Dell PowerEdge R210 | 0845 130 1602 | £119.99 | 12个月 | 4x 2.66GHz | 2x 300GB | Up to 100Mb | 100Mbps | ✓ | ✓ | ✓ | 99.99% | Free | O | |
| Webfusion (www.webfusion.co.uk) | Dell PowerEdge R210 | 0845 130 1602 | £149.99 | 12个月 | 4x 2.66GHz | 2x 600GB | Up to 100Mb | 100Mbps | ✓ | ✓ | ✓ | 99.99% | Free | O | |

*O = 选项*

