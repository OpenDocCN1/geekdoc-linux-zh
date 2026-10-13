
为了运行 VNC，本地或远程机器上必须运行一个 `vncserver`。在设置好配置后，运行 `vncserver` 来启动服务器。可以通过同一台计算机进行循环——只需运行 `vncviewer <hostname>:<display>` 即可弹出显示窗口。或者包含了许多选项——多到无法列出每一个。这些选项允许你在不编辑 VNC 系统文件的情况下运行 `vncserver` 或 `vncviewer`。对于 `vncserver`，你允许设置希望使用的显示名称（例如 `:1`）（只要它未被使用）、桌面顶部名称（例如 `<name>`）、深度（`-depth 16`）、几何图形（`-geometry 800x600`）。正如之前提到的，许多选项在运行时可以通过 `vncserver` 传递。命令包括更改访问端口（`-port`）、强制共享（`-alwaysshared`）、禁用共享（`-nevershared`），以及几何图形和深度设置。`vncviewer` 选项包括允许多个用户共享一个桌面（`-shared`）、使查看器变为只读（`-readonly`）、全屏模式（`-fullscreen`），以及设置深度（例如 `-depth 32`）。要获取可用选项的完整列表，请带有 `-help` 选项运行任一文件（`vncserver`、`vncviewer` 或 `Xnc`）。

# 实验习题

- 1. 编译 VNC 源文件并将这些文件安装到你的本地 `bin` 目录（即 `~/bin`）。找到你的 `perl` 命令并确保它准确地列在 `vncserver` 文件中。

- 2. 使标题仅显示为“Sair Linux/GNU”。仅允许鼠标事件传递到服务器。所有其他事件（键盘）都应显示弹出窗口。不应允许任何按事件通过。为你的 `vncserver` 弹出窗口设置默认值。

- 3. 更改 `vncserver` 的分辨率为 `800x600` 且分辨率为 16 位。将 `.Xauthority` 设置为系统默认，而不是用户的。配置 VNC 在启动时运行 GNOME 或 KDE。

- 4. 运行 `vncserver`。在本地运行 `vncviewer`，在远程运行 `vncviewer`。在 Windows 机器上启动 WinVNC 并在 Linux 机器上运行 `vncviewer`。

## 问题

- 1. 如果运行 `vncserver` 的系统突然崩溃会发生什么？

- 2. 如果运行 `vncviewer` 的系统突然崩溃会发生什么？

# 答案

- 1. `vncviewer` 将关闭，在 `vncviewer` 重新连接之前必须重启 `vncserver`。

- 2. 什么都不会发生，只有在系统恢复后，需要重新运行 `vncviewer` 来连接到 `vncserver`。

## 高级问题

- 1. 这项应用在业务中有什么意义？

- 2. 它与显示管理器（display manager）相比如何？

- 3. 这项应用对广域网（WAN）有什么意义？

通过编辑 `.bashrc` 文件，系统管理员可以定义实用的别名（`aliases`），让某些任务对用户更容易。例如，如果系统管理员希望所有用户都能在提示符处输入 `inbox` 直接进入他们的收收件箱，他应该在 `.bashrc` 的 `alias` 部分设置如下所示的别名：

```
alias inbox='vi -i'
```

设置别名是配置 Linux 易用性的重要部分。每个别名包含三个主要部分：

- `声明`。这部分告诉 `shell` 随后的信息将作为别名被执行。

- `别名名称`。执行该别名时需要输入的单词或短语。

- `命令`。调用该别名时应该执行的命令。

每个别名应具有以下形式：

```
alias alias_name='command'
```

为了设置 `rm` 命令在删除文件之前始终进行提示，可以使用以下别名：

```
alias rm='rm -i'
```

这将 `rm` 命令别命名为交互版本的 `rm`。

编辑 `.bash_profile` 文件同样重要。它负责设置用户定义的路径。如果向机器添加了软件，定义用户路径将非常有用。例如，如果系统添加了一个新程序，其可执行文件位于 `/usr/local/gn/bin`，将目录 `/usr/local/gn/bin` 添加到 `.bash_profile` 中的路径变量中将允许用户调用该可执行文件而无需指定路径。要更改路径变量，首先打开位于 `/etc/skel` 的 `.bash_profile` 文件，然后编辑路径变量将 `/usr/local/gn/bin` 添加到路径中。可以通过添加内容来实现：

