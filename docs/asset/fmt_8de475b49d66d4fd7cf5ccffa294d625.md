
以下指南将帮助你在 Trimslice 上安装 Kali Linux。

1. 你需要一张 8GB 或更大的 SD 卡或 eMMC 来安装 Kali Linux。
2. 从 https://www.offensive-security.com/kali-linux-arm-images/ 下载 Kali Linux 的 ISO。
3. 你现在可以使用 `dd` 工具将此镜像写入 SD 卡。在我们的示例中，我们将把 Kali Linux 安装在路径为 `/dev/sdb` 的 SD 卡上。你可以根据需要对其进行更改。

注意：这将擦除 SD 卡上的所有内容。选择错误的磁盘设备可能会导致设备硬盘被清空。

```
xzcat kali-$version-trimslice.img.xz | dd of=/dev/sdb bs=512k
```

此过程取决于设备速度和镜像大小，需要一些时间。

完成 Kali Linux 安装所需的时间取决于 SD 卡的速度和 Kali Linux 镜像的大小。

在 `dd` 操作完成后，在保持 SD 卡插入的情况下启动 Trimslice。你可以使用用户名 `root` 和密码 `toor` 登录 Kali 桌面。

# Trimslice Kali 开发者指南

如果你是一个喜欢冒险并喜欢软件开发，并且想要对 Trimslice 的 Kali Linux 镜像进行某些自定义，例如修改内核配置，可以 https://github.com/kalilinux/build-scripts/kali-arm 查看适用于 ARM 设备的 Kali 脚本。使用的脚本是 `trimslice.sh`

# Kali Linux – Cubieboard

Cubieboard 是一款 ARM 设备，具有以下配置：

1. 0.9GHz 双核处理器
2. 1GB 内存

可以使用外部 SD 卡为 Cubieboard 安装 Kali Linux。

## Cubieboard Kali 用户指南

以下指南将帮助你在 Cubieboard 上安装 Kali Linux。

1. 你需要一张 8GB 或更大的 SD 卡或 eMMC 来安装 Kali Linux。
2. 从 https://www.offensive-security.com/kali-linux-arm-images/ 下载 Kali Linux 的 ISO。
3. 你现在可以使用 `dd` 工具将此镜像写入 SD 卡。在我们的示例中，我们将把 Kali Linux 安装在路径为 `/dev/sdb` 的 SD 卡上。你可以根据需要对其进行更改。

注意：这将擦除 SD 卡上的所有内容。选择错误的磁盘设备可能会导致设备硬盘被清空。

```
xzcat kali-$version-cubieboard.img.xz | dd of=/dev/sdb bs=512k
```

此过程取决于设备速度和镜像大小，需要一些时间。

完成 Kali Linux 安装所需的时间取决于 SD 卡的速度和 Kali Linux 镜像的大小。

在 `dd` 操作完成后，在保持 SD 卡插入的情况下启动 Cubieboard。你可以使用用户名 `root` 和密码 `toor` 登录 Kali 桌面。

## Cubieboard Kali 开发者指南

如果你是一个喜欢冒险并喜欢软件开发，并且想要对 Cubieboard 的 Kali Linux 镜像进行某些自定义，例如修改内核配置，可以 https://github.com/kalilinux/build-scripts/kali-arm 查看适用于 ARM 设备的 Kali 脚本。使用的脚本是 `cubieboard.sh`

# Kali Linux – Riotboard

Riotboard 是一款 ARM 设备，具有以下配置：

1. 1GHz Cortex A9 处理器
2. 1GB 内存

可以使用外部 SD 卡为 Riotboard 安装 Kali Linux。

## Riotboard Kali 用户指南

以下指南将帮助你在 Riotboard 上安装 Kali Linux。

1. 你需要一张 8GB 或更大的 SD 卡或 eMMC 来安装 Kali Linux。
2. 从 https://www.offensive-security.com/kali-linux-arm-images/ 下载 Kali Linux 的 ISO。
3. 你现在可以使用 `dd` 工具将此镜像写入 SD 卡。在我们的示例中，我们将把 Kali Linux 安装在路径为 `/dev/sdb` 的 SD 卡上。你可以根据需要对其进行更改。

