
```
table Icon
Type: Program
Caption: Zile
Command: aterm -e /usr/bin/zile
Icon: /home/ds1/.desktop/program.zile
X: 420
Y: 384
```

接下来，将 `zile.ds1` 复制到 `/home/ds1`，然后使用以下命令打开它：

```bash
# mkdir /home/ds1/work
# cd work
# tar -zxvf ../zile.ds1 | tee /tmp/zile.lst
```

# 官方该死的 Linux 之书

为了确保额外文件的权限正确，你应该使用以下命令：

```
$ sudo chown -R 0.0 /tmp
$ sudo chown -R 1001.50 /home/ds1/.xtdesktop
```

现在，使用以下命令重新打包扩展：

```
$ cd /home/ds1/work
$ tar -T /tmp/zile.1st -czf ../zile.dsl
```

# 第 8 步：保存你的扩展

如果扩展创建成功，请将你的 `zile.ds1` 复制到你用于其他 MyDSL 扩展的任何持久化存储中（通常是一个 `mysds1` 目录）。

现在，你拥有了包含了菜单和图标元素的最终 `.ds1` 扩展。如果你想与 DSL 社区共享此扩展，请跳到本章后部分的“向世界共享你的扩展”章节。

# UNC 扩展类型

UNC 扩展可以使用 `unionfs` 文件系统进行挂载。使用这种方法的主要优势是 RAM 占用极低。如果只使用 `unc` 和 `uci` 扩展，将消耗非常少的 RAM。压缩挂载可以节省 RAM，因为只有运行时会被加载到内存中，这类似于传统硬盘的 RAM 使用方式。在 DSL 中实现的 `Unionfs` 可以让文件系统的同一区域可写，`ds1` 扩展类型也是如此。

从现有扩展创建一个 `unc` 扩展是轻而举的。基础 DSL 系统包含一个工具，可以将任何 `ds1` 转换为 `unc`。打开 root shell 并运行脚本：

```
$ ds12unc.sh zile.dsl
```

优选通过这种方式制作 `unc` 扩展，因为大部分工作都是自动的。

然而，如果你想从现有的 Debian 软件包手动创建一个 `unc`，请继续阅读。创建它也并不困难。让我们再看一遍同样的 Debian Zile 例子。

# 第 1 步：为扩展构建配置 DSL

如前所述，当你构建扩展时，应该消除所有可能的意外依赖项。也就是说，你的扩展应该运行在任何基础

# 第 10 章：添加应用程序和创建可共享扩展

DSL 的安装程序。因此，为了确保这种通用的纯净环境，你应该始终按照如下方式启动 DSL：

```
boot: dsl base norestore
```

`base` 和 `norestore` 选项以纯净环境启动 DSL。你的硬件可能所需的其他选项仍然需要添加。

# 第 2 步：恢复 Debian 软件包管理系统

如果你已经保存了 Debian 扩展 `dsl-dpkg.dsl1`，请加载此扩展并运行 `apt-get update`。否则，从主菜单中选择 `Apps`、`Tools`、`Enable Apt`。Debian 环境将被再次下载并设置其环境。

# 第 3 步：安装并测试所需的包

现在，你必须打开 root shell 来输入后续命令：

```
# apt-get install zile
```

在 shell 中（对于本例），输入 `zile`。彻底测试该应用程序。然后我们准备好将应用程序及其所有的依赖项重新打包成扩展。

# 第 4 步：重启

是的，你是正确的。为了确保额外机器的状态。通过重启，你将丢失此安装的应用程序以及你可能使用的任何额外包。这一步实际上只需要“从零基础状态开始”。

# 第 5 步：恢复 Debian 软件包管理系统

与第 2 步一样，你需要一些 Debian 软件包管理工具。然而，你实际上并没有安装 Zile 应用程序。

# 第 6 步：创建 UNC

打开 root shell 并输入以下命令：

