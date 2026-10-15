
| | `.s files` | `.h files` | `.c files` | TOTAL |
| --- | --- | --- | --- |
| `/drivers` | 310439 | 190738 | 846219 | 1075122 |
| `/arch` | 306894 | 645444 | 119799 | 518083 |
| `/src` | 20590 | 85916 | 106506 |
| `/fs` | 159607 | 56653 | 57653 |
| `/include` | 218 | 38808 | 484642 | 523642 |
| `/kernel` | 2773 | 140979 | 143752 |
| `/ms` | 256 | 6289 | 6545 |
| `/crypto` | 4721 | 4171 | 45892 |
| `/init` | 817 | 3166 | 3983 |
| `/scripts` | 3156 | 35473 | 38629 |
| `/blocks` | 167 | 1460 | 1627 |
| `/tools` | 1566 | 1372 | 2938 |
| `/Documentation` | 770 | 9158 | 9928 |
| `/virt` | 1524 | 4103 | 4627 |
| `/init` | 78 | 2994 | 3072 |
| `/firmware` | 2425 | 268 | 2693 |
| `/sound` | 150 | 1032 | 1182 |

这里大部分行都是驱动程序或不同类型的文件。与其它操作系统比较时，应该注意 X-window 源码没有包含在内。在这里，我们包含了所有架构。

以下是最近内核版本变化的行数：

## 内核版本 TOTAL L19B2

```
2.6.18 7022962
2.6.19 7308043
2.6.20 7400843
2.6.21 752299
2.6.22 774767
2.6.23 781716
2.6.24 806258
2.6.25 839505
2.6.26 863998
2.6.27 890698
2.6.28 912960
2.6.29 958126
2.6.30 1041963
2.6.31 1075122
```

### 5.2 内核浏览器

这里大部分行都是驱动程序或不同类型的文件。与其它操作系统比较时，应该注意 X-window 源码没有包含在内。在这里，我们包含了所有架构。

### 5.3 内核配置文件

这里大部分行都是驱动程序或不同类型的文件。与其它操作系统比较时，应该注意 X-window 源码没有包含在内。在这里，我们包含了所有架构。

## 5.4 编译你自己的内核

为了实验，你可能想尝试自己的，特别是如果你需要从 `http://www.kernel.org` 编译并安装一个原生内核。为了做到这一点，你需要：

- 内核源码（例如 `linux-2.6.31.tar.bz`）

- 配置文件（例如 `config-2.6.31.x86_64`）

第一个可以从 `http://www.kernel.com/cdp` 获取，第二个可以从此处获取：

包含在你源码中的以下脚本（`KERNEL.sh`）将处理解包、编译和安装的所有步骤。为此你只需要

```
$ KERNEL.sh 2.6.31.linux.tar.bz2 config-2.6.31.x86_64
```

如果内核已经解包并配置好，进入内核源码目录并不带参数运行将负责编译和安装。

## 5.5 initrd 和 initramfs

## 5.6 实验

# 第 5 章 内核编译与编译

## 5.4. 运行你自己的内核

```bash
echo "building: linux KERNEL kernel from FILE
   using: CONFIGFILE as the configuration file"
set -x
# 解压内核，假设为 bz2 格式
tar jf $KERNEL
# 拷贝配置文件
$CONFIGFILE $KERNEL
# 进入主源码目录
cd $KERNEL
set +x
```

```bash
}
function makeinitrd_REHDAY() {
# 构建 initrd 镜像
if [ "$KERNEL" -ge 2 ]; then kernel masked up
  if [ "$KERNEL_RAID4/5/.config" = "*" ]; then
    if [ "$BOOT-without-driver /sbin/initrd" = "*" ]; then
      rm -f $BOOT-initrd.img $KERNEL
      makeinitrd -v --without-driver $BOOT-initrd.img $KERNEL
    fi
  fi
fi
cp /boot/grub
cp $boot/grub.cfg /boot/grub/grub.bak
grub2 --update-default
}
```

```bash
# 确定我们哪个发行版
function get_SYSTEM() {
  if [ "$SYSTEM" = "*" ]; then
    if [ -f /etc/debian_version ]; then SYSTEM="DEBIAN"
      return
    fi
    if [ -f /etc/ubuntu_version ]; then SYSTEM="UBUNTU"
      return
    fi
    if [ -f /etc/centos-release ]; then SYSTEM="CENTOS"
      return
    fi
    if [ -f /etc/redhat-release ]; then SYSTEM="REDHAT"
      return
    fi
    if [ -f /etc/lsb-release ]; then SYSTEM="LINUX"
      return
    fi
    if [ -f /etc/arch-release ]; then SYSTEM="ARCH"
      return
    fi
    SYSTEM="UNKNOWN"
  fi
}
```

```bash
# 查询内核版本
function get_KERNEL_VERSION() {
  if [ -f /proc/kernel/version ]; then
    eval code="$(cat /proc/kernel/version)" # Makefile
    dfi
  fi
  # 是否有本地版本提示？
  if [ -f /local-version-tip ]; then
    KERNEL_PATCHLEVEL_EXTRAVERSION="$(cat /local-version-tip)_SUBLEVEL_EXTRAVERSION"
  fi
}
```

```bash
function makeinitrd() {
  make initrd
  if [ -f $BOOT/initrd.img ]; then
    update-initramfs -u -k $KERNEL
  else
    update-initramfs -c -k $KERNEL
  fi
}
```

```bash
# 确定 vmlin, System.map, image 配置文件的放置位置
function get_BOOT() {
  if [ "$BOOT" = "*" ]; then
    BOOT="/boot"
  fi
  if [ "$ARCH" = "i386" ]; then
    BOOT="$BOOT/32"
  elif [ "$ARCH" = "x86_64" ]; then
    BOOT="$BOOT/64"
  fi
}
```

```bash
function make_GRUB() {
  make_grub
}
```

```bash
# 并行处理，为多个 CPU 编译
function get_MAX() {
  CPU_COUNT=$(cat /proc/cpuinfo | wc -l)
  MAKE_MAX="make -j $(($CPU_COUNT * 2))"
}
```

```bash
function make_URUB() {
  makeinitrd_URUB()
}
```

```bash
# 如果内核是可行的的，则编译 nvidia.ko
function get_VIABLE() {
  if [ "$KERNEL" = "*" ]; then
    if [ "$(which --skip-alias-nvidia)" = "*" ]; then
      dealwith_nvidia $KERNEL
    fi
  fi
}
```

```bash
function make_SURE() {
  make install
  root
}
```
