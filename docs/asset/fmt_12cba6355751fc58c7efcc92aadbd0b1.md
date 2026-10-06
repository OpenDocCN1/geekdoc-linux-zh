
...将 `my`（主机名） `mydomain` 替换为你的相关信息。

## 03 MySQL 用户

你需要另一个用户账户来访问数据库。大多数 GUI 工具会通过以下命令自动设置：

```bash
$ mysql -u root -p -h mydomain.com

GRANT ALL PRIVILEGES ON tiny_trss.* TO 'username'@'localhost';

FLUSH PRIVILEGES;
```

## 04 Tiny RSS

从馈送阅读器下载最新稳定版的 Tiny RSS，确保提取完成数据库创建所需的特定文件，然后进行设置。

![](img/511bb591be9ee7dc0f73776baf9a0548_42_2.png)

## 05 数据库设置

在存档中找到 `mysql sql` 文件

## 06 配置

将复制的文件重命名为 `config.php`，并在文本编辑器中打开它。使用相关信息编辑以下行：

![](img/511bb591be9ee7dc0f73776baf9a0548_42_3.png)

## 07 设置 URL

编辑 Tiny RSS 用于连接服务器上数据库和服务的配置文件。更改其周围的值，确保创建一个副本以便你可以恢复或重新开始。你可以在配置的左上角找到它。

```php
define('SELF_URL_PATH', 'http://example.org/tt-rss/');
```

将示例更改为你的域名，你可以保留 `tt-rss` 或选择任何打算安装 Tiny RSS 的名称。

## 08 配置

将复制的文件重命名为 `config.php`，并在文本编辑器中打开它。使用相关信息编辑以下行：

`www.linuxuser.com`

# 教程 创建你的 Google Reader

![](img/511bb591be9ee7dc0f73776baf9a0548_43_0.png)

## 10 下载

保存文件后，回到终端并登录你的网络空间。使用以下命令创建 `tiny-rss` 文件夹：

```bash
mkdir tt-rss
```

进入目录，然后使用以下命令下载最新版本的 Tiny RSS `rss`：

```bash
wget https://github.com/gothfix/Tiny-RSS/archive/v1.9.tar.gz
```

## 11 解压

将以下文件解压到你的目录：

```bash
tar -zvf 1.9.tar.gz
```

确保所有文件都已从文件夹解压，这样当你导航到 `tt-rss` 文件夹时，它是打开的。

## 12 更新

通过 FTP 或下载方法将你创建的配置文件移动到你的空间，或者按照我们之前的方法编辑配置文件。你也可以使用 FTP 程序将文件移动到空间，而无需在终端中进行任何操作。

![](img/511bb591be9ee7dc0f73776baf9a0548_43_1.png)

## 13 登录

现在我们可以进入了。访问你指定的 URL 你将看到登录界面 - 现在使用 `admin` 和密码。登录后，前往 `Actions/Preferences/Personal`。`Data/Authentication` 并更改密码。

## 14 导入馈送

如果你已经从 Google Reader 获取了数据，现在可以将其导入 Tiny RSS。进入 `Acts` 菜单并选择 `feeds`，然后选择 `OPML`。点击“Choose file”，导航到你的 `subscriptions.xml` 然后点击 `Import`。如果你有结构文件夹，它将创建。

就像 Google Reader 一样，但现在你可以编辑偏好来查看馈送是如何工作的。如果你的馈送没有显示在任何地方，不要担心 - 我们稍后会修复它。如果你在文件夹中没有看到任何馈送，你可以加载一些最新条目。你还可以开始编辑馈送项目的显示方式，按从旧优先，而不是如何显示已读项目。

## 15 阅读

请注意 Tiny RSS 将无法工作

![](img/511bb591be9ee7dc0f73776baf9a0548_43_2.png)

Tiny Tiny RSS 的工作将像 Google Reader 那样消失

`tinylux.com`

# 创建你的 Google Reader

