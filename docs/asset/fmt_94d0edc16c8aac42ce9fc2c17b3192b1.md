
# 第 7 章 GNOME 桌面管理器

| 菜单项 | 说明 |
| --- | --- |
| 使用默认背景 | 将桌面背景更改为正在使用的框架默认背景。 |
| 更改桌面背景 | 显示背景窗口，你可以用它更改桌面背景。 |

- 当你在命令行界面工作时，应避免在文件名中使用空格，因为空格很难处理。然而，GNOME 鼓励使用空格。

## 更改输入焦点

你可以根据窗口管理器的设置（207 页），通过各种方式点击窗口来更改输入焦点（182 页）。要让工作区上的每个窗口轮流激活，按住 ALT 键并反复按 TAB。当你按住 ALT 键时，默认会在桌面中心显示一个框，显示窗口标题栏（181 页）的内容，如果你松开 ALT 键，该窗口将移动到窗口栈的顶端。

## 菜单

GNOME 有许多菜单。表 7-4 列出了所有常见菜单以及在何处查找每个菜单的相关信息。

| 菜单 | 说明 |
| --- | --- |
| 上下文 | 参见第 184 页的“上下文菜单”。 |
| 桌面 | 参见第 212 页的“桌面菜单”。 |
| 通用图标 | 右键点击任何不在面板上的图标（第 208 页）。 |
| 帮助 | 参见第 205 页的“帮助菜单/工具栏选择”。 |
| 主菜单 | 参见第 208 页的“GNOME 菜单”。 |
| 菜单 | 参见第 253 页的“菜单菜单”。 |
| 菜单面板 | 参见第 246 页的“菜单面板”。 |
| Nautilus 栏 | 参见第 220 页的“菜单栏”。 |
| 面板 | 参见第 250 页的“面板菜单”。 |
| 面板图标 | 右键点击面板上的任何对象（第 212 页）。 |
| Sawfish | 参见第 258 页的“Sawfish 菜单”。 |
| 窗口列表 | 参见第 211 页的“窗口列表和工作空间切换小组件”。 |
| 窗口操作 | 参见第 256 页的“窗口操作菜单”。 |

## Nautilus: 文件管理器

Nautilus 有许多功能。² 本节讨论作为文件管理器的 Nautilus。当 Nautilus 未打开时，双击工作区左上角的“主目录”图标或选择 GNOME 菜单中的“主文件夹”，即可打开显示主目录内容的 Nautilus 窗口（图 7-6，第 217 页），该窗口使用图标（默认）表示文件。

² 截至 Red Hat 8.0 版本发布时，Mozilla 尚未适配 GTK 2，因此 Mozilla 无法与 Nautilus 链接，导致 Nautilus 失去了大部分 Web 浏览功能。在浏览网站时打开侧边栏；Nautilus 会提供在另一个浏览器中打开 URL 的选项。

### 可选项

#### URI

URI 是统一资源标识符（Uniform Resource Identifier）的缩写。URI 的格式非常熟悉，因为 URL（第 407 页）如 `http:` 和 `ftp:` 是 URI 的子集。Nautilus 使用 URI 来指定特殊位置。URI 中冒号之前的部分称为方案（scheme），由 `gnome-vfs`（虚拟文件系统）模块处理。`gnome-vfs` 的工作原理是每个方案都可以有自己的处理代码。标准代码处理标准的 URI 方案，如 `http:` 和 `ftp:`。由 Red Hat 引入的特殊代码则处理非标准的 URI。

登录时，许多系统会显示 Nautilus 窗口，显示“在此开始”（`start-here`）；以下是“在此开始”显示的条目的位置：

- `start-here:` `/etc/X11/startherse`
- `server-settings:` `/etc/X11/serverconfig`
- `system-settings:` `/etc/X11/systemconfig`

`/etc/X11/startherse` 中的所有文件都是 Desktop 文件。结合其他信息，这些文件中的每个都包含一行以 URL (URI): 开头的内容：

```
$ cd /etc/X11/startherse; grep URL *
applications.desktop:URL=applications://
preferences.desktop:URL=preferences://
serverconfig.desktop:URL=server-settings://
systemconfig.desktop:URL=system-settings://
```

