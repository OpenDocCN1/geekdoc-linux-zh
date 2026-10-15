
这些设置会影响 GNOME 桌面环境以及在其中启动的任何应用程序（如 `gnome-terminal`）。但是，默认情况下，它们不会应用于通过远程系统的 `ssh` 登录访问的账户，或在虚拟控制台（如 `tty5`）上的文本文本登录。

> 注意

您可以让您的 shell 环境使用与图形环境相同的 `LANG` 设置，即使当您通过文本虚拟控制台或 `ssh` 登录时也是。实现这一点的方法是在 `~/.bashrc` 文件中放置类似于下面的代码。此示例将文本登录使用的语言设置为与当前 GNOME 桌面环境设置的语言匹配：

```bash
i=$(grep 'LANGUAGE=' /var/lib/AccountsService/users/${USER} \
| sed 's/LANGUAGE=/')
if [ "$i" != "" ]; then
  export LANG=$i
fi
```

日语、韩语、中文以及其他非拉丁字符集的语言在文本虚拟控制台上可能无法正常显示。

可以通过在命令行中设置 `LANG` 变量来使单个命令使用另一种设置：

`[user@host]$ LANG=fr_FR.utf8 date`

`jeudi avril 25 17:55:01 CET 2019`

随后的命令将恢复到系统的默认输出语言。可以使用 `locale` 命令来确定 `LANG` 以及其他相关环境变量当前值。

### 输入法设置

Red Hat Enterprise Linux 7 或更高版本中的 GNOME 自动使用 `IBus` 输入法选择，便于快速更改键盘布局和输入。

“区域与语言”应用程序也可用于启用替代输入法。在“区域与语言”应用程序中，“输入源”（Input Source）框显示当前可用的输入法。默认情况下，英语（美国）可能是唯一可用方法。高亮英语（美国）并点击键盘图标选择当前布局。

要添加另一种输入法，点击输入源窗口左下角的 `+` 按钮。将打开“添加输入源”窗口。选择您的语言，然后选择您偏好的输入法或键盘布局。

当配置了多个输入法时，用户可以通过输入 `Super+Space` 快速切换。GNOME 顶栏还会出现一个状态指示器，它有两个功能：指示哪种输入法处于激活状态，并作为一个用于在输入法之间切换或选择复杂输入法高级功能的菜单。

某些方法标记有齿轮图标，表示这些方法具有高级配置选项和功能。例如，日语（假名字符）输入法允许您在拉丁字母中预编辑文本，并使用方向键和向上键选择正确的字符。

美国英语使用者也可能发现这有用。例如，英语（美国）键盘布局是英语（国际 AltGr 键），它将 PC 104/105 键键盘上的 AltGr（或右 Alt）视为“次级位移”修饰键和用于输入额外字符的死键激活键。还有 Dvor 等其他替代布局可用。

> 注意

如果知道 Unicode 代码，可以在 GNOME 桌面环境中输入 Unicode 字符。按下 `Ctrl+Shift+U`，然后输入代码。在输入 `Ctrl-Shift-U` 后，将显示带下划线的 `u`，表示系统正在等待 Unicode 代码。

例如，希腊字母 lambda 代码为 `U+03BB`，可以通过输入 `Ctrl-Shift-U` 然后 `03BB` 输入。

## 系统默认语言设置

系统的默认语言设置为英语，使用 UTF-8 编码作为字符集（`en_US.utf8`），但可以在安装期间或之后更改。

从命令行，root 用户可以使用 `localectl` 命令更改全局区域设置。如果带参数运行 `localectl`，则显示当前的全局设置。

要设置全局默认语言，运行命令 `localectl set-locale LANG=locale`，其中 `locale` 是本节“语言代码”表中的 `LANG` 变量值。此更改将在下次登录时生效，并存储在 `etc/locale.conf`。

```bash
root@host]# localectl set-locale LANG=fr_FR.utf8
```

在 GNOME 中，管理员用户可以通过点击窗口右上角的“区域与语言”更改设置。更改登录界面的语言还将调整存储在 `/etc/locale.conf` 中的全局语言设置。

文本虚拟控制台（如 `tty4`）在显示的字体上存在限制，类似于图形环境中的虚拟控制台或 `ssh` 会话。例如，日语、韩语和中文文字可能在具有拉丁字符集的默认虚拟控制台上无法显示。

同样，文本虚拟控制台在支持的输入法上存在限制，并与桌面环境分开管理。可以通过 `localectl` 配置文本虚拟控制台和图形环境可用的全局设置。更多信息请参见 `localectl(1)` 和 `vconsole.conf(5)` 手页。

## 语言包

特殊的 RPM 包安装包含特定语言支持的软件区域设置、字典和翻译的额外 RPM 包。

要列出已安装和可能安装的包，使用 `yum list langpacks-*`：

```bash
root@host]# yum list langpacks-*
Updating Subscription repositories.
Updating Subscription repositories.
Installed Packages
langpacks-en.noarch               1.0-12.el8               AppStream
Available Packages
langpacks-mf.noarch               1.0-12.el8               rhel-8-for-x86_64-appstream-rpms
langpacks-am.noarch               1.0-12.el8               rhel-8-for-x86_64-appstream-rpms
langpacks-ar.noarch               1.0-12.el8               rhel-8-for-x86_64-appstream-rpms
langpacks-as.noarch               1.0-12.el8               rhel-8-for-x86_64-appstream-rpms
langpacks-ast.noarch               1.0-12.el8               rhel-8-for-x86_64-appstream-rpms
```

要添加语言支持，请安装适当的 `langpacks` 包。例如，以下命令添加法语支持：

```bash
root@host]# yum install langpacks-fr
```

使用 `yum repopoly --whatsupplements` 确定语言包可能安装哪些 RPM 包：

```bash
[root@host ~] yum repopoly --whatsupplements langpacks-fr
Updating Subscription Management repositories.
Updating Subscription Management repositories.
Last metadata expiration check: 0:01:33 on Wed 06 Feb 2019 10:47:24 AM CST.
glibc-getting-started-docs-fr:0:2.20-18.el8.x86_64
gnome-hunspell-fr:6.2-1.el8.noarch
hyphen-fr:0:3.0-1.el8.noarch
libreoffice-lang-fr:1:0.6.1-9.el8.x86_64
man-pages-fr:0:3.7-16.el8.noarch
mythes-fr:0:2.3-10.el8.noarch
```

> 重要

语言包使用 RPM 弱依赖，以便仅在核心包需要时才安装补充包。

例如，如前面的示例所示安装 `langpacks-fr`，只有当系统也安装了 `mythes` 字典时，才会安装 `mythes-fr` 包。

如果随后在该系统上安装 `mythes`，由于已安装的 `langpacks-fr` 包存在弱依赖，`mythes-fr` 包也将自动安装。

> 引用

`locale(7)`, `localect(1)`, `locale.conf(5)`, `vconsole.conf(5)`, `unicode(7)` 和 `utf-8(7)` 手页

图形桌面环境的 XI 布局名称与 `localect` 中名称之间的转换可以在 `/usr/share/X11/kb/rules/base.lst` 文件找到。

## 语言代码参考

> 注意

此表可能未反映系统上所有可用的语言包。使用 `yum langpacks-SUFFIX` 获取有关任何特定特定包的更多信息。

| 语言 | LANGPACKS 后缀 | $LANG 值 |
| :--- | :--- | :--- |
| 英语 (美国) | en | en_US.utf8 |
| 语言 | 语言包后缀 | $LANG 值 |
| --- | --- | --- |