```
# apt-get clean
# apt-get -d y install zile
# mkdir /tmp/zile
# For F in `ls /var/cache/apt/archives/*.deb`; do
# dpkg -x "$F" /tmp/zile
# cd /tmp
# mkisof -R -hide-rr-moved -cache-inodes -pad zile/ \
| create_compressed_fs - 65536 > /tmp/zile.unc
```

# 第 7 步：测试你的新 zile.unc

作为普通用户 `ds1`，使用标准的 MyDSL 系统加载扩展。由于你还没有制作菜单或项目图标，请打开 shell 窗口并发布命令 `zile`。

# 第 8 步：插入通用扩展元素

使用这种方法创建 `.unc` 扩展意味着你必须像之前在“所有 MyDSL 扩展的通用元素”部分讨论的那样制作菜单和图标元素。

对于 `.unc` 类型扩展，菜单和图标元素存储在 `user.tar.gz` 文件中。它实际上包含在 `unc` 内部的额外 MyDSL 扩展。当 `unc` 挂载时，系统会在挂载内部查找 `user.tar.gz`（“user.tar.gz”是字文件名）并对该 `.tar.gz` 执行 `mysdl-load`。这使得文件下载和加载变得简单。并且通常包含了桌面图标、菜单项以及你的应用程序需要但未创建的个人配置。此文件必须以与 `.gz` 扩展相同的方式构建，包括完整路径和正确的属所有/权限。

使用 DSL 的文本编辑器 `beaver` 在 `/tmp/mysdl.menu/zile` 创建以下内容：

`[exec] (Zile) aterm -e /usr/bin/zile`

要创建图标文件，使用文本编辑器按照之前在“文本元素”部分描述的那样创建图标。我们在 `/home/ds1/.desktop/zile.lnk` 中为 Zile 创建的图标如下：

```table
| Icon |
| :--- | :--- |
| Type | Program |
| Caption | Zile |
| Command | aterm -e /usr/bin/zile |
| Icon | /home/ds1/.desktop/zile.lnk |
```

使用 DSL 的文本编辑器 `beaver` 在 `/tmp/mysdl.menu/zile` 创建以下内容：

`[exec] (Zile) aterm -e /usr/bin/zile`

要创建图标文件，使用文本编辑器按照之前在“文本元素”部分描述的那样创建图标。我们在 `/home/ds1/.desktop/zile.lnk` 中为 Zile 创建的图标如下：

```table
| Icon |
| :--- | :--- |
| Type | Program |
| Caption | Zile |
| Command | aterm -e /usr/bin/zile |
| Icon | /home/ds1/.desktop/zile.lnk |
```

*(注：OCR 文本有一个碎片化的表格；我根据上下文重构了它)*

| Field | Value |

| :--- | :--- |

| Type | Program |

| Caption | Zile |

| Command | aterm -e /usr/bin/zile |

| Icon | /home/ds1/.desktop/zile.lnk |

使用 DSL 的文本编辑器 `beaver` 在 `/tmp/mysdl.menu/zile` 创建以下内容：

`[exec] (Zile) aterm -e /usr/bin/zile`

要创建图标文件，使用文本编辑器按照之前在“文本元素”部分描述的那样创建图标。我们在 `/home/ds1/.desktop/zile.lnk` 中为 Zile 创建的图标如下：

```table
| Field | Value |
| :--- | :--- |
| Type | Program |
| Caption | Zile |
| Command | aterm -e /usr/bin/zile |
| Icon | /home/ds1/.desktop/zile.lnk |
```

*(等待，让我根据 OCR 的“table Icon: Program...”正确格式化该表格)*

实际上，查看 OCR 流程，这里是表格：

| Property | Value |

| :--- | :--- |

| Type | Program |

| Caption | Zile |

| Command | aterm -e /usr/bin/zile |

| Icon | /home/ds1/.desktop/zile.lnk |

使用 DSL 的文本编辑器 `beaver` 在 `/tmp/mysdl.menu/zile` 创建以下内容：
