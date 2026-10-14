

## 高级技巧

优化交换空间与索引，并精简你的内核。

前面几页的技巧能帮助你以最少的精力充分利用你的 Linux 发行版。但如果这些还不能满足你对速度的渴望，那就让我们继续学习一些高级调整技巧。不过，在应用这些技巧之前，请记住，它们不仅操作更复杂，而且如果粗心大意地应用，可能会对你的系统设置产生严重影响。

让我们从 RAM 磁盘开始。RAM 磁盘是一种基于内存的文件系统，它直接在计算机的 RAM 中创建存储区域，就像磁盘驱动器上的分区一样。这样做的主要好处是 RAM 磁盘非常快。由于重启机器时其中的数据会丢失，因此 RAM 磁盘只适用于需要重复性小数据区域进行缓存或用作临时空间的应用。

在创建 RAM 磁盘之前，请使用 free 命令检查你的发行版上未使用的 RAM 数量。然后使用 sudo mkdir /mnt/ramdisk 创建一个文件夹作为 RAM 磁盘的挂载点，并使用以下命令挂载它：

```
sudo mount -t tmpfs -o size=1024M tmpfs /mnt/ramdisk
```

这将使用专为创建 RAM 磁盘而设计的 tmpfs 文件系统创建一个 1GB 的 RAM 磁盘。

为了确保每次启动进入发行版时 RAM 磁盘都能自动挂载，你需要将其添加到 /etc/fstab 文件中。在文本编辑器中打开它，并在新的一行中输入以下内容：

```
tmpfs /mnt/ramdisk tmpfs nodev,nosuid,noexec,nodiratime,size=2048M 0 0
```

一旦你创建了 RAM 磁盘，就可以用它来存放浏览器的缓存。如果你使用 Chromium 浏览器，只需修改启动器条目，使用适当的开关（如 --disk-cache-dir="/mnt/ramdisk"）将其指向 RAM 磁盘即可。

如果你使用 Firefox，请在地址栏中输入 about:config。在列表中的某处右键单击，选择“新建”>“字符串”。当被问到首选项名称时，输入 browser.cache.disk.parent_directory，然后在其值中输入你想存储缓存的路径，例如 /mnt/ramdisk。接下来找到首选项 browser.cache.disk.enable，确保其设置为 True，否则双击它以切换该值。

## 控制交换空间使用

想知道为什么你的配备大量 RAM 的机器仍然起步缓慢？原因很可能是你的发行版仍在使用的硬盘交换空间，其读写速度比 RAM 慢。

如果你的系统有足够的内存来处理你交给它的任何任务，你应该尽量减少交换空间的使用。swappiness 参数管理内核将进程从物理内存转移到交换磁盘的能力。当进程被频繁地移出内存时，这可能会增加应用程序的响应时间。

命令 cat /proc/sys/vm/swappiness 将显示你的发行版当前设置的 swappiness 级别。Ubuntu 的默认 swappiness 值是 60。该参数将

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_127_0.png)

> 考虑使用诸如 Phoronix Test Suite 之类的基准测试工具，定期评估你的机器性能。

## 分析并优化启动过程

我们已经了解了大多数发行版自带的图形工具，这些工具有助于精简不必要的应用程序和服务。在这里，我们将研究使用 Systemd 进一步优化启动的方法。Systemd 是一个系统管理守护进程，旨在取代日益老化的 init 系统。与 init 一样，Systemd 是一个管理其他守护进程的主守护进程。

主要的桌面发行版，如 Fedora、Mageia 和 OpenSUSE 已经切换到 Systemd 守护进程，而 Debian 和 Ubuntu 等其他发行版也已宣布计划在即将发布的版本中进行切换。

在 Systemd 发行版上，你可以使用 systemd-analyze 命令测量启动时间，该命令会打印启动内核、加载服务和用户空间所花费的时间。

你可以使用 systemd-analyze blame | head 获取占用大部分启动时间的进程列表，这些进程按初始化所需时间排序。systemd-analyze plot > boot.svg 命令将在 boot.svg 图像文件中可视化整个启动过程。你可以在浏览器中查看此文件，以了解进程链的情况。

一旦你识别出有问题的服务，你可以将其屏蔽。当你对某个服务执行此操作后，它将无法通过 Systemd 启动，并且实质上变得不可见。如果你不使用 LVM、RAID 或任何加密设备，你可以屏蔽几乎所有 Fedora 存储服务，例如 sudo systemctl mask lvm2-monitor.service 和 sudo systemctl mask mdmonitor.service。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_127_1.png)

> 你也可以使用图形化的 Systemadm 工具管理 Systemd 服务。

