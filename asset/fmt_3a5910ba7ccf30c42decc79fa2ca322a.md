
## 让你的 LINUX 运行起来：核心技巧与技术

### 3. 配置 `.Xclients` 文件

首先检查是否存在 `.Xclients` 文件：

```
$ ls .Xclients<Enter>
```

如果不存在 `.Xclients` 文件，请复制系统的全局 Xclients 文件。在 RedHat Linux 7 和 Caldera eDesktop 2.4 上，该文件位于 `/etc/X11/xinit/Xclients`：

```
$ cp /etc/X11/xinit/Xclients ./.Xclients<Enter>
```

用你喜好的文本编辑器打开 `.Xclients` 文件。例如，使用 `Emacs` 打开该文件，可以使用以下命令：

```
$ emacs .Xclients<Enter>
```

通常情况下，你的窗口管理器或桌面环境是在 `.Xclients` 文件内部启动的。寻找你的窗口管理器启动的位置。这可能包括 `fwm`、`twm` 或 `gnome-session` 等命令。通常，这些命令包含在如下形式的条件块中：

```
if [ <some condition> ]; then
  <some commands>
else
  <other command>
fi
```

例如，一个典型的条件块可能是：

```
if [ -f /usr/X11R6/bin/fvwm ]; then
  exec fwm
else
exec twm
fi
```

#### 强制启动 KDE

要强制你的 `.Xclients` 文件启动 `KDE` 而不是当前列出的窗口管理器或桌面环境，你有两个选择：

1. 注释掉所有此类命令，包括与启动窗口管理器或桌面环境相关的整个条件块或多个块。这些块应该从 `if` 语句开始到结束语句结束都被注释掉。你可以通过在行首放置井号（`#`）来注释掉文件中的某行。将被注释的部分替换为命令：
   ```
   exec startkde
   ```
2. 将命令：
   ```
   exec startkde
   ```
   放在 `.Xclients` 文件中任何尝试启动另一个窗口管理器或桌面环境的代码之前。请记住，该命令之后的任何代码都不会被执行。

保存 `.Xclients` 文件并关闭文本编辑器。

你可以通过作为 `root` 用户编辑全局 `.Xclients` 文件（通常为 `/etc/X11/init/.Xclients`）来更改所有用户的默认桌面管理器。

### 提示 6.1.3：在 RedHat Linux 中将默认桌面更改为 KDE

正如提示 6.1.2 “将 KDE 设为默认桌面环境”中所讨论的，你需要编辑 `.Xclients` 文件来让 `KDE` 成为你的默认桌面。默认的 RedHat `.Xclients` 文件可以轻松地选择 `KDE` 作为你的默认桌面：

使用以下命令将工作目录更改到主目录，并检查你的主目录中是否已存在 `.Xclients` 文件：

```
$ cd<ENTER>
$ ls .Xclients<ENTER>
```

如果不存在 `.Xclients` 文件，请复制系统的全局 Xclients 文件：

```
$ cp /etc/X11/xinit/xclients ./.Xclients<ENTER>
```

用你喜好的文本编辑器打开 `.Xclients` 文件。例如，使用 `Emacs` 打开该文件，可以使用以下命令：

```
$ emacs .Xclients<ENTER>
```

找到以 `PREFERRED=` 开头的行。这一行大约位于文件的第五行。

编辑该行使其内容为：

```
PREFERRED=startkde
```

保存 `.Xclients` 文件并关闭文本编辑器。

你可以通过作为 `root` 用户编辑全局 `.Xclients`（通常为 `/etc/X11/xinit/Xclients`）来更改所有用户的默认桌面管理器。

### 提示 6.1.4：启动 KDE

`KDE` 包含一个启动脚本 `startkde`，用于启动 `KDE` 桌面环境。`startkde` 命令通常位于 `/usr/bin/startkde`。

