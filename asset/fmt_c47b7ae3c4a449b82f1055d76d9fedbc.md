
- IRQ, DMA, I/O 地址
- 槽位类型、速度和时钟芯片
- 型号、RAM 类型和芯片组
- 型号、RAM 大容量和芯片组

28. 哪个 `SuperProbe` 选项将显示可检测的视频适配器硬件列表？

- a. 无；它将探测任何连接到系统的显卡
- b. `-1`
- c. `-info`
- d. `-help`

29. `GNOME` 桌面环境使用哪个窗口管理器？

- a. `K Window Manager`
- b. `Starfish Window Manager`
- c. `Sawfish Window Manager`
- d. `Swordfish Window Manager`

30. 哪个命令可以让你配置电脑使用的鼠标？

- a. `mouseadmin`
- b. `mouseconfig`
- c. `mouseconfigurator`
- d. `configmouse`

31. 下列哪个命令可以配置视频适配器卡和显示器信息？

- a. `vidconfig`
- b. `vidconfigurator`
- c. `Xconfigurator`
- d. `SuperProbe`

# 动手项目

这些项目应该按照给出的顺序完成。所有动手项目总共需要三个小时来完成。本实验的要求包括：

- 一台按照“动手项目 7-2”安装了 `Red Hat 7.2` 的计算机。

## 项目 10-1

在这个动手项目中，你将从运行级别（`runlevel`） 3 启动和停止 `X Windows` 以及 `GNOME` 桌面环境。

1. 开启电脑。当完全启动后，使用用户名 `root` 和密码 `secret` 登录 `gdm`。
2. 当 `GNOME` 桌面加载后，按下 `Ctrl-Alt-Bkspce` 组合键。发生了什么？为什么？
3. 通过按下 `Ctrl-Alt-F2` 切换到命令行终端 (`tty2`)，并使用用户名 `root` 和密码 `secret` 登录终端。
4. 在命令提示符处，输入 `runlevel` 并按 `Enter`。显示了什么？为什么？
5. 在命令提示符处，输入 `init 3` 并按 `Enter`。
6. 当到达运行级别 3 时，使用用户 `root` 和密码 `secret` 登录。
7. 输入 `startx` 并按 `Enter` 加载 `GNOME` 桌面。
8. 当 `GNOME` 桌面加载后，按下 `Ctrl-Alt-Bkspce` 组合键。发生了什么？为什么？
9. 输入 `exit` 并按 `Enter` 退出你的 shell（壳）。

## 项目 10-2

在这个动手项目中，你将从运行级别 3 启动和停止 `X Windows` 以及各种窗口管理器和桌面环境。

1. 通过按下 `Ctrl-Alt-F2` 切换到命令行终端 (`tty2`)，并使用用户名 `root` 和密码 `secret` 登录终端。
2. 在命令提示符处，输入 `runlevel` 并按 `Enter`。如果你不在运行级别 3，在命令提示符处输入 `init 3` 并按 `Enter`。当到达运行级别 3 时，使用用户 `root` 和密码 `secret` 登录。
3. 输入 `startx` 并按 `Enter` 加载 `GNOME` 桌面。
4. 当 `GNOME` 桌面加载后，使用鼠标导航到 工具栏 $\rightarrow$ `GNOME` 按钮（最左侧按钮） $\rightarrow$ 程序 $\rightarrow$ 系统 $\rightarrow$ 桌面切换工具。
5. 使用鼠标选择 `KDE` 并点击 `OK` 按钮。
6. 按下 `Ctrl-Alt-Bkspce` 组合键返回你的 shell。

# 第 10 章 X 窗口系统

7. 在命令提示符处，输入 `cat .Xclients-default` 并按 `Enter`。显示了什么？
8. 在命令提示符处，输入 `startx` 并按 `Enter`。加载了哪一个？为什么？
9. 当 `KDE` 桌面加载时，使用鼠标导航到 工具栏 $\rightarrow$ `K` 按钮（最左侧按钮） $\rightarrow$ 系统 $\rightarrow$ 桌面切换工具。
10. 使用鼠标选择 `FVWM` 并点击 `OK`。
11. 按 `Ctrl-Alt-Bkspce` 组合键返回你的 shell。
12. 在命令提示符处，输入 `cat .Xclients-default` 并按 `Enter`。显示了什么？
13. 在命令提示符处，输入 `startx` 并按 `Enter`。加载了哪个窗口管理器？为什么？
14. 使用鼠标左键点击桌面背景并选择 `Exit Fwm → Yes, Really Quit`（真的退出吗）。
15. 在命令提示符处，输入 `vi .Xclients-default` 并按 `Enter`。修改读取如下的行：

