
`time` 命令以“分钟.秒”格式显示三个结果：从程序开始到结束的实际经过时间、程序作为用户运行的时间，以及程序作为系统运行的时间。

- 8. 输入 `time ./rpm- --version` 并按回车，查看未压缩程序运行所需的时间。你可能会发现花费的时间更短。

你可以使用 `gzexe` 命令的 `-d` 选项将压缩程序恢复到原始未压缩状态。

- 9. 输入 `rpm*` 并按回车删除你创建的两个 rpm 文件。按 y 然后按回车确认每次删除。

- 10. 如果你要继续进行下一个实验，请注销并切换到 GUI；否则，关闭计算机。

### 复习题

- 1. 哪个命令可以压缩 Linux 二进制程序并允许以压缩格式运行？
  a. gzip
  b. compress
  c. gzexe
  d. rpm

- 2. 当你使用 `time cp /bin/rpm ./` 命令时，输出 `real 0.100s` 的含义是什么？
  a. cp 程序运行了 1.1 分钟，使用实时优先级。
  b. cp 程序花费了 1.1 秒完成运行。
  c. rpm 程序花费了 1.1 秒完成运行。
  d. time 程序花费了 1 分钟 1 秒运行 cp 程序。

- 3. 压缩后的二进制程序加载速度与相同的未压缩程序一样快。对或错？

- 4. `gzexe` 命令允许你将压缩程序转换回原始未压缩状态。对或错？

- 5. 如果一个程序运行 2 小时，`time` 命令会显示什么结果？
  a. 2h.0m.000s
  b. 1h.60m.000s
  c. 120m0.000s
  d. 2h.0m

## 实验 11.2 压缩图像文件

### 目标

在本实验中，你将下载 ImageMagick 软件包并使用 `convert` 命令压缩位图图像文件并转换为 JPEG 格式，这对于发布在 Web 网页上或通过电子邮件或互联网发送图像非常有用。你还可以使用 `convert` 将 JPEG 图像文件从彩色转换为灰度模式，并比较压缩文件与未压缩文件的文件大小和图像质量。

### 所需材料

- 本实验需要：
- 一台运行 Fedora 20 Linux 的计算机
- 一个位图图像（详情见具体步骤）

预计完成时间：20 分钟

### 活动步骤

- 1. 如必要，以 User1 登录 GUI 并打开一个终端窗口。

- 2. 如果你安装了 Libre-Office。本实验使用的位图图像应该已经存在于你的系统中。输入 `cp /usr/share/libreoffice/4/share/sample/sample/image.bmp ~/` 并按回车，将位图图像复制到你的主目录。

- 3. 输入 `ls -l *.bmp` 并按回车查看位图文件。输入 `file image.bmp` 并按回车查看文件类型。

- 4. 输入 `convert image.bmp image.jpg` 并按回车将位图转换为 JPEG。输入 `ls -l *.jpg` 并按回车查看文件大小。

- 5. 输入 `file image.jpg` 并按回车查看文件类型。你会看到类似下面的输出：
image.jpg: JPEG image data, 800x 600, 2 color, progressive, standard

- 6. 输入 `./image.jpg` 并按回车查看图像。你可以使用图像查看器查看它。接下来，输入 `./image.bmp` 并按回车。你会看到未压缩文件 (image.bmp) 和压缩文件 (image.jpg) 都可以工作。

- 7. 输入 `convert image.bmp -gray gray.jpg` 并按回车将图像转换为灰度。输入 `./gray.jpg` 并按回车查看结果。

- 8. 输入 `ls -l *.jpg` 并按回车查看文件大小。你会发现灰度版本的文件更小。

- 9. 输入 `file image.jpg` 并按回车查看文件类型。

- 10. 关闭所有窗口。如果你计划继续进行下一个实验，请保持登录；否则，关闭计算机。

### 复习题

- 1. 哪个命令可以告诉你扩展名为 .bmp 的文件是否真的是位图？
  a. ls -file
  b. bmp
  c. file
  d. ls -1 * | grep bmp

- 2. ImageMagick 软件包中的哪个命令可以将位图转换为压缩图像文件？
  a. file
  b. bmpcvt
  c. convert
  d. jpeg

- 3. 灰度 jpeg 文件通常比彩色 bmp 文件大。对或错？

- 4. 写出列出具有 jpeg 扩展的文件及其文件大小的命令。

- 5. 为什么你可能将位图文件转换为 jpeg？
  a. 为了保持最佳质量
  b. 为了节省空间和带宽
  c. 为了图像显示更多颜色
  d. 为了允许文件在 Windows 中显示

