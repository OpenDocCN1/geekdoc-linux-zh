
`sudo chmod +x pia-linux-3.5.3-07926.run`

`sudo ./pia-linux-3.5.3-07926.run`

## 驱动程序

硬件和软件驱动程序对于计算机至关重要，作为操作系统与打印机或键盘等设备之间通信的桥梁。它们分为两种：用于基本功能的通用驱动和针对特定设备的驱动（后者需要手动安装）。驱动程序确保设备和软件顺畅交互，方便从网页浏览到媒体播放的各种任务。过时或错误的驱动程序会导致性能问题或系统故障。安装通常通过制造商网站进行，通过更新确保兼容性和安全性。没有驱动程序，计算机无法访问硬件，导致操作失败。签名驱动程序提供额外的安全性，以验证真实性。保持驱动程序更新对于顺畅运行至关重要，版本兼容性随 `Windows` 版本而异。设备管理器可以帮助检查驱动程序是否正常工作。

`NVIDIA` 驱动是将计算机与其 `NVIDIA` 图处理器连接的软件，对于最大化硬件性能至关重要。来自 `NVIDIA` 官方的认证驱动程序可确保系统优化，提升帧率、分辨率和 3D 图形性能，同时减少崩溃。可以从 `NVIDIA` 或 PC 制造商下载。

`AMD` 驱动程序是确保 `AMD` 硬件（如显卡）与计算机操作系统之间顺畅通信的必备软件。它们对于优化性能以及兼容游戏和应用程序至关重要。可以通过访问 `AMD` 支持部分检查最新的 `AMD` 驱动程序。更新可以通过 `AMD` 更新软件手动或自动进行，提高性能、稳定性和并修复漏洞。建议定期更新以获得最佳体验。

`Radeontop` 是一款多功能工具，旨在监控 `AMD` 显卡的 GPU 利用率，从 `R600` 系列开始。它提供了 GPU 整体活动和特定区块使用的的实时数据，有助于优化性能。你可以在多个 GPU 之间进行选择，将数据转储到文件，并调整输出频率和样式。虽然它主要支持开源驱动，但也与 `AMD Catalyst` 兼容（尽管存在局限）。它访问 `/dev/dri/cardN` 或 `/dev/mem` 路径需要 root 权限，确保了对 `OpenCL` 和 `OpenGL` 工作负载的详细见解，使其成为图形专业人士爱好者的必备工具。

打印机驱动程序是允许计算机与打印机通信的必备软件，将数字数据转换为打印机理解的格式。这包括转换页面布局、纸张类型和打印质量设置，确保你的文档打印准确。打印机驱动程序了解打印机的功能并处理技术细节，使从任何应用程序打印变得无缝。它们支持多种操作系统并提供装订和书籍制作等功能。通过 `Brother`、`Epson`、`HP` 和 `Canon` 等许多品牌的驱动程序，它们确保了兼容性并丰富了打印选项，简化了从数字到物理形式的过程。

### `NVIDIA`

访问 `NVIDIA` 官方网站 `https://www.nvidia.com/` 获取所有关于 `NVIDIA` 的信息。

通过驱动管理器进行图形化安装：

1. 打开驱动管理器 (`Driver Manager`)
2. 在 `NVIDIA Corporation` 下
3. 点击最新 `Nvidia-???`（推荐）驱动旁边的圆圈
4. 点击“应用更改” (`Apply Changes`)

在终端中通过 `APT` 安装 `NVIDIA`：

只需输入以下命令：

```bash
sudo apt update
```

```bash
sudo dpkg --add-architecture i386
```

```bash
sudo apt update
```

```bash
sudo apt install nvidia-driver-535 libvulkan1 libvulkan1:i386
```

在终端中通过 `APT` 仓库安装 `NVIDIA`：

只需输入以下命令：

```bash
sudo apt update
```