```
exec /usr/X1R6/bin/fwwm2
```

改为：

```
exec /usr/bin/enlightenment
```

完成后，保存更改并退出 `vi` 编辑器。
16. 在命令提示符处，输入 `startx` 并按 `Enter`。加载了哪个窗口管理器？为什么？
17. 在按住 `Ctrl` 键的同时，使用鼠标左键点击桌面背景并选择 `Log Out → Yes, Log Out`（注注销）。
18. 在命令提示符处，输入 `vi .Xclients-default` 并按 `Enter`。修改读取如下的行：

```
exec /usr/bin/enlightenment
```

改为：

```
exec /usr/bin/wmaker
```

完成后，保存更改并退出 `vi` 编辑器。
19. 在命令提示符处，输入 `startx` 并按 `Enter`。加载了哪个窗口管理器？为什么？
20. 使用鼠标右键点击桌面背景并选择 `Exit → Exit`（退出），然后在提示出现时点击 `Exit`。

# 动手项目

21. 在命令提示符处，输入 `vi .Xclients-default` 并按 `Enter`。修改读取如下的行：

```
exec /usr/bin/wmaker
```

改为：

```
exec /usr/bin/dwm
```

完成后，保存更改并退出 `vi` 编辑器。
22. 在命令提示符处，输入 `startx` 并按 `Enter`。加载了哪个窗口管理器？为什么？
23. 使用鼠标右键点击桌面背景并选择 `Exit`。
24. 在命令提示符处，输入 `rm .Xclients-default` 并按 `Enter`。删除了哪些文件？
25. 在命令提示符处，输入 `startx` 并按 `Enter`。加载了哪个？为什么？
26. 按 `Ctrl-Alt-Bkspce` 组合键返回你的 shell。
27. 在命令提示符处，输入 `init 5` 返回运行级别 5。显示了什么？

## 项目 10-3

在这个项目中，你将配置 `GDM`。

1. 通过 `Ctrl-Alt-F7` 切换到图形界面，使用用户名 `root` 和密码 `secret` 登录 `GNOME` 桌面。
2. 使用鼠标导航到 工具栏（最左侧按钮） $\rightarrow$ 程序 $\rightarrow$ 系统 $\rightarrow$ `GDM` 配置。
3. 在外观选项卡中，点击 `Logo` 旁的浏览按钮。
4. 当文件对话框显示时，选择 `/usr/share/pixmaps` 中的 `apple-png`。
5. 点击 登录 选项卡，勾选允许用户运行。
6. 点击 界面 选项卡，勾选显示图像。
7. 点击默认图像旁的浏览按钮。
8. 当文件对话框显示时，选择 `apple-png` 并点击 `OK`。
9. 点击背景选项卡，选择颜色。
10. 观察 `gdm`。背景是什么颜色的？登录框旁边有 logo 吗？系统上的每个有效用户都有 logo 吗？
11. 使用鼠标点击系统菜单。菜单中有指向 `GDM` 配置工具的链接吗？
12. 双击代表 `root` 用户的苹果图标。输入密码 `secret` 并按 `Enter` 登录系统。
13. 按 `Ctrl-Alt-Bkspce` 组合键返回 `gdm` 屏幕。

# 项目 1-4

在这个动手项目中，你将记录系统中的视频硬件信息。

1. 通过按下 `Ctrl-Alt-F2` 切换到命令行终端 (`tty2`)，并使用用户名 `root` 和密码 `secret` 登录终端。
2. 在命令提示符处，输入 `SuperProbe` 并按 `Enter`。根据显示的关于视频适配器的信息填充以下表格：

| 型号 |
| 芯片组（可能与型号相同） |
| RAM 容量 |
| RAMDAC（可选） |
| 时钟芯片（可选） |

3. 使用你的电脑手册补充上一步表格中缺失的视频适配器卡信息。
4. 使用你的电脑手册或显示器背后的信息填充以下表格：

| 显示器型号 |
| 垂直同步频率范围 |
| 水平同步频率范围 |
| 支持的最大分辨率 |

## 动手项目

## 487

5. 使用你的电脑手册或观察电脑后部，确定你拥有的鼠标设备类型：

| 型号 | 端口 (PS/2, COM1, 等) |
| :--- | --- |