## 实验 11.3 安装和卸载软件包

### 目标

大多数 Linux 发行版使用 Red Hat 包管理器 (RPM) 来安装和卸载软件。你将使用 `rpm` 对已安装的软件包进行基本查询，然后使用 `yum` 执行安装和其他软件包管理任务。`yum` 程序与 `rpm` 软件包配合工作并使用互联网上的仓库。在本实验中，你将学习如何执行以下操作：

- 显示所有已安装的软件包
- 使用 yum 安装软件包
- 查看已配置的软件包仓库
- 卸载软件包

### 所需材料

本实验需要以下材料：

- 一台运行 Fedora 20 Linux 的计算机
- Fedora 20 安装 DVD

预计完成时间：15 分钟

### 活动

1. 按下 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，并以 root 用户身份登录。

2. 要查看计算机上安装的所有软件包列表，输入 `rpm -qa` 并按 `Enter`。注意，它们不是按字母顺序列出的。若要按字母顺序排序并一次显示页，输入 `rpm -qa | sort | more` 并按 `Enter`。检查完列表后，按 `q` 退出 more。要检查是否安装了名为 cracklib 的软件包，输入 `rpm -qa | grep cracklib` 并按 `Enter`。如果已安装，你将看到几行包含字符串 `cracklib` 的输出。使用相同的方法检查名为 rdesktop 的软件包。你不应该看到任何输出，因为该软件包未安装。

3. 输入 `rpm -qa | grep x*` 并按 `Enter`。你将看到所有以 x 开头的已安装软件包。接下来，你将使用 yum，它同样可以与 rpm 软件包配合工作。

4. 输入 `yum search rdesktop` 并按 `Enter`。你将看到列出软件包名称和描述的输出。

5. 输入 `yum list rdesktop` 并按 `Enter` 以查看该软件包的详细版本信息。在列表中，寻找以 Repo: 开头的行。这是可以找到 rdesktop 软件包的仓库。

6. 要查看 yum 用于查找软件包的仓库列表，输入 `yum repolist` 并按 `Enter`。这显示了 yum 使用的仓库的基本信息。

7. 若要获取更详细的仓库信息，输入 `yum repoinfo` 并按 `Enter`。你将看到仓库的详细信息，包括访问每个仓库所需的 URL。

8. 要查看显示仓库的 yum 配置文件，输入 `ls /etc/yum.conf` 并按 `Enter`。读取文件的最后几行，其中告诉你可以在 yum.conf 文件中添加仓库，也可以创建包含仓库信息的、以 .repo 扩展名的文件。按 `q` 退出 less。

9. 输入 `ls /etc/yum.reposd` 并按 `Enter` 查看仓库列表。输入 `cat /etc/yum.reposd/fedora.repo` 并按 `Enter` 查看其中一个仓库配置文件。

10. 输入 `yum-config-manager` 并按 `Enter` 查看 yum 配置选项。你可以使用此命令配置 yum 选项并添加新仓库，而不是编辑配置文件。例如，要添加仓库，输入 `yum-config-manager --add-repo repositoryurl`，其中 repositoryurl 是仓库的 url。

11. 通过输入 `yum install rdesk*` 并按 `Enter` 安装 rdesktop 软件包。在提示时按 `y` 和 `Enter`。只要没有冲突，你可以使用通配符代替输入整个名称。

12. 要验证 rdesktop 软件包已安装，输入 `yum info rdesk*` 并按 `Enter`。你将看到信息列表。在以 Repo 开头的行上，你将看到软件包已安装。

13. 接下来，通过输入 `yum remove rdesktop` 并按 `Enter` 使用 remove 卸载软件包。按 `y` 和 `Enter` 确认。

14. 通过输入 `whereis rdesktop` 并按 `Enter` 验证软件包是否已卸载。你不应该看到 rdesktop；这意味着找不到该软件包。

15. 输入 `yum info rdesk` 并按 `Enter`。查看以 Repo: 开头的行。该行告诉你可以在 updates/20/x86_64 仓库中找到该软件包（如果你使用的是 Fedora 20 的 32 位版本，则“x86_64”将是“i386”）。

16. 如果计划继续下一个实验，请保持登录；否则请关闭计算机。

### 复习题

1. 哪个命令显示了计算机上安装的所有软件包？
a. rpm --list
b. rpm -q
c. rpm -qa
d. rpm -qa | all