```
:$usr/local/gn/bin
```

到以 `PATH=` 开头的行中。通过将目录放置在此行中并用冒号分隔，可以向路径添加额外的目录。

接下来是 `.xinitrc` 和 `.xclients`。系统管理员可以通过编辑 `.xinitrc` 和 `.xclients` 文件来设置默认窗口配置。这些文件由 `startx` 脚本读取，以设置用户偏好和资源。`.xclients` 包含了当运行 `startx` 时启动哪个窗口管理器或桌面环境的信息。`.xinitrc` 包含了关于 X Window 如何初始化的信息。

是什么让 `.xclients` 在其语境下变得有用？例如，如果用户拥有漫游配置文件（也就是说，用户可以登录网络上的任何计算机并加载所有的偏好和设置），`.xclients` 会根据定义的设置设置其偏好的环境。然而，`.xclients` 的功能不仅于此。它还为用户设置了桌面环境的层次。如果本地机器上没有首选的桌面环境，`.xclients` 将在层次中搜索下一个，直到找到为止。

以下是 `.xclients` 的示例：

```bash
# 检查用户是否有偏好的桌面环境
if [ -f /etc/config/desktop ]; then
    PREFERRED_SESSION=gnome
elif [ -f /etc/config/desktop ]; then
    PREFERRED_SESSION=kde
fi

# 默认情况下我们运行 gnome
if [ -n "$PREFERRED_SESSION" ]; then
    exec $PREFERRED_SESSION
# 如果没有安装 gnome，则尝试 kde
if [ -n "$START_SESSION" ]; then
    exec $START_SESSION
fi
```

`.xinitrc`# 尝试自己操作

此练习的第一步是设置一个别名。要做到这一点，请编辑 `.bashrc` 并设置别名以像之前一样执行 `tar -cvf`。下一个练习是将你的路径设置为特定目录。系统管理员有一个目录 `/fileserver/work`，她希望系统上的所有文件都在该目录中编译和运行。为了设置默认配置，将编辑 `.xclients` 文件，以便在没有安装其他窗口管理器时进行初始化。保持故障备设置不变。为了此标签的目的，还需要编辑 `.xinitrc`。编辑 `.xinitrc` 以便仅使用用户定义的设置，而不是全局配置。

## 问题

1. `.bashrc` 是否依赖于 `.bash_profile`，或者反之亦然？为什么？

2. `/etc/skel` 中最重要的文件是什么？也就是说，`/etc/skel` 中必须存在哪些文件，用户账户才能处于“激活”状态？

3. 配置错误的 `.xclients` 会阻止用户登录 X 吗？图形化登录又是怎样的呢？

4. 创建一个名为 `untar` 的别名来归档文件。

5. 桌面图标可以通过编辑 `/etc/skel` 目录中的信息来创建。正确或错误？

## 回答

1. `.bashrc` 依赖于 `.bash_profile`，因为 `.bash_profile` 先被读取，并且在其中定义了读取 `.bashrc` 中定义的环境。

2. `/etc/skel` 中最重要的文件是 `.bash_profile` 和 `.bashrc`。没有这些文件，用户就没有 `shell` 环境，因此账户是没用的。

3. 配置错误的 `.xclients` 可能会阻止用户登录 X，但有故障备设置可以尝试防止这种情况的发生。`.xclients` 文件对图形化登录没有影响。

4. 要创建名为 `untar` 的别名，请编辑 `.bashrc` 文件并添加条目：

```
alias untar='tar -xvf'
```

5. 通过编辑 `/etc/skel` 中桌面目录下的信息，可以创建桌面图标。

## 高级问题

1. 如果在定义的路径内创建了一个新目录，该新创建的目录在用户的路径中吗？路径会遵循符号链接吗？

2. 为了节省路径的时间和麻烦，创建一个条目将用户的路径设置为当前工作目录。

3. 效率是编程的重要部分；不必要的代码块会影响效率。浏览 `.initrc` 文件，看看可以删除哪些内容以提高效率。对 `.xclients` 也这样做。

# 实验 XXI 性能测试

## 目的