```bash
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt install nvidia-graphics-drivers-550 libvulkan1 libvulkan1:i386
```

### 在终端中通过 `NVIDIA` 开发者 `APT` 仓库安装 `NVIDIA`：

从更新软件包列表开始：

```bash
sudo apt update
```

为了兼容性添加 `i386` 架构：

```bash
sudo dpkg --add-architecture i386
```

再次更新软件包列表：

```bash
sudo apt update
```

导入 `NVIDIA GPG` 密钥以确保仓库的真实性：

```bash
curl -fSSL https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/3bf863cc.pub | sudo gpg --dearmor | sudo tee /usr/share/keyrings/nvidia-drivers.gpg > /dev/null 2>&1
```

将 `NVIDIA` 仓库添加到您的系统：

```bash
echo 'deb [signed-by=/usr/share/keyrings/nvidia-drivers.gpg] https://developer.download-nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/ /' | sudo tee /etc/apt/sources.list.d/nvidia-drivers.list
```

再次更新您的软件包列表：

```bash
sudo apt update
```

要查找可用的 `NVIDIA` 驱动包，可以使用以下命令搜索：

```bash
apt-cache search nvidia-driver
```

导航到源列表目录：

```bash
cd /etc/apt/sources.list.d
```

列出目录内容以确认 `NVIDIA` 列表是否存在：

```bash
dir
```

使用 `nano` 打开 `nvidia-drivers.list` 文件以验证其内容：

```bash
sudo nano nvidia-drivers.list
```

确保它包含正确的仓库行：

```bash
deb [signed-by=/usr/share/keyrings/nvidia-drivers.gpg] https://developer.download-n-nvidia.com/compute/cuda/repos/debian12/x86_64/ /
```

按下 `CTRL + X` 退出 `nano`。

最后，安装带有 `Vulkan` 支持的 `NVIDIA` 驱动：

```bash
sudo apt update
```

```bash
sudo apt install nvidia-driver libvulkan1 libvulkan1:i386
```

通过遵循这些指令，你将成功地向系统添加 `NVIDIA` 仓库并在系统上安装 `NVIDIA` 驱动和 `Vulkan` 库，确保与各种应用程序和游戏具有最佳性能和兼容性。

### `AMD`

访问 `AMD` 官方网站 `https://www.amd.com/en.html` 获取所有关于 `AMD` 的信息。

最新的稳定开源 `AMD` 驱动已作为标准包含在 `Linux Mint 21.3` 中。

在终端中通过 `APT` 仓库安装 `AMD`：

只需输入以下命令：

```bash
sudo apt update
sudo add-apt-repository ppa:oibaf/graphics-drivers
sudo apt update
sudo apt upgrade
```

通过 GUI 中的 `.deb` 安装 `AMD Radeon` 软件：

1. 访问 `AMD Linux` 驱动支持页面：`https://www.amd.com/en/support/linux-drivers`。
2. 选择“`Ubuntu x86 64-Bit`”。
3. 找到最新的 `Ubuntu 22.04 HWE` 部分并点击“`下载 (DOWNLOAD)`”。
4. 进入您的 `~/Downloads` 文件夹。
5. 双击下载的文件 `amdgpu-install_6.0.60002-1_all.deb`。
6. 在打开的窗口中点击“`安装 (Install)`”继续安装。

### `Radeontop`

访问 `Radeontop` 官方网站 `https://github.com/clbr/radeontop` 获取所有关于 `Radeontop` 的信息。

通过软件管理器进行 `DEB/FLATPAK` 包安装：

1. 打开软件管理器并搜索 `Radeontop`。
2. 点击 `Radeontop`，点击源选择框。
3. 选择系统包 (`System Package`) 或 `Flatpak` 并点击安装 (`Install`)。

在终端中通过 `APT` 安装 `Radeontop`：

只需输入以下命令：

```bash
sudo apt update
```

```bash
sudo apt install radeontop
```