2. 哪个命令显示所有以 y 开头的已安装软件包的名称？
a. rpm -q y*
b. rpm -qa y*
c. rpm -qp y*
d. rpm -qa | grep y

## 实验 11.4 检测和替换软件包文件

### 目标

有时文件会因为用户失误或攻击从硬盘上被删除。如果这些文件是软件包的一部分，软件包中的程序可能无法运行或运行得正确。你需要某种方法来检测文件丢失，以及一种替换它们的方法。软件包管理器可以为你这些。本实验将向你展示 Red Hat 包管理器 (RPM) 和 yum 如何执行这些功能。

### 所需材料

本实验需要以下材料：

- 一台运行 Fedora 20 Linux 的计算机
- Fedora 20 安装 DVD

预计完成时间：20 分钟

### 活动

1. 按下 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，如有必要，以 root 用户身份登录。

2. 大多数 Linux 计算机上安装了 gzip 软件包。要找到它的包名，输入 `rpm -qa | grep gzip` 并按 Enter。它可能名为 `gzip-1.6-2-fc20.x86_64` 或类似名称。

3. 使用 -i 选项获取软件包描述，输入 `rpm -qi gzip-1.6-2-fc20.x86_64`（如果你使用的是 32 位版本，则为 i386）并按 Enter。

4. 要查看哪些文件是软件包的一部分，使用 -l 选项，输入 `rpm -ql gzip-1.6-2-fc20.x86_64`（如果你使用的是 32 位版本，则为 i386）并按 Enter。

5. 要检查软件包的所有文件是否都已安装在硬盘上，使用 -V 选项，输入 `rpm -V gzip-1.6-2-fc20.x86_64`。

6. 检查是否缺少 `gzip-1.6-2-fc20.x86_64`（如果你使用的是 32 位版本，则为 i386）并按 Enter。

7. 删除一些文件，输入 `rm /usr/share/man1/gzip*`。

8. 要查看 rpm 如何处理文件，输入 `rpm -V gzip-1.6-2-fc20.x86_64`（如果你使用的是 32 位版本，则为 i386）并按 Enter。

9. 为了修复问题，你需要重新安装软件包。输入 `yum reinstall gzip`。按 `y` 和 `Enter` 确认。

10. 再次检查所有文件已安装，输入 `rpm -Va`。注意 yum 不包含像 rpm 那样的 verify 选项。

11. 检查系统中所有软件包的缺失文件。

### 复习题

1. 哪个命令显示关于 words-17 软件包的信息？
a. rpm -i words-17
b. rpm -qa words-17
c. rpm -iq words-17
d. rpm -qi words-17

2. 哪个命令显示软件包包含的文件？
a. rpm -q words-17
b. rpm -qa words-17
c. rpm -ql words-17
d. rpm -qi words-17

3. 哪个命令显示软件包的一部分但未安装在硬盘上的文件？
a. rpm -q words-17
b. rpm -ql words-17
c. rpm -V words-17
d. rpm -Z words-17

4. 哪个命令使用 yum 安装 blivet-2.3 软件包？
a. yum -i rdesk
b. yum -a blivet-2.3
c. yum install blivet*
d. yum install blivb

5. 哪个命令显示 yum 用于查找安装和更新软件包的仓库列表？
a. yum repolist
b. yum -list repos
c. yum showrepos
d. yum repos

6. 要为 yum 添加 http://repoexample/example.repo 仓库，输入 yum --config http://repoexample/example.repo。正确还是错误？

7. yum 的默认安装允许你验证软件包的安装。正确或错误？

8. 如果从 `words-2-17` 软件包中删除了文件，你可以使用 `yum reinstall words-2-17` 来解决该问题。正确或错误？

## 实验 11.5 备份到 SAMBA 共享

### 实验目标

本实验解释了如何挂载 SAMBA 共享并使用 `tar` 将文件备份到该共享中。你需要一个创建了 SAMBA（Windows SMB）共享且不需要身份验证的网络服务器。你也可以使用网络附属存储（NAS）设备并创建一个公共共享。在实验中，共享路径为 `/server1/public`，但你应该将其替换为你自己的服务器和共享名称。如果你无法创建一个不需要凭据的公共共享，则提供了一种使用凭据登录的备选方法。

### 所需材料

本实验需要以下材料：

- 一台运行 Fedora 20 Linux 的计算机
- 可以访问不需要登录凭据的 SAMBA 共享

预计完成时间：30 分钟

### 活动步骤

1. 启动 Linux 计算机。按下 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，并以 root 用户身份登录。

