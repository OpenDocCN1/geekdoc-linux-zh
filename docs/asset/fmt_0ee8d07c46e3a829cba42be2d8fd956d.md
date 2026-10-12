
# n 是数值或布尔值

```bash
# n 是数值或布尔值
```

# 字符串

```bash
# 字符串
```

# 请编辑括号引号之间的内容

保持原样。

```bash
# 请编辑括号引号之间的内容
# 保持原样。
```

# 调试

```bash
# 调试
# 格式与 -D 选项相同
# (但不带 -D 前缀)
```

# 中断

```bash
# 中断
# 模拟 INT08 类型中断
# 或关闭 CPU 模拟，有效值：80[345]86
```

# 计数器

```bash
# 计数器
# 如果可能使用 Pentium 计数器
# 0 = 由 dosemu 校准，否则给定 (例如 166.66)
```

# 内存

```bash
# 内存
# 以 KB 为单位
$_pci = (off)
# 以 KB 为单位
$_xms = (1024)
# 以 KB 为单位
$_ems = (1024)
# 以 KB 为单位
$_ems_frame = (0xe000)
# 以 KB 为单位，< 640
$_dosmem = (640)
# 段值/范围列表，例如
# "0xc8000 range 0xc000,0xcffff"
```

# 安全

```bash
# 安全
# 安全性：n (普通用户), g (访客), d
# 空字符串：取决于'restricted'
# "0"：始终不安全（不推荐）
```

# 列表

```bash
# 列表
# 黑名单，如 "hacker1 newbie gateway"
```

# 配置文件

```bash
# 配置文件
# 空或 3 字符，config.sys -> config.XXX
# 空或 3 字符，autobect -> autoexec.XXX
# 空或 3 字符，system.ini -> system.XXX
```

# 阈值

```bash
# 阈值
$_hogthreshold = (1)
# 0 === 将所有 CPU 功率分配给 DOSEMU
```

# 第 30 章 • Linux 与 DOS/Windows

```bash
$ irqpassing = " "  # 传递给 DOS 的 IRQ 编号列表 (2-15)，例如 "3 8 10"
```

```bash
$ speaker = " "  # 扬声器 "native" (原生) 或 "emulated" (模拟)
```

```bash
$ term_char_set = " "  # 全局代码页和字符集选择。
# "" = 自动，否则为：ibm, latin, latini, latin2
```

```bash
$ term_color = (on)  # 支持颜色的终端
$ term_updfreq = (4)  # 刷新之间的时间（单位：20 == 1 秒）
$ esccarr = (30)  # 30 == 等于 Ctrl-^，特殊序列前缀
```

```bash
$ rawkeyboard = (0)  # 跳过普通键盘输入，可能有危险
$ layout = "auto"  # 选项之一：finish-(latin1), de-(latin1), be, it, us
# uk, dk-(latin1), keyb-no, no-latin1, dvorak, po
```

```bash
$ sg-(latin1), fr-(latin1), sf-(latin1), es-latin1
$ sw, hu-(latin2), hu-cwi, key-user
# hr-cp852, hr-latin2, hu-cwi, key-user
# 或 'auto'（尝试根据当前的 Linux 控制台设置生成标题）
```

```bash
$ keybint = (on)  # 模拟 ECI 键盘中断
```

```bash
$ X_updfreq = (5)  # 刷新之间的时间（单位：20 == 1 秒）
$ X_title = "DOS IN A BOX"  # 窗口顶部栏的标题
$ X_icon_name = "xdos"  # 最小化时的图标文本
$ X_keycode = (auto)  # 或 on -- 通过 dosemu 键盘键位表翻译键盘
# 或 off 或 auto
```

```bash
$ X_blinkrate = (8)  # 光标闪烁频率
$ X_font = ""  # 位于 /usr/X11R/lib/X11/fonts/* 的文件名（不带后缀）例如 vga
$ X_sharecolormap = (off)  # 与其他应用程序共享颜色表
$ X_fixed_aspect = (on)  # 设置固定比例以缩放图形窗口
```

```bash
$ X_aspect_43 = (on)  # 图形始终使用 4:3 的宽高比
$ X_lin_filt = (off)  # 对于 >15 bpp 插值使用线性过滤
```

# 在 Linux 中运行 DOS

```bash
$ X_bilin_filt = (off) # 对于 >15 bpp 插值使用双线性过滤
```

```bash
$ X_model3fact = (2) # 视频模式 0x13 的初始缩放因子 (320x200)
```

```bash
$ X_winsize = "" # "x,y" 初始窗口大小（默认浮点数）
```

```bash
$ X_gamma = (1.0) # 伽马校正
$ X_vgaemu_memsize = (1024) # 模拟 vga 帧缓冲区的大小（KB）
```

```bash
$ X_lfb = (on) # 在 VESA 模式下使用帧缓冲区
$ X_pm_interface = (on) # VESA 模式下使用保护模式接口
$ X_mgrab_key = "" # 激活鼠标捕获的 KeySym 名称，为空则关闭
```

```bash
$ X_vesamode = "" # xres,yres ... xres,yres 要添加的 vesamodes 列表。该列表必须包含
```

（注：由于原文文本后部分存在乱码或重复，上述翻译已根据指令对可逻辑部分进行了清理和处理）

```bash
$ esccarr = (30)  # 30 == 等于 Ctrl-^，特殊序列前缀
$ rawkeyboard = (0)  # 跳过普通键盘输入，可能有危险
$ layout = "auto"  # 选项之一：finish-(latin1), de-(latin1), be, it, us
# uk, dk-(latin1), keyb-no, no-latin1, dvorak, po
```

```bash
$ sg-(latin1), fr-(latin1), sf-(latin1), es-latin1
$ sw, hu-(latin2), hu-cwi, key-user
# hr-cp852, hr-latin2, hu-cwi, key-user
# 或 'auto'（尝试根据当前的 Linux 控制台设置生成标题）
```

```bash
$ keybint = (on)  # 模拟 ECI 键盘中断
```