使用 Tiny Tiny RSS 创建一个 Google Reader 的替代品

# 教程

![](img/511bb591be9ee7dc0f73776baf9a0548_44_0.png)
![](img/511bb591be9ee7dc0f73776baf9a0548_44_1.png)
![](img/511bb591be9ee7dc0f73776baf9a0548_44_2.png)
![](img/511bb591be9ee7dc0f73776baf9a0548_44_3.png)
![](img/511bb591be9ee7dc0f73776baf9a0548_44_4.png)
![](img/511bb591be9ee7dc0f73776baf9a0548_44_5.png)
![](img/511bb591be9ee7dc0f73776baf9a0548_44_6.png)
![](img/511bb591be9ee7dc0f73776baf9a0548_44_7.png)
![](img/511bb591be9ee7dc0f73776baf9a0548_44_8.png)

## 16 配置

有两种方式可以：

## 17 更新

如果你在服务器上使用 Tiny RSS。

## 18 查看

默认情况下，你可以看到：

## 19 快捷键

快捷键略有不同。

## 20 添加馈送

它似乎可以重新排列到一个。

## 21 重新排列

就像所有其他一样，Tiny RSS 是为了。

## 22 Android

如果你习惯了 Android，你会很高兴发现。

## 23 更新

这不是一个问题，尽管在便携式、USB 外部硬盘上。

## 24 保持

这些是你可以进行的所有调整，例如：

# 教程 简单步骤：从外部硬盘双启动

![](img/511bb591be9ee7dc0f73776baf9a0548_45_0.png)

创建一个可以在硬盘上的每个安装之间切换的 GRUB 菜单：

```
grub version 2.02-ubuntu2

Boot with Linux 5.15.0-76-generic

Boot with Linux, kernel (recovery mode)

Advanced options for Ubuntu

  Linux 5.15.0-76-generic

  Linux 5.15.0-76-generic (recovery mode)

Select enter 启动选定的项或 e 进入命令行
```

随身携带你的发行版到任何地方，这样在有电脑的地方就可以使用

在两个发行版之间创建共享空间，以便数据可以轻松共享

# 资源

一个具有至少 75GB 空间的 USB 供电外部硬盘

在这里我们展示了如何在外部硬盘上分区、安装和运行两个发行版。我们在示例使用了 Fedora 和 Ubuntu，因为它们是两个最常见的发行版。

# 简单步骤：从外部硬盘实现双启动

设置一个包含两个发行版的便携驱动器

# 教程

## 交换分区 (Swap partition)

在示例中，我们将从 Ubuntu 开始。插入 USB 驱动器并进入 Ubuntu。确保你已将重要数据保存在外部硬盘上。你需要的第一件事是创建一个交换分区——将其大小设置为 4GB，并放置在硬盘末尾。

![](img/511bb591be9ee7dc0f73776baf9a0548_46_0.png)

## 安装新的 Fedora 19

此部分包含你 Fedora 19 安装的手动挂载点。你可以：
- 点击 "+" 按钮创建新的挂载点
- 将挂载点分配给现有分区
- 为现有分区分配交换分区的挂载点

| 名称 | 大小 | 类型 |
|---|---|---|
| sda1 | 500 MB | linux |
| swap | 2.0 GB | linux |
| root | 18.35 GB | ext4 |

## Linux 适用于 16gb

安装设计：在剩余空间中创建一个 `ext4` 格式的自定义分区，并将挂载点设置为 `/`。安装。

## 查找 fstab

输入以下命令：

```
ls -l /dev/sdX-by-uuid
```

## 共享空间

你可以为两个发行版创建一个共享空间，可以独立创建，也可以作为共享家目录（home）。我们希望在创建时为共享家目录设置 15GB。使用 `ext3` 或 `ext4` 作为文件系统，如果你需要跨平台，则使用 `NTFS`。

## 安装 GRUB

进入 Ubuntu Live 系统，并记录哪个磁盘标签将 Ubuntu 根分区标记为外部硬盘。

