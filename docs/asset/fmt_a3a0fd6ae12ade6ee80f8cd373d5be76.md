
```
remove snd-atixp /usr/sbin/asisctl store >/dev/null 2>&1 \
  | : -sbin/modprobe -r --remove snd-atixp

alias usb-controller ehci-hnd

alias usb-controller1 ohci-hnd

alias ieel3194-controller ohci3194
```

配置可能会变得复杂，因为你通常会在安装或删除操作中使用使用了另一个 `modprobe` 操作来实际安装或删除模块。如果你有嵌套的 `modprobe` 操作，即在第一个安装或删除操作内部调用的第二个 `modprobe` 操作，就会出现这种情况。上一个示例中的 `install snd-atixp` 和 `remove snd-atixp` 条目就是如此。问题在于，第二个 `modprobe` 操作也会读取 `modprobe.conf` 文件并重新执行 `install` 和 `restore` 命令。这可以通过 `--ignore-install` 选项来解决，它可以忽略第二次的 `install` 和 `remove` 操作。

**提示** 在某些情况下，Kmod 可能无法以你想要的方式检测设备，从而无法加载你需要的内核模块。在这种情况下，需要向 GRUB 启动加载器指定内核参数以加载正确的模块。

## 从供应商处安装新模块

通常，你可能会发现你的硬件设备不支持当前的 Linux 模块。在这种情况下，你可能需要从硬件供应商或开源开发小组下载驱动，创建你自己的驱动并为你的内核安装。

### 驱动包

驱动程序可能是 RPM 格式或压缩包。安装驱动程序的过程取决于供应商如何支持该驱动。这里列出了不同类型的包：

- `RPM` 包：某些网站将提供已经封装成 RPM 文件的驱动程序，以便直接在 Fedora 上安装。在这里，你只需要运行 `system-config-packages` 或 `rpm3` 来安装该模块。
- 在存档中编译的驱动：某些会提供已经为 Fedora 编译好的驱动，但封装在压缩包中。在这种情况下，简单的 `install` 操作会将支持的模块放在 `modules` 目录中并供内核使用。
- 源代码：其他一些仅提供源代码，编译时，它将检测你的系统配置并据此编译模块。
- 带有源码的脚本：某些会提供自定义脚本，这些脚本可能会提示你回答关于系统的基本问题，然后编译并安装模块。

对于以压缩包 `tar.gz` 或 `tar.bz2` 形式提供的驱动程序，`compile` 和 `install` 操作通常会运行一个由 `make` 命令操作的 Makefile 脚本。简单的 `install` 通常只需要在驱动程序的软件目录中运行以下命令：

```
make install
```

对于提供源代码的网站，你可能需要像处理任何软件一样同时执行 `configure` 和 `compile` 操作。

```
./configure

make

make install
```

对于没有 `install` 选项的包，无论是已编译的还是源码，你必须手动将模块移动到内核目录 `/lib/modules/version/`，并使用 `depmod` 来加载它。

如果某个网站给了你一个自定义脚本，你只需要运行该脚本即可。例如，许多主板上的 Marvel 千兆以太网接口使用 `sk98linux.o` 模块中的 SysConnect Linux 驱动。标准的内核配置将生成并安装此模块。但如果你使用的是较新的主板，可能需要下载并安装最新的 Linux 驱动程序。SysConnect 提供了一个名为 `install.sh` 的脚本，它可以引导你配置、编译并安装模块。

```
./install.sh
```

### 内核头文件：`/lib/modules/version/build`

如果你需要编译模块，请使用 `/lib/modules/version/build` 下的内核源码。要编译，请确保 `/usr/src/linux` 是一个符号链接。

```bash
ln -s /usr/src/kernel-2.6.11-42-fc14 /usr/src/linux
```

## 第六部分：系统管理

现在切换到内核目录。对于 RPM 源包，该目录位于 `/usr/src/redhat/BUILD/kernel-version/linux-version`，其中 `version` 是内核版本。然后使用 `make` 命令并配合 `xconfig` 或 `menuconfig` 参数来显示内核配置菜单，通过以下命令调用它们。`make xconfig` 会启动一个 X Window 系统界面，需要在你桌面的终端窗口中运行。

```bash
make xconfig
```

使用如第 35 章描述的菜单，选择你需要的模块。确保每个模块都被标记为模块。在 `xconfig` 中点击 `Module` 复选框，或在 `menuconfig` 中输入 `m`。内核配置完成后，选择并退出配置菜单。然后，你使用以下命令编译模块并创建模块二进制文件：

```bash
make modules
```

这将模块置于内核源码模块目录。你可以将所需的模块拷贝到内核模块目录 `/lib/modules/version/kernel`，其中 `version` 是你的 Linux 内核版本号。简单的方法是使用以下命令重新安装所有模块。这会将所有编译后的模块复制到 `/lib/modules/version/kernel` 目录：

```bash
make modules_install
```
