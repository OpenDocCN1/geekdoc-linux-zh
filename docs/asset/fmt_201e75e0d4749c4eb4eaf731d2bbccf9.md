
- D. `xhost` 命令用于允许其他系统访问你的 X-server。`xhost +` 命令开启安全性但不授予任何访问。

```bash
xclock -geometry 200x200-0 &
```

- C. 编辑或编辑 `/etc/X11/X86Config` 文件并添加命令：

```bash
xclock -geometry 200x200-0 &
```

- D. 创建或编辑你家目录下的 `xintrc` 文件并添加命令：

`xclock &`

- D. `startx` 命令可以由任何用户运行，而不是 root 账户。你应该将任何自定义内容放在家目录下隐藏的 `.xintrc` 中。

### 18. 你通过 `telnet` 登录到远程系统，意在启动几个远程 X 客户端，它们会将输出发送到你的显示器 (admin1.xyz)。你可以做什么让这变得更容易？

- A. 使用 `-display admin1.xyz`。

### 16. 你如何从运行 `gdm` 显示器管理器的系统启动 KDE 会话？

- A. 重新链接 `/etc/X11/prefdm`。
- B. 点击 gdm 登录对话框上的 Options 按钮并选择 Sessions -> KDE。
- C. 正常登录并使用 `switchdesk` 更改你的默认桌面。
- C. 创建一个 DISPLAY admin1.xyz
- D. 创建一个带有以下内容的 DISPLAY 变量：

### 14. 你的系统正在使用 `xdm` 显示器管理器。你想使用 GNOME 显示器管理器 (gdm)。你可以怎么做？

- B. 运行 `Configurator`。
- A. 修改 `/etc/X11/prefdm` 配置。
- C. 修改 `/etc/X11/prefdm` 链接。
- B. 编辑 `/etc/X11/X86Config`。
- D. 执行 runlevel 5 命令。
- D. 使用 GNOME 控制面板更改显示器管理器。文件 `/etc/X11/prefdm` 是一个指向你的 X-Window 系统将使用的显示器器的链接。使用 GNOME 显示器管理器，运行命令：
- A. 更改 Linux 系统 runlevel 的简单方法是编辑 `/etc/init.ab` 文件并：

```bash
ln -fs /usr/bin/gdm /etc/X11/prefdm
```

- D. 你无法从 `gdm` 显示器管理器登录 KDE 环境。B 和 C 选项 B 的优势是你无需注销并重新登录。

### 15. 你希望在每次使用 `startx` 启动 X-Window 会话时自动启动 `xclock` 应用程序。你会如何做？

- A. 创建或编辑 `.xdefault` 文件并添加命令：`xclock &`

### 17. 你会发布什么命令来允许 IP 地址为 172.16.200.99 的系统上的 X 客户端访问你的 X-server？

- A. `xauth +172.16.200.99`
- B. `xhost -172.16.200.99`
- C. `xhost +`
- D. `xhost +172.16.200.99`
- D. `xhost` 命令用于允许其他系统访问你的 X-server。`xhost +` 命令开启安全性但不授予任何访问。

```bash
xclock -geometry 200x200-0 &
```

- C. 编辑或编辑 `/etc/X11/X86Config` 文件并添加命令：

```bash
xclock -geometry 200x200-0 &
```

- D. 创建或编辑你家目录下的 `xintrc` 文件并添加命令：

`xclock &`

- D. `startx` 命令可以由任何用户运行，而不是 root 账户。你应该将任何自定义内容放在家目录下隐藏的 `.xintrc` 中。

### 18. 你通过 `telnet` 登录到远程系统，意在启动几个远程 X 客户端，它们会将输出发送到你的显示器 (admin1.xyz)。你可以做什么让这变得更容易？

- A. 使用 `-display admin1.xyz`。

### 16. 你如何从运行 `gdm` 显示器管理器的系统启动 KDE 会话？

- A. 重新链接 `/etc/X11/prefdm`。
- B. 点击 gdm 登录对话框上的 Options 按钮并选择 Sessions -> KDE。
- C. 正常登录并使用 `switchdesk` 更改你的默认桌面。
- C. 创建一个 DISPLAY admin1.xyz
- D. 创建一个带有以下内容的 DISPLAY 变量：

### 629

### 14. 更改 Linux 系统 runlevel 的简单方法是编辑 `/etc/init.ab` 文件并：

```bash
export DISPLAY=admin.xyz
```

- D. 你无法从 `gdm` 显示器管理器登录 KDE 环境。B 和 C 选项 B 的优势是你无需注销并重新登录。

### 15. 你希望在每次使用 `startx` 启动 X-Window 会话时自动启动 `xclock` 应用程序。你会如何做？

- A. 创建或编辑 `.xdefault` 文件并添加命令：`xclock &`

### 17. 你会发布什么命令来允许 IP 地址为 172.16.200.99 的系统上的 X 客户端访问你的 X-server？

- A. `xauth +172.16.200.99`
- B. `xhost -172.16.200.99`
- C. `xhost +`
- D. `xhost +172.16.200.99`
- D. `xhost` 命令用于允许其他系统访问你的 X-server。`xhost +` 命令开启安全性但不授予任何访问。

```bash
xclock -geometry 200x200-0 &
```

- C. 编辑或编辑 `/etc/X11/X86Config` 文件并添加命令：

```bash
xclock -geometry 200x200-0 &
```

- D. 创建或编辑你家目录下的 `xintrc` 文件并添加命令：

`xclock &`

- D. `startx` 命令可以由任何用户运行，而不是 root 账户。你应该将任何自定义内容放在家目录下隐藏的 `.xintrc` 中。

### 18. 你通过 `telnet` 登录到远程系统，意在启动几个远程 X 客户端，它们会将输出发送到你的显示器 (admin1.xyz)。你可以做什么让这变得更容易？

- A. 使用 `-display admin1.xyz`。

### 16. 你如何从运行 `gdm` 显示器管理器的系统启动 KDE 会话？

- A. 重新链接 `/etc/X11/prefdm`。
- B. 点击 gdm 登录对话框上的 Options 按钮并选择 Sessions -> KDE。
- C. 正常登录并使用 `switchdesk` 更改你的默认桌面。
- C. 创建一个 DISPLAY admin1.xyz
- D. 创建一个带有以下内容的 DISPLAY 变量：

### 14. 你的系统正在使用 `xdm` 显示器管理器。你想使用 GNOME 显示器管理器 (gdm)。你可以怎么做？

- B. 运行 `Configurator`。
- A. 修改 `/etc/X11/prefdm` 配置。
- C. 修改 `/etc/X11/prefdm` 链接。
- B. 编辑 `/etc/X11/X86Config`。
- D. 执行 runlevel 5 命令。
- D. 使用 GNOME 控制面板更改显示器管理器。文件 `/etc/X11/prefdm` 是一个指向你的 X-Window 系统将使用的显示器器的链接。使用 GNOME 显示器管理器，运行命令：
- A. 更改 Linux 系统 runlevel 的简单方法是编辑 `/etc/init.ab` 文件并：

```bash
ln -fs /usr/bin/gdm /etc/X11/prefdm
```

- D. 你无法从 `gdm` 显示器管理器登录 KDE 环境。B 和 C 选项 B 的优势是你无需注销并重新登录。