以找到硬盘上共享分区的 UUID。该 UUID 在 Ubuntu 和 Fedora 中是相同的。进入终端并使用文本编辑器打开 `fstab`，以便：

```
$ sudo mount /dev/sdX /mnt
```

![](img/511bb591be9ee7dc0f73776baf9a0548_46_1.png)

## 使用 fstab

你需要添加一个新条目，以便每次启动到其中一个外部硬盘时都会挂载共享空间。输入内容：

然后通过 Ubuntu 重新安装 GRUB：

```
$ sudo grub-install --root-directory=/mnt/ /dev/sda
```

```
UUID=mount point ext4

error=remount-ro 2
```

## Ubunturoot

为 Ubuntu 创建 15GB 的空间并在菜单中选择将其设置为根目录。它会自动找到以后启动 Ubuntu/Fedora 时使用的交换分区。继续执行安装说明。

## 更新 GRUB

重启后，你可以回到 Ubuntu 硬盘。然后进入 Fedora 分区，并运行：

## 实现便携化

你最终可以在随处设置便携式 Linux，它们之间有一个共享空间，并且可以在它们之间切换启动，而无需猜测哪一个是哪个。

# Fedora 目录

在插入 USB 硬盘的情况下插入 Fedora 并启动。在磁盘列表中选择外部硬盘。

```
$ sudo update-grub
```

它将自动检测 Fedora 安装，并在下次从硬盘启动时更新启动菜单。

![](img/511bb591be9ee7dc0f73776baf9a0548_46_2.png)

`42 www.linuxux.co.uk`

# 使用 Graphviz 可视化目录结构

运行 `visDir.pl` Perl 脚本并使用 `dot` 创建 PDF 文件

`visDir.pl` 脚本的一部分 一个简单的 Graphviz 图形 Linux 内核目录结构的一小部分！

![](img/511bb591be9ee7dc0f73776baf9a0548_47_0.png)

# 使用 Graphviz 可视化目录结构

使用此开源包使大型目录结构变得实用

## 顾问

Vitalis Tsoukalis 拥有 15 年的 Unix 系统管理和编程经验。他在 Oracle 数据库管理、C++ 和 Java 编程方面也是专家。

Graphviz 是用于处理图形结构和生成布局的工具集合。支持有向图和无向图，并提供图形界面。

`dot` 是一个使用圆形布局绘制图形的实用程序。选择一个节点作为中心，其他节点环绕中心放置。如果一个节点连接到节点，则位于距离 2 处。

Graphviz 包含许多程序和库。`dot` 程序接受 `dot` 语言并生成各种类型的图形：节点和边。`Neato` 是一个用于绘制无向图的程序。`circo` 是一个用于创建圆形布局的实用程序，`fdp` 是一个用于构建大型无向图的实用程序。`fdiop` 程序

Graphviz 提供了三个图形界面：`doty` 是用 Tcl 编写的可定制图形界面。还有两个库叫做 `libraph` 和 `libigraph`。它们的存在意味着可以使用 Graphviz 作为库而不是工具。

# 资源

Graphviz: http://www.graphviz.org

Perl: http://perl.org

Perl Graphviz 模块: search.cpan.org/~cro/Graphviz-22/lib/Graphviz.pm

Graphviz 输出格式：www.graphviz.org/doc/output.html

# 使用 Graphviz 可视化目录结构

使用此开源包理解大型目录结构

# 教程

![](img/511bb591be9ee7dc0f73776baf9a0548_48_0.png)

## 01 为什么使用 Graphviz？

可视化像 Linux 内核这样的目录结构是实用的。Linux 内核有超过 2000 个目录和 27000 个文件，否则将非常难以观察。我们的 Perl 脚本输出可以包含文件以及大小。通过分析网络、跟踪函数调用等，你可以获得 Graphviz 知识。这有很多好处。

注意：对于像内核内核这样的目录结构，有时最好不要一次性可视化，而是分成部分。