要启动 `KDE`，你需要确保 `X Windows` 已经启动，然后让 `KDE` 作为窗口管理器和桌面环境运行。通常，你的窗口管理器是从全局 `.xinitrc` 文件或你的本地 `.xinitrc` 文件启动的。在某些 Linux 版本中，`.xinitrc` 文件会作为其最后项操作启动全局的 `.Xclients` 文件或本地的 `.Xclients` 文件（如果存在的话）。

通常情况下，你希望在这些文件的最后一步启动窗口管理器或桌面环境。例如，你可以在主目录中创建自己的 `.xinitrc` 文件。在 `.xinitrc` 文件中，文件的最后一个命令应该是：

```
exec startkde
```

命令中的 `exec` 部分会导致当前脚本停止并开始 `startkde`。通过这种方式，你的脚本中 `exec` 命令之后的任何命令都不会运行。这对于 `KDE` 或任何窗口管理器正确启动至关重要。

如果你想使用 `.Xclients` 文件将启动 `X` 应用程序（`.xinitrc`）与启动窗口管理器（在 `.Xclients` 中）分开，请在 `.xinitrc` 文件结尾加上：

```
exec .Xclients
```

然后在 `.Xclients` 文件结尾加上：

```
exec startkde
```

`.xinitrc` 和 `.Xclients` 文件都应该在你的主目录中。

### 提示 6.1.5：配置 xdm 以启动 KDE

`xdm` 程序用于在 `X` 环境下为 Linux 提供图形登录。当你运行级别 5 而不是级别 3 的 Linux 时，`xdm` 将启动时启动并允许你从图形窗口登录。

当你启动 `X Windows` 时，`.xinitrc` 和 `.Xclients` 文件用于确定启动哪个窗口管理器或桌面管理器以及启动哪些应用程序。使用 `xdm` 时，通过 `Xsession` 脚本确定 `X Windows` 的初始启动。全局文件存储在 `/etc/X11/Xsession` 或 `/etc/X11/xdm/Xsession`，取决于你的 Linux 版本。你的个人脚本将是 `.xsession`。

全局脚本首先尝试执行 `Xsession`。如果不存在，它会尝试执行 `Xclients`，最后，如果该脚本不存在，则在用户登录时执行全局 `Xclients` 脚本。因此，你可以按照在提示 6.1.2 “制作你的默认环境”中讨论的那样，配置 `xdm` 以启动 `KDE`，以便对你的 `.Xclients` 文件进行必要的更改。

你可以通过在 Linux 控制台输入以下命令来测试 `xdm` 配置是否生效：

```
$ xdm<Enter>
```

当显示登录界面时，登录后 `KDE` 应该就会启动。如果你想让 `xdm` 在启动时运行，你需要将默认运行级别从 3 改为 5：

用你喜好的文本编辑器打开 `.xinitrc`。例如，使用 `Emacs` 打开该文件，可以使用以下命令：

```
$ emacs .xinitrc<ENTER>
```

找到以下行：

```
id:3:initdefault:
```

将该行改为：

```
id:5:initdefault:
```

保存文件并关闭文本编辑器。`xdm` 现在会在系统启动时运行。

### 提示 6.1.6：从 xdm 切换到 kdm

`KDE` 提供了一个替代 `xdm` 的图形登录管理器，称为 `kdm`。如果你使用 `KDE` 作为桌面环境，使用 `kdm` 而不是 `xdm` 有几个优势：

- `kdm` 可以通过控制中心进行配置。
- `kdm` 与 `KDE` 紧密集成。

如果你已经按照提示 6.1.5 “配置启动 KDE”让 `xdm` 正常工作，则可以通过以下步骤切换到 `kdm`：

用你喜好的文本编辑器打开 `/etc/initab`。例如，使用 `Emacs` 编辑该文件，可以使用以下命令：

```
$ emacs /etc/initab<ENTER>
```

找到以下行：

```
respawn:/usr/X11/xdm -nodaemon
```

将该行替换为：

```
respawn:/opt/kde/bin/kdm -nodaemon
```

对于 RedHat Linux 7，该行应该是：

```
respawn:/usr/bin/kdm -nodaemon
```