2. 输入 `mkdir /mnt/backup` 并按回车，创建一个用于挂载 SAMBA 共享的目录。

3. 输入 `mount -t cifs //server1/public /mnt/backup` 并按回车。如果提示输入密码，直接按回车。

> 如果你的共享需要登录凭据，请将挂载命令替换为：`mount -t cifs -o username,password //server1/public`，其中 `username` 和 `password` 是所需的凭据。

![](img/272b3b99ebe228b8c0cfa22abe675a46_133_0.png)

4. 输入 `ls /mnt/backup` 并按回车查看共享内容。

5. 要查看 `/etc/yum` 目录下所有与 yum 相关的文件，输入 `ls /etc/yum*` 并按回车。

6. 接下来，创建一个 tar 文件并将其保存到 `/mnt/backup` 目录中。输入 `tar -cvf /mnt/backup/yumback.tar /etc/yum*` 并按回车。

7. 输入 `ls -l /mnt/backup/yum*` 并按回车检查 tar 文件的大小。文件可能约为 20000 字节。

8. 现在，输入 `tar -cvf /mnt/backup/yumback.tar.gz /etc/yum*` 并按回车创建一个压缩的 tar 文件。`z` 选项允许 `tar` 通过 `gzip` 过滤文件以进行压缩。

9. 输入 `ls -l /mnt/backup/yum*` 并按回车检查压缩 tar 文件的大小。带有 `.gz` 扩展的文件约为 2000 字节，几乎缩小了十倍。实际获得的压缩率取决于你添加到 tar 文件中的文件类型。图形和其他二进制文件的压缩率通常低于文本文件。

10. 关闭计算机。

### 复习题

1. 哪个命令将位于名为 `accounting` 服务器上名为 `mydocs` 的 SAMBA 共享挂载到 `/mnt/docs` 目录？

   a. mount -t samba /mnt/docs //mydocs/accounting
   b. mount -t cifs //mydocs/accounting /mnt/docs
   c. mount -t samba //accounting/mydocs /mnt/docs

2. 哪个命令在 `/mnt/backup` 中创建 `/lib` 目录的未压缩 tar 文件？

   a. tar -xcf /mnt/backup/libback.tar /lib
   b. tar -xcf /lib /mnt/backup/libback.tar
   c. tar -cvf /mnt/backup/libback.tar /lib
   d. tar -xzf /lib /mnt/backup/libback.tar

3. tar 命令中的 `z` 选项通过 `bzip2` 过滤存档。正确或错误？

4. 写出命令，将位于 `operations` 服务器上名为 `reports` 的 SAMBA 共享挂载到 `/mnt/reports` 目录。

5. 如果使用 `tar` 命令通过 `gzip` 过滤文件，你总是获得大约 90% 的压缩率。正确或错误？

## 网络配置

## 本章包含的实验

- 实验 12.1 配置以太网接口
- 实验 12.2 创建 IP 别名
- 实验 12.3 安装并配置 NcFTPd
- 实验 12.4 在网络工具中使用高级选项

## CompTIA Linux+ 考试目标

| 目标 | 实验 |
| --- | --- |
| 109.1 | 互联网协议基础 | 12.1–12.4 |
| 109.2 | 基础网络配置 | 12.1–12.3 |
| 109.3 | 基础网络故障排除 | 12.4 |

## 实验 12.1 配置以太网接口

### 实验目标

本实验向你展示如何在不重启 Linux 的情况下更改任何接口参数。特别是，它展示了如何更改以太网 NIC 的 IP 地址、子网掩码、广播地址和 MAC 地址。你还学习了如何为访问本地网络网段的数据包设置默认路由。

### 所需材料

本实验需要以下材料：

- 一台运行 Fedora 20 Linux 的计算机
- 局域网连接

预计完成时间：15 分钟

### 背景知识

处理接口和 IP 地址时使用的主要命令是 `ifconfig`（全称为 "interface configuration"）。在本实验中，你将配置一个以太网 NIC。![](img/272b3b99ebe228b8c0cfa22abe675a46_137_0.png)

> `ifconfig` 的 Windows 版本是 `ipconfig`。这两个命令的功能相似，但 `ifconfig` 更多功能。你还将学习使用 `route` 命令设置访问本地网段外的默认网关。

### 活动步骤

1. 启动你的 Linux 计算机。按下 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，并以 root 用户身份登录。

2. 输入 `ifconfig` 显示所有接口的状态。对于 eth0，你应该看到类似类似的输出：
```
