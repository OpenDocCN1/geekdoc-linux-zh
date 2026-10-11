
```bash
cd ~/arm-stuff/images
git clone git://github.com/raspberrypi/firmware.git rpi-firmware
cp -rf rpi-firmware/boot/* boot/
rm -rf rpi-firmware

cp ~/arm-stuff/kernel/tools/mkimage/kernel.img kgdboc=ttyAMA,115200 console=ttyAMA0,115200 console=tty1
echo "dwc_otg.enable=0 console=ttyAMA0,115200 ... root=/dev/mmblk0p2 roottype=ext4 rootwait" > boot/cmdline.txt
```

```bash
umount $root
umount $boot
kpartx -dv $loopdevice
losetup -d $loopdevice
```

我们使用 `dd` 工具将此文件镜像到你的 SD 卡中。在我们的示例中，假设存储设备位于 `/dev/sdb`。根据需要更改此项。

```bash
dd if=kali-pi.img of=/dev/sdb bs=1M
```

一旦 `dd` 操作完成，卸载并弹出 SD 卡，然后启动你的 Pi 进入 Kali Linux。

# KALI LINUX

官方 Linux 文档

此 PDF 在 docs.kali.org 上自动生成 - 2013年8月19日

# 自定义 Chromebook 镜像

本文档描述了我们创建**自定义 Kali Linux Samsung Chromebook 镜像**的方法，目标群体是开发者。如果你想安装预制的 Kali 镜像，请查看我们的[在 Samsung Chromebook 上安装 Kali](Install Kali on Samsung 文章。

在本指南中，我们创建了一个包含两个启动分区的镜像——其中一个硬编码从 SD 卡启动，另一个硬编码从 USB 启动。根据你的存储介质，按照指南最后阶段的说明，在镜像到 USB 后标记相关的启动分区。

## 01. 创建 Kali rootfs

按照我们 Kali 文档中的描述构建 Kali rootfs，使用 `armhf` 架构。在此过程结束时，你应该在 `~/arm-stuff/rootfs/kali-armhf` 中拥有一个填充了内容的 rootfs。

## 02. 创建镜像文件

接下来，我们创建物理镜像文件，它将包含我们的 Chromebook rootfs 和启动镜像。

```bash
apt-get install kpartx xz-utils gdisk uboot-mkimage vboot-utils
cd ~
mkdir -p arm-stuff
cd arm-stuff/
mkdir -p images
cd images
dd if=/dev/zero of=kali-custom-chrome.img bs=1MB count=7000
```

## 03. 分区并挂载镜像文件

```bash
parted kali-custom-chrome.img --script -- mlabel msdos
parted kali-custom-chrome.img --script -- mkpart primary fat32 0 64
parted kali-custom-chrome.img --script -- mkpart primary ext4 64 -1
gdisk kali-custom-chrome.img --script -- gpt
```

```bash
loopdevice=`losetup -f --show kali-custom-chrome.img`
device=`kpartx -va $loopdevice | sed -E 's/.*(loop[0-9]).*/\1/g' | head -1`
device="/dev/mapper/${device}"
boot1=${device}p1
boot2=${device}p2
root=${device}p3
```

```bash
mkfs.ext4 $root
mkdir -p root
mount $root
```

## 04. 复制并修改 Kali rootfs

使用 `rsync` 将之前引导的 Kali rootfs 复制到挂载的镜像中。

```bash
cd ~/arm-stuff/images/
rsync -HPavz ~/arm-stuff/rootfs/kali-armhf/ root
echo nameserver 8.8.8.8 > root/etc/resolv.conf
```

```bash
mkdir -p root/etc/X11/
cat << EOF > /root/etc/X11/xorg.conf/50-touchpad.conf
Section "InputClass"
Identifier "touchpad"
MatchIsSynaptics
Option "TapButton1" "1"
Option "TapButton2" "3"
Option "TapButton3" "2"
Option "FingerLow" "15"
Option "FingerHigh" "20"
Option "FingerPress" "256"
End
EOF
```

## 05. 编译 Samsung 内核和模块

如果你没有使用 ARM 硬件作为开发环境，你需要设置一个 ARM 环境来构建 ARM 内核和模块。完成后，请按照以下指令操作。

获取 Chromium 内核并将将其放入我们的开发树中：

```bash
cd ~/arm-stuff
mkdir -p kernel
cd kernel
git clone http://git.chromium.org/chromiumos/third_party/kernel.git -b chromeos-3.4 chromeos
cd chromeos
```

# KALI LINUX

官方 Linux 文档

此 PDF 在 docs.kali.org 上自动生成 - 2013年8月19日

```bash
cat << EOF > kernel.its
/dt-v1;
description = "Chrome OS kernel image with one or more blobs";
#address-cells = 0;
images {
  kernel@1 {
    description = "kernel";
    data = "/incbin(arch/arm/boot/zimage)";
    type = "kernel_noload";
    arch = "arm";
    os = "linux";
    compression = "none";
    entry = 0;
  };
  fdt@1 {
    description = "exynos5250-snow.dtb";
    data = "/incbin(arch/arm/boot/exynos5250-snow.dtb)";
    type = "flat_dt";
    arch = "arm"
    compression = "none";
    hash@1 {
      algo = "sha1";
    }
  }
};
configurations {
  default = "conf@1";
  conf@1 {
    kernel = "kernel@1";
    fdt = "fdt@1";
  }
};
EOF
```

# KALI LINUX

官方 Linux 文档

此 PDF 在 docs.kali.org 上自动生成 - 2013年8月19日

在我们的案例中，为内核应用无线注入补丁。

```bash
mkdir -p ../patches
wget http://patches.airrack-ng.org/mac80211.compat08082009.wl_frag+ack_v1.patch -O ../patches/mac80211.patch
wget http://patches.airrack-ng.org/channel-negative-one.patch -O ../patches/negative.patch
```

等待，OCR逻辑有些混乱：

配置，然后如下所示交叉编译 Chromium 内核。