这些 URI 中的每一个都指向某处；前面的列表告诉你在何处。通常情况下，URI 与文件系统位置之间没有对应关系。

### Desktop 文件

带有 `.desktop` 文件扩展名的文件存储了关于它们应该如何显示以及指向何处的信息。以下简化的文件显示了在“在此开始”窗口中的系统设置图标（`Icon-system_settings.png`，此处为 `sysconfig.desktop`）。它是指向“偏好设置”（`URL=preferences:`）的链接（`Type=Link`）。其意大利语名称为 Preferenze（`Name[it]=Preferenze`）。注释也包含默认值和意大利语值。当你查看系统上的该文件时，你会发现文件中包含了多种语言。

```
cat /etc/X11/starthere/sysconfig.desktop
Type=Link
Name=System Settings
Name[it]=Impostazioni di sistema
Comment=Change system settings
Comment[it]=Modifica impostazioni del sistema
Icon=system-settings.png
Encoding=UTF-8
URL=preferences://
```

**在此开始**（图 7-5）

登录时，许多系统会显示 Nautilus 窗口，显示“在此开始”（`start-here`）；以下是“在此开始”显示的条目的位置：

- `start-here:` `/etc/X11/startherse`
- `server-settings:` `/etc/X11/serverconfig`
- `system-settings:` `/etc/X11/systemconfig`

### Nautilus 鼠标操作（续）

查看父级文件夹：点击 Nautilus 工具栏上的向上箭头。

打开对象：请参考下文的“打开文件”。

![](img/aa8214d49e1cf50152c432845129fb3b_268_0.png)

图 7-7 Nautilus 在窗口底部显示工具栏并列出列表。

### 打开文件

你可以双击⁴一个文件或图标来打开它，也可以右键点击文件并在弹出菜单中选择“打开”。当你打开一个文件时，Nautilus 会尝试确定使用哪种工具来打开它，它使用 MIME（第 178 页）将文件名扩展名与 MIME 类型及程序关联起来。当你打开扩展名为 `.ps` 的文件时，Nautilus 会调用 `gs`（ghostscript），它会以可读格式显示 PostScript 文件。当你打开像 Mozilla 等可执行文件时，Nautilus 会运行该可执行文件。当你打开文本文件时，Nautilus 会打开一个文本编辑器，显示并允许你编辑该文件。当你打开一个目录时，Nautilus 会显示其内容。当 Nautilus 不知道使用哪种工具来打开文件时，它会询问你。请参阅第 232 页的“文件类型和程序（MIME 类型）”获取自定义信息。

### 控制栏

本节讨论了最初出现在 Nautilus 窗口顶部的三个控制栏——菜单栏（图 7-8）、工具栏和位置栏。

- 4. 如果你的系统设置为“单击打开”，则只需点击一下即可打开。请参阅第 243 页的“点击行为”。

### 菜单栏

当你点击菜单栏中的某一个选项时，它会呈现下拉菜单。表 7-6 显示了菜单选择并描述了每个选择中的各个选项。Nautilus 会根据其在子窗口中显示的内容改变其菜单选择。

![](img/aa8214d49e1cf50152c432845129fb3b_269_0.png)

图 7-8 Nautilus 菜单栏

### Nautilus 菜单栏

| 文件 | 说明 |
| :--- | :--- |
|  | 你可以右键点击文件以获得略有不同的“文件”菜单。 |
| 新窗口 | 创建另一个 Nautilus 窗口，复制你当前操作的窗口。 |
| 新文件夹 | 在工作目录（显示在位置栏上）中创建一个文件夹。将名称从“未命名文件夹”更改为此名称。如果此方法失败，请右键点击文件夹并选择“重命名”。 |
| 打开 | 根据文件类型打开选中的图标/文件。 |
| 在新窗口中打开 | 与“打开”相同，但在适当的情况下，打开的对象将出现在新窗口中。 |
| 用...打开 | 提供可选应用程序和/或查看器来打开选中的图标/文件。 |
| 脚本（脚本列表） | `~/.gnome2/nautilus-scripts` 中的可执行文件列表。选择其中一个文件并执行它。Nautilus 将在子窗口中选中的文件名作为参数。 |
