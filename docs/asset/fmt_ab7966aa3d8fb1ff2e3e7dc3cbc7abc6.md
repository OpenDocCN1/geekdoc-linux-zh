
## 关于列含义的信息

字母`EIOM`分别代表错误（error）、已安装（installed）、旧标记（old mark）和标记为（marked for）。如果`dselect`检测到依赖项冲突并更改`M`列中的设置，则`O`和`M`列之间会出现差异（见下文）。

### 列 E（错误）
*   空格：正常状态。
*   `R`（重新安装）：在之前的安装尝试期间发生错误。该软件包需要重新安装。

### 列 I（已安装）
*   空格：未安装该软件包，也没有安装任何配置文件。
*   `+`：软件包将被安装。
*   `-`：软件包将不被安装，但之前的安装留下了配置文件。
*   `U`, `C`或`I`：软件包已安装，但在安装过程中发生了错误。

### 列 O（旧标记），M（标记）
*   `+`：软件包将被安装。
*   `-`：软件包将被移除，但将保留配置文件。
*   `-`：软件包将同其配置文件一起移除。
*   `=`：软件包将保持不变（'hold'，阻止自动更新）。
*   `n`：软件包是新的；没有可用的安装信息。

### 列 Pri（优先级）
此列指定了软件包对系统的重要性。可能的值有`Req`（需要）、`Imp`（重要）、`Std`（标准）、`Opt`（可选）或`Xtr`（额外）。

### 列 Section（区域）
此列将软件包分配给一个类别。可能的类别有：`admin`, `base`, `comm`, `contrib`, `doc`, `dev`, `editors`, `electronics`, `games`, `graphics`, `hamradio`, `interpreters`, `libs`, `mail`, `math`, `misc`, `misc`, `net`, `news`, `non-free`, `others`（用于其他操作系统的工具或文件系统），`shells`, `sound`, `text`, `util`, `web`和`x11`。

其余列较易描述：软件包名称、当前安装的版本号、`CD-ROM`上的软件包版本、简要描述。更详细的描述可以在屏幕下半部分找到。使用`T`可以在信息文本的不同模式之间切换，你可以（在可能）使用`U`和`D`进行翻阅。

## dselect 快捷键

| | |
|---|---|
| `Home`, `End` | 跳到开头或末尾 |
| `N`, `P` | 滚动上一个/下一个 |
| `Shift+B`, `Shift+F` | 搜索 |
| `+`, `Ins` | 安装（删除） |
| `=` | 不更改安装状态 |
| `V` | 显示（详细） |
| `O` | 更改排序 |
| `I` | 更改信息（依赖关系） |
| `U`, `D` | 翻阅信息（向上/向下） |
| `←` | 退出；返回主菜单 |
| `?` | 显示帮助 |

通常，软件包选择的工作方式如下：你搜索软件包（主要使用`T`）并使用`+`安装或使用`-`卸载。当你认为已完成所有设置时，退出`dselect`。

## Package dependencies（软件包依赖关系）

一旦你选择了一个依赖于其他软件包的软件包，就会出现一个显示缺失软件包的新屏幕。此列表显示了应该安装的所有软件包。需要的软件包已被标记为安装，而仅推荐的软件包未标记。以下行显示了`tkman`的未解决依赖关系。

```
* Xtr non-free tkman A graphical, hypertext, manual page browser.

* Opt libs tk42 The Tk toolkit for TCL and X11 v4.2 - Run-Time

* Xtr non-free rman Reverse compile pages

* Opt libs tcl76 Tool Command Language (TCL) v7.6 - Run-Time
```

```
tkman depends on tk42

tkman depends on rman

tk42 depends on tcl76 (>= 7.6-0)
```

在简单的情况下，你退出依赖页面。在这种情况下，直接接受所有设置。

然而，在按下之前，你也可以使用选择可选软件包进行安装，从而更改默认设置。但是，在存在未解决依赖关系的情况下，无法离开。（如果你知道自己在做什么，可以使用`Q`强制接受你的设置。）

如果所需软件包的范围太大，你想撤销对引起冲突软件包的选择，只需按`X`。

## dpkg

`dselect`为软件包安装和管理提供了一个较为友好的界面，但相同的任务可以通过命令行驱动的`dpkg`命令来实现。作为`Debian`用户，你通常使用`dpkg`。如果你想快速安装单个软件包（例如从额外的`contrib` CD中），`dpkg`是`dselect`的高效替代方案。不同的`dpkg-xyz`命令对于你想要构建自己的软件包来说通常非常有用。

### DEBIAN GNU/LINUX 2.1

```
dpkg --install package_file
```

此命令安装指定的软件包。如果已经安装了旧版本，它将被新版本替换。以下示例显示了图形程序`xv`的安装，它作为非自由（`non-free`）软件包包含在`contrib` CD中。

```
# dpkg --install /cdrom/debian/non-free/binary-i386/graphics/xv_3.10a-20.deb
```

正在选择之前取消选择的`xv`。
(正在读取已安装的 4537 个文件和目录)
正在解压`xv`(来自`.../graphics/xv_3.10a-20.deb`)
正在设置`xv`(3.10a-20)...

`Update-menus`: 等待`dpkg`完成（正在后台派生）

`Update-menus`: 正在检查`/var/lib/dpkg/lock`

```
dpkg --configure package_name
```

此命令用于重新配置已安装的软件包。请注意，你不需要指定完整文件名（带有`*.deb`扩展名），只需要不带路径和扩展名的软件包名。

```
dpkg --remove package_name

dpkg --purge package_name
```

这两个命令用于删除指定的软件包。在第二种变体中，配置文件也会被删除。

```
dpkg --list

dpkg --list 'pattern'
```

在第一种语法变体中，`dpkg`显示所有实际安装的软件包。第二种变体还考虑了在上次菜单项`UPDATE`中选择时被注册为可用的所有未安装软件包。

```
dpkg --listfiles package_name
```

此命令显示软件包的所有文件。该命令仅对已安装的软件包有效。未安装软件包的内容可以通过`dpkg-deb --contents file_name`显示。

```
dpkg --search file_name
```