注意：这将擦除 SD 卡上的所有内容。选择错误的磁盘设备可能会导致设备硬盘被清空。

```
xzcat kali-$version-riot.img.xz | dd of=/dev/sdb bs=512k
```

此过程取决于设备速度和镜像大小，需要一些时间。

完成 Kali Linux 安装所需的时间取决于 SD 卡的速度和 Kali Linux 镜像的大小。

在 `dd` 操作完成后，在保持 SD 卡插入的情况下启动 Riotboard。你可以使用用户名 `root` 和密码 `toor` 登录 Kali 桌面。

## Riotboard Kali 开发者指南

如果你是一个喜欢冒险并喜欢软件开发，并且想要对 Riotboard 的 Kali Linux 镜像进行某些自定义，例如修改内核配置，可以 https://github.com/kalilinux/build-scripts/kali-arm 查看适用于 ARM 设备的 Kali 脚本。使用的脚本是 `riot.sh`

## RIOTboard 上的 Kali – 开发者指南

如果你是一个喜欢冒险并热衷于软件开发的人，并想对 RIOTboard 的 Kali Linux 镜像进行一些自定义，例如更改内核配置，你可以访问 https://gitlab.com/kalilinux/build-scripts/kali-arm 查看 ARM 设备的 Kali 脚本。使用的脚本是 `riot.sh`。

# Kali Linux – NanoPi2

NanoPi2 是一款 ARM 设备，其配置如下：

1. 1.9 GHz 四核处理器
2. 1GB 内存

NanoPi2 可以使用外部 SD 卡安装 Kali Linux。

## NanoPi2 上的 Kali – 用户指南

以下说明将帮助你如何在 NanoPi2 上安装 Kali Linux。

1. 你需要一张 8GB 或更高容量的 SD 卡或 eMMC 来安装 Kali Linux。
2. 从 https://www.offensive-security.com/kali-linux-arm-images/ 下载适用于 NanoPi2 的 Kali Linux ISO 文件。
3. 你现在可以使用 `dd` 工具将此镜像写入 SD 卡。在我们展示的示例中，我们将 Kali Linux 安装在路径为 `/dev/sdb` 的 SD 卡上。你可以根据自己的需求进行更改。

注意：这将删除 SD 卡上的所有内容。选择错误的磁盘设备也可能导致设备的硬盘被擦除。

```
xzcat kali-$version-nanopi2.img.xz | dd of=/dev/sdb bs=512k
```

此过程取决于你的设备速度和镜像大小，可能需要一段时间时间。

完成 Kali Linux 安装所需的时间取决于 SD 卡的速度和 Kali Linux 镜像的大小。

在 `dd` 操作完成后，你可以在插着 SD 卡的情况下启动 NanoPi2。你可以使用用户名 `root` 和密码 `toor` 登录 Kali 桌面。

## NanoPi2 上的 Kali – 开发者指南

如果你是一个喜欢冒险并热衷于软件开发的人，并想对 NanoPi2 的 Kali Linux 镜像进行一些自定义，例如更改内核配置，你可以访问 https://gitlab.com/kalilinux/build-scripts/kali-arm 查看 ARM 设备的 Kali 脚本。使用的脚本是 `nanopi2.sh`。

# Kali Linux – Utilit Pro

Utilit Pro 是一款 ARM 设备，其配置如下：

1. 1.2 GHz 四核 Cortex A9 处理器
2. 2GB 内存

Utilit Pro 可以使用外部 SD 卡安装 Kali Linux。

## Utilit Pro 上的 Kali – 用户指南

以下说明将帮助你如何在你的 Utilit Pro 上安装 Kali Linux。

1. 你需要一张 8GB 或更高容量的 SD 卡或 eMMC 来安装 Kali Linux。
2. 从 https://www.offensive-security.com/kali-linux-arm-images/ 下载适用于 Utilit Pro 的 Kali Linux ISO 文件。
