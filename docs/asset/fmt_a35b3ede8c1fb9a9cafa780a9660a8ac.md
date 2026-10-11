
## 8.73. MarkupSafe-2.1.5

MarkupSafe 是一个实现 XML/HTML/XHTML Markup 安全字符串的 Python 模块。

预计编译时间：小于 0.1 SBU

所需的磁盘空间：508 KB

### 8.73.1. 安装 MarkupSafe

使用以下命令编译 MarkupSafe：

```
pip3 wheel -w w dist --no-cache-dir --no-build-isolation --no-deps $PWD
```

此软件包不带测试套件。

安装软件包：

```
pip3 install --no-index --no-user --find-links dist markups
```

### 8.73.2. MarkupSafe 的内容

安装目录：`/usr/lib/python3.12/site-packages/MarkupSafe-2.1.5.dist-info`

## 8.74. Jinja2-3.1.3

Jinja2 是一个实现简单 pythonic 模板语言的 Python 模块。

近似编译时间：少于 0.1 SBU

所需磁盘空间：3.2 MB

### 8.74.1. 安装 Jinja2

构建包：

```
pip3 wheel -w dist --no-cache-dir --no-build-isolation --no-deps $PWD
```

安装包：

```
pip3 install --no-index --no-user --find-links dist Jinja2
```

### 8.74.2. Jinja2 内容

安装目录：`/usr/lib/python3.12/site-packages/Jinja2-3.1.3.dist-info`

## 8.75. 来自 Systemd-255 的 Udev

Udev 包包含了用于动态创建设备节点的程序。

近似编译时间：0.2 SBU

所需磁盘空间：144 MB

### 8.75.1. 安装 Udev

Udev 是 `systemd-255` 包的一部分。使用 `systemd-255.tar.xz` 作为源 tar 包。

从默认的 udev 规则中移除两个未使用的组 `render` 和 `sgx`：

```
sed -i -e 's/GROUP="render"/GROUP="video"/'
-e 's/GROUP="sgx"//' rules/50-udev-default.rules
```

移除一个需要完整 Systemd 安装的 udev 规则：

```
sed '/systemd-sysctl1/s///' rules/99-systemd.rules
```

为独立安装调整调整到网络配置文件的硬编码路径：

```
sed '//NETWORK_DIRS/s/systemd/udev/\1' -i src/basic/path-lookup.h
```

为编译准备准备 Udev：

```bash
mkdir -p build
cd build

meson setup \
  --prefix=/usr \
  --buildtype=release \
  --Dmode=release \
  --Ddev-kvm-mode=0660 \
  -Dlink-udev-shared=false \
  -Dlogind=false \
  -Dvconsole=false
```

`meson` 选项的含义：

- `--buildtype=release`

此开关覆盖了默认的编译类型 ("debug")，它会产生未优化的二进制文件。

- `--Dmode=release`

禁用上游认为实验性的某些功能。

- `--Ddev-kvm-mode=0660`

默认的 udev 规则允许所有用户访问 `/dev/kvm`。编辑者认为这是危险的。此选项覆盖了该设置。

- `--Dlink-udev-shared=false`

此选项防止 udev 链接到内部 systemd 共享库 `libsystemd-shared`。该库设计供许多 Systemd 组件共享，对于独立安装来说太冗余了。

- `--Dlogind=false -Dvconsole=false`

这些选项防止生成属于我们不会安装的其他 Systemd 组件的多个 udev 规则文件。

Linux From Scratch - 版本 12.1

获取内置辅助工具列表并将其保存到环境变量中（导出并不是绝对必要的，但它使得作为普通用户或使用包管理器时更加简单）：

```bash
export udev_helpers=$(grep "name" :" "/src/udev/meson.build | \
  awk 'print $3' | tr -d '"' | grep -v 'udevadm')
```

仅构建 udev 需要的组件：

```bash
ninja udevadm system-hwdb \
  $(grep -n -Eo '(src/lib)?udev.rules.d/[^/]*[\\]]*') \
  $(realpath libudev.so --relative-to .) \
  $udev_helpers
```

安装包：

```
install -vm75 -d /usr/lib,/etc/udev/[udev,hwdb.d,network
install -vm75 -d /usr/lib,/share/pkgconfig \
install -vm75 udevadm /usr/bin/
install -vm75 system-hwdb /usr/bin/udev-hwdb \
install -xvrn ./bin/udev /sbin/udev \
install -cp -av libudev.so /usr/lib/
install -vm664 /src/udev/libudev.h /usr/include/
- -vm664 /src/libudev.* /usr/lib/pkgconfig \
install -vm664 /src/udev/*.conf /usr/share/pkgconfig/
install -vm664 udev.conf /etc/udev/
install -vm664 rules.d/*../rules.d/ /usr/lib/udev/rules.d/
install -vm664 $(find . -name "power-switch*") /usr/lib/udev/rules.d/
install -vm664 hwdb.d/*../hwdb.d/ /usr/lib/udev/hwdb/
install -vm755 $udev_helpers /usr/lib
install -vm664 ../network/99-default.link /network
```

在 LFS 环境中安装一些自定义规则和文件：

```bash
tar -xf /systemd-man-pages.tar.xz \
  --no-owner --strip-components=1 \
  -C /usr/share/man --wildcards '*udev*' '*systemd.link.5
```

安装 man 页：

```bash
tar -xf /systemd-man-pages.tar.xz
make -f udev-2018/Makefile install
```

```bash
sed 's/systemd/udev/network|' /usr/share/man/man5/systemd.link.5 \
  /usr/share/man/man5/udev.link.5
```

```bash
sed 's/systemd/(udev\)/ /usr/share/man/man8/systemd-hwdb.8 \
  /usr/share/man/man8/udev-hwdb.8
```

```bash
sed 's/.lib|udev/udev|' /usr/share/man/man8/systemd-udev.service \
  /usr/share/man/man8/udev.8
```

```bash
rm /usr/share/man/man*
```

最后，取消 `udev_helpers`：

```bash
unset udev_helpers
```

### 8.75.2. 配置 Udev

关于硬件的信息维护在 `/etc/udev/hwdb.d` 和 `/usr/lib/hwdb.d` 目录中。Udev 需要将这些信息编译成二进制数据库 `/etc/udev/hwdb.bin`。创建数据库：

```bash
udev-hwdb update
```

此命令在硬件信息更新时需要运行。

### 8.75.3. Udev 内容

- 安装的程序：`udevadm`（`udevadm` 的软链接）， `udev-hwdb`

- 安装的库：`libudev.so`
