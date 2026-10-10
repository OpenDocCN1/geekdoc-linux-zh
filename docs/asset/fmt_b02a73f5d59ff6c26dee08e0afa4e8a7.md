
# 第 16 章

## 设置 XFree86 的工具（第 306 页）

- `SuperProbe` 命令可以告诉你你的显卡。
- `Xconfiguration` 是简单的 Red Hat 配置程序。
- 需要更精确的控制（以及更多问题），使用 `xf86config` 程序。
- 如果你必须手动编辑文件，请阅读 `/usr/lib/X11/doc/Devices` 和 `/usr/lib/X11/doc/Monitors` 中的文档。

如果你真的必须手动生成配置文件，请查看互联网上以下网址的文档：

`http://www.xfree86.org/3.1.2/VideoModes.html`
`http://www.ccil.org/-esr/faqs/video-modes.html`
`http://tsikora.tiac.net/video-modes.html`

* 在创建好配置后，你可以使用 `xvidtune` 对其进行调整。

## X Window 系统如何启动（第 309 页）

X Window 系统在启动时会执行以下步骤：

1. 运行 `startx` 命令。
2. 执行脚本 `$HOME/.xserverrc`。如果文件不存在，则使用 `/usr/X11R6/lib/X11/xserverrc`。
3. 客户端启动并执行 `$HOME/.xinitrc`，如果不存在，则执行 `/usr/X11R6/lib/X11/xinit/xinitrc`。
4. 该脚本通常查找 `$HOME/.clients`，如果可用则运行。

5. 脚本运行初始化程序，如下：

| 程序 | 用户文件 | 系统文件 |
| :--- | :--- | :--- |
| `xrdb` | `.Resources` | `/usr/X11R6/lib/X11/xinit/.Resources` 1 |
| `xmodmap` | `.Xmodmap` | `/usr/X11R6/lib/X11/xinit/.Xmodmap` 2 |

1. 首先加载系统资源，然后合并用户资源。
2. 你的键盘修改映射将覆盖系统映射。
6. 运行窗口管理器。

## 窗口管理器（第 311 页）

Linux 自带了以下窗口管理器：

| 名称 | 描述 |
| :--- | :--- |
| `fwm2-95` | Free 窗口管理器版本 2 |
| `fwm` | Free 窗口管理器 |
| `twm` | Trivial 窗口管理器 |
| `olwm`, `olvm` | Open Look 窗口管理器及其虚拟版本 |

## 映射映射（第 313 页）

要交换 Ctrl 和 Caps Lock 键，请将以下行放入 `$HOME/.Xmodmap` 文件中：

348

发现中心

```
remove Lock = Caps_Lock

remove Control = Control_L

keysym Control_L = Caps_Lock

keysym Caps_Lock = Control_L

add Lock = Caps_Lock

add Control = Control_L
```

## 将你的窗口管理器更改为 fwm2（第 314 页）

在默认的 `$HOME/.Xclients` 文件中注释掉以下行：

```bash
#if [ ! -z($type -path fwm95-2) ]; then
# env > /tmp/rootzenenv.0
# exec fwmM4 fwm95-2 -f "RCFILE"-debug -display :0 \
# $HOME/.FWM95-errors 2>&1
#fi
```

## 将你的窗口管理器为 olwm 或 olvm（第 315 页）

要使用 `olwm`，你需要将以下行放在 `.Xclients` 文件的开头：

```bash
#!/bin/bash
PATH=/usr/openwin/bin:$PATH
olvm
```

## 配置 fwm95-2（第 315 页）

从 `/etc/X11/TheNextLevel` 拷贝配置文件并对其进行编辑。你可能只需要 `.fwm92rc.defines` 即可。

# 第 17 章

## 调试源代码（第 320 页）

要调试源代码，请按照以下步骤操作：

1. 使用 `rpm` 命令安装源代码，如下：

```bash
[root@pc root]# cd /mnt/cdrom/SRPMS
[root@pc root]# rpm -i <package-file>
```

2. 使用以下命令解压源代码：

```bash
[root@pc SRPMS]# cd /usr/redhat/SPECS
[root@pc SPECS]# rpm -bp <spec-file>
```

3. 通过以下命令生成程序：

```bash
[root@pc SRPMS5]# cd /usr/src/redhat/SPECS
[root@pc SPECS]# rpm -bc <spec-file>
```
