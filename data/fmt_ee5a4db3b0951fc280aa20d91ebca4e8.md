
```
erik@NOT-A-DELL~$ sudo -
last login: root@NOT-A-DELL at 23:50:16 on Sat 5 23:50:30
root@NOT-A-DELL# dnf install nmap -y
Last metadata date: 0:00:32 ago on Sat 5 23:50:32.
Dependencies resolved:
**********************************
Package                Architecture      Version                Size
**********************************
Installing:             x86_64              2.70-6.el8           ol8_appstream         5.8 M
umata                  noarch               0.34-10.el8          ol8_bases_latest      1.7 M
libnports              x86_64              35.0-1.el8          ol8_bases_latest      335 K
db3                   x86_64              35.0-1.el8          ol8_bases_latest      323 K
nmap                   x86_64              16.1-5.el8          ol8_bases_latest      249 K
ciutils               x86_64              2.70-6.el8           ol8_appstream         237 K
openssl-libs          x86_64              3.7-1.el8           ol8_bases_latest      54 K
rdma-core             x86_64              35.0-1.el8          ol8_bases_latest      59 K
**********************************
Transaction Summary
```

![](img/110fa0d6324f0893fff03cee6394144d_39_0.png)

你可以从 WSL 访问你的 Windows 磁盘。它们将以 `/mnt/DRIVE` 的形式呈现，其中 c: 盘是 `/mnt/c`。Windows 系统也可以访问 `\\OracleLinux_0_5` 路径下的 Linux 目录：

![](img/110fa0d6324f0893fff03cee6394144d_40_0.png)

## 注意事项

请注意，在编辑文件时要务必小心。Windows 和 Linux 的文本格式不同，如果你不小心，很容易损坏文件。建议使用 Windows 存储和访问 Windows 文件，并在 WSL 镜像上编辑和存储 Linux 文件。

将 Oracle 8.5 作为 Windows 子系统运行对于系统管理员和开发人员来说是一个很棒工具。它与 Windows 的集成使其安装既快捷方便，同时可以在你的个人系统中透明地访问 Linux 系统。

## 为 IT 的未来做准备——这不仅仅是一块树莓派

首先，让我们谈谈在高级 RISC 机器（通常称为 Arm CPU）上的 Oracle Linux。这种新架构相比 Intel 等使用的旧版 `x86_64` 架构具有许多优势

AMD 的使用。这包括更低的功耗；更低的延迟，带来了更好的性能；以及简化的架构，实现了更高密度的系统。在 Arm 系统上利用 Oracle Linux 对于像 Oracle 和微软这样的云端规模运营商，以及正寻求减少计算算力和冷却需求的较小规模组织来说，这都是一个热门选择。

在所有 Linux 系统上使用简单的企业级操作系统有许多优势，例如在所有服务器上使用相同的工具，并可以为您的服务器获得相同的商业支持。在您的服务器库存中，Arm 的用例也很有趣。从整体而言，Arm 处理器由于其具有更高的潜在核心密度和更低的功耗，提供了更低的成本。在企业领域，Ampere 占据主导地位，并在单个机架单元（RU）空间内在单个芯片上提供高达 128 个核心的 Arm 处理器。

性能也毫不逊色，每个系统在两个 RU 的空间内即可支持高达 128 个核心，每个核心的 CPU 频率高达 3.0 GHz。I/O 性能同样强大，拥有 128 条高速 PCIe Gen4 通道和 8*7 ECC 保护的 DDR4 3200 内存。配合 64 GB 的内联内存模块（DIMMs），在小型外形规格下就拥有 4 TB 的内存！这些企业级系统具备了 Oracle Linux 的所有动力、安全性和可靠性。

Arm 不仅用于数据中心；当您需要小型系统时（例如 DNS 服务器或远程访问设备），有著名的树莓派（Raspberry Pi），它由于其小巧的尺寸非常适合隐藏在布线间内作为备份 DNS 服务器，或放置在 Oracle Exadata 机箱内部实现远程访问。你可以将树莓派作为监控系统或 DMZ 中的 Web 服务器。

无论你运行在何种 Arm 平台上（Ampere 或树莓派），当运行 Oracle Linux 时，你也可以获得带有增强功能的 UEK（无人升级内核），其中包含 Ansible 等工具。Oracle Linux 以一个支持的价格包含了所有主要技术，而且你始终可以选择免费使用它；你可以免费打补丁。在 Arm 方面，该平台也不受限制。你可以使用如 MySQL 8.0 等商业软件，还有大量的开源软件。

强大的不仅仅是树莓派的案例。当你接触较大的基于 Arm 的服务时，你将获得大量的边缘计算用例。边缘计算需要应用程序将数据从云端带到需要低延迟访问的地方。通过 MySQL 8.0 的复制功能，你可以轻松地将数据从云端复制到边缘，保持性能的同时，利用 Ampere 等公司制造的 Arm 系统的高核心数和低功耗需求（Ampere 提供了一个 80 核心且功耗仅为 210w 的 CPU）。高核心数结合 Docker 和 Kata 等容器技术实现了分布式微服务架构，通过集中维护的应用程序在利用云端自动化的同时，仍然提供传统本地解决方案的性能。这就是 IT 的未来。

## 准备工作

在开始之前，你需要一个带有 Micro SD 卡槽的树莓派。你还需要一张可以用于安装操作系统的 Micro SD 卡。如果你使用的是树莓派计算模块（compute module）或企业级 Arm（如 Ampere 系统），请跳到第 2 章并使用 PXE 启动系统。

## 如何操作...

话虽如此，让我们在树莓派上安装 Oracle Linux。虽然我一直在 Arm 上使用 Oracle Linux 并通过这种硬核的方式进行安装，但现在有更简单的方法来安装它。Oracle 为树莓派提供了免费的镜像，其中已经安装了操作系统。

让我们采取以下步骤：

- 1. 在以下链接下载 Oracle 镜像：`https://www.oracle.com/linux/downloads/linux-arm-downloads.html`。
- 2. 接下来，你需要将镜像写入 SD 卡。在 Windows 系统上，最简单的方法是使用 `balenaEtcher`，它是一个免费工具，可以轻松地将镜像写入 SD 卡和 USB 驱动器。你可以从 `https://www.balena.io/etcher` 下载它。

### 注意

虽然示例使用了 `balenaEtcher`，但还有许多其他方法可以将文件写入闪存盘，例如 Raspberry Pi Imager，或者直接在 Linux 中使用 `dd` 命令将文件写入闪存。

- 3. 运行 `Etcher`（确保右键点击它并以管理员身份运行），选择镜像文件作为源，选择 SD 卡作为目标。

![](img/110fa0d6324f0893fff03cee6394144d_43_0.png)

`Etcher` 可以自动处理压缩文件，因此在一分钟或两分钟后，你就应该拥有一个安装好镜像的 SD 卡了。

- 4. 接下来，将卡插入你的树莓派并启动。正常的 GRUB 加载程序将启动，你应该会看到登录提示符。

Oracle Linux Server 8 (5.15.0-3.60.5.1.e18uk.aarch64)

System setup

图 1.14 - 启动树莓派

是的，这很简单！

- 5. 一旦启动，以 root 身份登录，密码为 `oracle`。系统将要求你更改密码。
