
不会对您的物理机器或已驻留在机器上的操作系统进行任何更改，因为 Kali Linux 将直接从 USB 驱动器运行。您只需拔掉 USB 驱动器，即可轻松启动到机器上的常规操作系统，无需任何额外努力。

## 便携性

您可以随身携带 Kali Linux，因为它可以一直存放在您口袋里的 USB 驱动器中。您所要做的就是将其插入可用的系统，然后即可启动 Kali Linux。

## 可定制性

我们已经讨论过，Kali Linux 是开源的，其所有代码库都公开在 GitHub 上。因此，您可以使用 Kali Linux 代码库中可用的脚本来构建自定义的 Kali Linux 安装镜像，并将其加载到 USB 驱动器上。

## 持久性

您可以定制 Kali Linux USB 驱动器以使其具有持久性。这将允许其在 USB 上存储数据，并在多次重启后保留这些数据。

为了做到这一点，我们首先需要创建一个可启动的 USB 驱动器，该驱动器已由 Kali Linux 的 ISO 镜像设置完成。

## 创建 Kali Linux USB 驱动器的要求

-   一份经过验证的 Kali Linux ISO 副本，以适应您打算运行或安装它的系统。
-   如果您使用的是 Windows，则需要 Win32 Disk Imager 软件来创建 Kali Linux USB 驱动器。在 Linux 或 OS X 上，您可以使用终端中预装的 `dd` 命令来创建可启动的 USB 驱动器。
-   容量为 4GB 或更大的 USB 驱动器。如果您的系统支持 SD 卡插槽，您也可以使用类似的流程使用 SD 卡。

现在让我们了解创建 Kali Linux Live USB 驱动器的过程。此过程将根据您正在使用的系统（即 Windows、Linux 或 MacOS）而有所不同。

## 在 Windows 上创建可启动的 Kali USB 驱动器

1.  将 USB 插入机器上的 USB 插槽，并记下分配给它的驱动器号。启动您之前下载的 Win32 Disk Imager 应用程序。
2.  选择用于 Kali Linux 安装的 ISO 文件，并确保已选择正确的 USB 驱动器进行写入。点击 **Write**（写入）。
3.  USB 驱动器写入完成后，您可以弹出驱动器，并将其用作可启动的 USB 驱动器来启动 Kali Linux Live 或在机器上安装 Kali Linux。

## 在 Linux 操作系统上创建可启动的 Kali Linux USB 驱动器

在 Linux 操作系统中，创建可启动的 USB 驱动器非常简单。一旦下载并验证了 Kali Linux ISO 文件，您就可以在终端使用 `dd` 命令将文件写入 USB 驱动器。运行 `dd` 命令需要 root 或 sudo 权限。

> **警告：** 如果您不确定如何使用 `dd` 命令，最终可能会将 Kali Linux 镜像写入您未打算写入的磁盘驱动器。因此，在使用 `dd` 命令时保持高度警惕极其重要。

您需要知道用于将 Kali Linux 镜像写入 USB 驱动器的设备路径。在未插入 USB 驱动器的情况下，在终端窗口的命令提示符中执行以下命令。

```
sudo fdisk -l
```

您将获得一个输出，显示系统中挂载的所有设备，分区将显示为：

`/dev/sda1`

`/dev/sda2`

现在，插入 USB 驱动器并再次运行相同命令 `sudo fdisk -l`。这次您会看到额外的设备，即您的 USB 驱动器。它会显示为类似 `/dev/sdb` 的内容，旁边显示 USB 驱动器的大小。

继续小心使用以下命令在 USB 驱动器上写入镜像。示例假设您的 Kali Linux ISO 文件名为 “kali-linux-2019.1-amd64.iso”，并且位于当前工作目录中。块大小参数 `bs` 可以增加，但理想值为 `bs=512k`。

```
dd if=kali-linux-2019.1-amd64.iso of=/dev/sdb bs=512k
```

向 USB 驱动器写入过程需要几分钟，完成写入所需时间略多于 10 分钟并不异常。

`dd` 命令在进程完成之前不会显示任何输出。如果您的 USB 驱动器有 LED，您会看到它闪烁，这是磁盘写入正在进行中的指示。一旦 `dd` 命令完成，输出将如下所示。

```
5823+1 records in
5823+1 records out
3053371392 bytes (3.1 GB) copied, 746.211 s, 4.1 MB/s
```

