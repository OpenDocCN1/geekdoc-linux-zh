
id 行指示默认运行级别。`l5` 行负责启动所有 `/etc/rc.d/rc5.d` 脚本。我们稍后再回到这一点。`pr` 行用于电源故障后恢复供电的情况，所以我们其实不需要关心它。所有那些 `mingetty` 行代表按下 `Ctrl+Alt+F#` 时出现的虚拟控制台，因此我们也不关注它们。

最后，那个 `x` 行正是我们要找的。不要认为 `x` 本身有什么含义。请记住，在 OpenLinux 中，这一行被标记为 `gu`。第一个字段只是发行版为这条规则起的名字。我们通常要找的是某种能启动显示管理器（`xdm`、`gdm`、`kdm`）的条目。这个版本的 Red Hat 使用 `/etc/X11/prefdm`。我们稍后就会研究 `prefdm`，但现在请留意：这条规则在我们进入运行级别 5 时触发，并且如果 `prefdm` 退出，`init` 会重新启动它（这就是 `respawn` 的含义）。`-nodaemon` 参数表示 `prefdm` 不应将自己放到后台运行。由 `init` 运行的程序就应该这样工作，因为 `init` 会负责让它们转入后台运行。

有时候，仅靠名字里找 `dm` 并不那么容易。OpenLinux 运行一个名为 `rc.gui` 的脚本，该脚本随后运行 `kdm`。不过，我们感兴趣的那一行通常靠近文件底部，一旦你知道要找什么，应该还是相当明显的。

你可能会发现 `inittab` 中似乎没有任何东西能启动显示管理器。在这种情况下，你应该查看 `rc` 脚本。`rc` 脚本通常存放在 `/etc/rc.d/rc#.d` 或 `/etc/rc#.d` 中，其中 `#` 是运行级别。以 Debian 为例，你会找到一个名为 `xdm` 的 `rc` 脚本，它就是用来启动显示管理器的脚本。快速查看这个脚本，我们会看到这样一行：

```
DAEMON=/usr/bin/X11/xdm
```

这就是 Debian 将启动的显示管理器。

### 显示管理器

`init` 将运行级别设为 5 的最终目标是启动一个显示管理器。无论是直接启动（例如调用 `xdm`），还是通过脚本（如 `rc.gui`）启动，最终都应该启动一个显示管理器。

在前面的例子中，我们看到 Red Hat 使用 `prefdm`。在 Red Hat 的旧版本中，`prefdm` 是指向所需显示管理器的符号链接。在新版本中，它是一个脚本（类似于 OpenLinux 的 `rc.gui`）。

常见的显示管理器有三种。

#### XDM

`xdm` 是最古老的显示管理器。大多数发行版将 `xdm` 的配置文件存放在 `/etc/X11/xdm` 中。如果出于某种原因配置文件不在这里，请尝试以下命令：

```
locate xdm-config
```

作为探索者，我们的下一个站点是 `xdm-config`（如果我们已确定该系统使用 `xdm`）。这个文件中有大量有趣的信息，但以下是最重要的部分：

```
DisplayManager.errorLogFile:    /var/log/xdm-error.log

DisplayManager._0.setup:         /etc/X11/xdm/Xsetup_0

DisplayManager*session:          /etc/X11/xdm/Xsession
```

第一行 `errorLogFile` 决定 `xdm` 将错误消息输出到哪里。这在尝试排查 `xdm` 问题时非常重要。大多数发行版似乎都统一使用 `/var/log/xdm-error.log`。

第二行 `_0.setup` 决定 `xdm` 在显示登录提示符之前会运行哪个脚本。该脚本通常用于提供美观的背景，或许还有一个控制台窗口。`_0` 表示此配置项用于主显示器。在多显示器机器上，你可能还会看到 `_1.setup` 行，但这种情况非常少见。除非你在调试 `xdm` 本身的问题，否则不太可能需要研究这个脚本。

第三行 `session` 可能是最重要的。这是用户登录后运行的脚本。这也是不同发行版开始出现最大差异的地方。我们将在后面的内容中更详细地研究 `Xsession`。

#### KDM

`kdm` 是 KDE 显示管理器，其配置与 `xdm` 几乎相同。实际上，`kdm` 直接基于 `xdm` 的源代码。`kdm` 提供了一些不错的功能，例如用户头像（显示系统上可用的用户 ID）、多语言支持以及更具可配置性的外观。所有这些高级配置都由控制中心管理。该对话框名称为“登录管理器”（Login Manager），但其具体位置似乎随着 KDE 的每次小更新而变化。通常可以在“应用程序”（Applications）、“系统”（System）或仅“系统”（System）下找到。

由于 `kdm` 使用 `xdm` 的配置文件，因此用户登录时它也会调用 `/etc/X11/xdm/Xsession`。

#### GDM

`gdm` 是 GNOME 显示管理器，是 `xdm` 的完全重写，尽管它通常实现相同的功能（以及 `kdm` 新增的功能）。

主要的 `gdm` 配置文件是 `/etc/X11/gdm/gdm.conf`。这个位置相当标准，但如果你在这里找不到 `gdm.conf`，可以尝试：

```shell
$ locate gdm.conf
```

`gdm` 的配置实际上有点复杂，但 `gdm.conf` 中的以下几行应该能为你理解启动顺序指明正确方向：

```text
LogDir=/var/gdm

DisplayInitDir=/etc/X11/gdm/Init

PreSessionScriptDir=/etc/X11/gdm/PreSession

SessionDir=/etc/X11/gdm/Sessions/

PostSessionScriptDir=/etc/X11/gdm/PostSession/
```