![](img/511bb591be9ee7dc0f73776baf9a0548_48_1.png)

```
"Hello world";
```

```dot
digraph G {
  node [label="Hello world!"];
}
```

使用以下命令编译：

```
$ dot -ps hw.dot -o hw.ps
```

上述命令将生成一个你可以查看的 PostScript 文件。这意味着将创建一个图。对于无向图，应该使用。对于简单的示例，图是有向还是无向并没有区别。

虽然 PostScript 非常流行，但建议使用 PDF 格式，因为渲染和显示更快。此外，PDF 文件放大时不会丢失清晰度。

## 04 基础图形信息

图 `(V, E)` 是 `V`（节点）和边 `E` 的非空集。图包含节点和边，每个都有属性。Graphviz 有你可能想要学习的自己的方言。这种语言可能简单优雅，但非常强大。好处它是一个简单的纯文本编辑器——你可以轻松编写生成 graphviz 的脚本。

通过编写 graphviz 代码，你会发现带有 `#` 的行是重要的。

## 节点属性

| 名称 | 解释 | 允许的值 |
| --- | --- | --- |
| shape | 节点的形状 | 椭圆、菱形、圆形等 |
| width | 节点的宽度 | 数字 |
| height | 节点的高度 | 数字 |
| color | 节点的颜色 | 颜色 |
| font | 节点的字体 | 字体 |
| style | 节点的样式 | 粗体、虚线、点状、等 |

## 02 安装并运行 Graphviz

你的 Linux 发行版提供了一个可以安装即可使用的 Graphviz 包。例如，你只需要运行以下命令即可安装 Graphviz：

```
# apt-get install graphviz
```

安装 Graphviz 后，尝试编译以下 Graphviz 代码：

```
digraph G {
```

## 03 Perl Graph 模块

使用 Perl 包（包括 `Perl::Graph`）为创建 Graphviz 提供接口。Perl 模块被作为生成 Graphviz 的替代方案。

在使用 Graphviz 模块时，记住这一点很有用：如果你想获取输出为 PNG 文件，程序的最后一行应该是：

```
print \$Graph->as_text;
```

同样，如果你想获取输出为文本，请使用以下行：

```
print \$Graph->as_text;
```

## 边属性

| 名称 | 解释 | 允许的值 |
| --- | --- | --- |
| penwidth | 边的粗细 | 数字 |
| color | 边的颜色 | 颜色 |
| style | 边的样式 | 粗体、虚线、点状、等 |
| arrowhead | 箭头的方向 | 向、向后或无 |
| label | 边的标签 | 字母数字字符 |

`49 www.linuxer.com`

# 教程

## 使用 Graphviz 可视化目录结构

![](img/511bb591be9ee7dc0f73776baf9a0548_49_0.png)

```
"articles.viz"[label="articles.viz"]
"articles.viz" -> "home/msouk/docs/article/working/Graphviz.LUD"
"visdir.pl"[label="visdir.pl 3628b"]
"visdir.pl" -> "home/msouk/article/working/Graphviz.LUD"
"docs.pdf"[label="docs.pdf 4488b"]
"docs.pdf" -> "home/msouk/article/working/Graphviz.LUD"
"code.viz"[label="code.viz 371b"]
"code.viz" -> "home/msouk/article/working/Graphviz.LUD"
"code.pdf"[label="code.pdf 3268b"]
"code.pdf" -> "home/msouk/article/working/Graphviz.LUD"
"dir.viz"[label="dir.viz 80"]
"dir.viz" -> "home/msouk/article/working/Graphviz.LUD"
"home/msouk/article/working/Graphviz.LUD"[label="figures"]
```

- `kernel.viz`

- `$ neato -pdf kernel.viz -o kernel.viz`

如你所知，Graphviz 软件套包含许多用于创建图表的工具。对于节点大量的图表，你应该根据任务找到合适的工具和参数。该工具生成的 Linux 目录结构输出没有使用 `neato` 工具创建的图表那么漂亮。