这就结束了。现在您可以使用 USB 驱动器启动 Kali Linux Live 或在机器上开始安装 Kali Linux。

## 在 MAC OS X 操作系统上创建可启动的 Kali Linux USB 驱动器

Apple OS X 是基于 Unix 的操作系统，因此在 OS X 上创建 Kali Linux 可启动 USB 驱动器与在 Linux 上创建类似。在下载并验证您的 Kali Linux ISO 副本后，您可以直接使用 `dd` 命令将 ISO 写入 USB 驱动器。

**警告：** 如果您不确定如何使用 `dd` 命令，最终可能会将 Kali Linux 镜像写入您未打算写入的磁盘驱动器。因此，在使用 `dd` 命令时保持高度警惕极其重要。

您可以使用以下步骤将 ISO 写入 USB 驱动器。

1.  在未将 USB 驱动器插入 MAC 台式机或笔记本电脑的情况下，在终端窗口的命令提示符中输入以下命令：
    ```
    diskutil list
    ```
2.  将显示一个设备路径列表，显示系统中挂载的所有磁盘，以及分区数据：
    ```
    /dev/disk1
    /dev/disk2
    ```
3.  现在，插入 USB 并再次运行 `diskutil list` 命令。您会看到列表现在也显示了您的 USB 驱动器。它将是不在第一次显示中出现的那个。假设它是：
    ```
    /dev/disk6
    ```
4.  使用以下命令卸载 USB 驱动器（假设 USB 为 `/dev/disk6`）：
    ```
    diskutil unmount /dev/disk6
    ```
5.  继续使用以下命令小心地将 Kali Linux ISO 写入您的 USB 驱动器。假设当前工作目录与保存 ISO 文件的目录相同。块大小参数 `bs` 可以增加，但理想值为 `bs=1m`：
    ```
    sudo dd if=kali-linux-2017.1-amd64.iso of=/dev/disk6 bs=1m
    ```
6.  向 USB 驱动器写入过程需要几分钟，完成写入所需时间略多于 10 分钟并不异常。
7.  `dd` 命令在进程完成之前不会显示任何输出。如果您的 USB 驱动器有 LED，您会看到它闪烁，这是磁盘写入正在进行中的指示。一旦 `dd` 命令完成，输出将如下所示：
    ```
    5823+1 records in
    5823+1 records out
    3053371392 bytes transferred in 2151.132182 secs (1419425 bytes/sec)
    ```

这就结束了。现在您可以使用 USB 驱动器启动 Kali Linux Live 或在机器上开始安装 Kali Linux。要在 OS X 机器上从期望的驱动器启动，请在计算机启动后立即按下 “Option”（选项）按钮，并选择您希望使用的驱动器。

## 在硬盘驱动器上安装 Kali Linux 的过程

在本节中，我们将学习如何在系统的硬盘上物理安装 Kali Linux。这将使其能够直接从硬盘驱动器运行，而不是如我们在上一节中讨论的那样从 USB 驱动器运行。

### 安装要求

Kali Linux 的安装过程相当简单易懂。首先，我们需要一台具有兼容 Kali Linux 安装的硬件的机器。Kali Linux 支持 32 位、64 位和 ARM (armhf 和 armel) 架构。

我们已经完成了创建 Kali Linux ISO 可启动 USB 介质的过程。如果您有 DVD 驱动器，您也可以将 ISO 镜像写入 DVD 以在机器上安装 Kali Linux。

在机器上安装 Kali Linux 的最低硬件要求如下：

-   安装文件所需的最小可用磁盘空间为 20 GB。
-   最小 RAM 容量为 1GB。虽然建议 2GB 或更多以获得更好的性能。
-   DVD 驱动器或 USB 启动支持，以协助 Kali Linux 安装。

### 安装准备

您可以通过准备以下检查表来为安装做准备。

1.  根据系统架构下载 Kali Linux ISO。
2.  使用上一章中提到的工具将 Kali Linux ISO 写入 DVD 或 USB 驱动器。
3.  确保您的计算机已设置为允许从 USB 驱动器启动。

### Kali Linux 安装过程

1.  要开始安装 Kali Linux，请使用您创建的安装介质（即 DVD 或 USB 驱动器）启动。您将看到 Kali Linux 启动屏幕。您可以选择图形模式或文本模式安装。理想情况下，继续图形安装。

