
| Filesystem | 1-blocks | Used | Available | Use | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/devdb1` | 2824932 | 2372952 | 2572080 | 9 % | `/` |
| `tmpfs` | 383916 | 12 | 383904 | 0 % | `/dev` |
| `/devdb5` | 5766924 | 1422332 | 4051744 | 26 % | `/ubuntu` |
| `/devdb7` | 6258180 | 2989250 | 3251004 | 51 % | `/debian` |
| `/devdb9` | 5766924 | 1422232 | 4051744 | 26 % | `/ubuntu` |
| `/devdb10` | 5766932 | 1872932 | 3600984 | 35 % | `/mempie` |
| `/devdb11` | 1955850 | 1370170 | 1818828 | 8 % | `/xanders` |
| `/devda2` | 1608766 | 1059343 | 5494312 | 6 % | `/windows` |
| `/devdb1` | 10742660 | 9613028 | 9781352 | 9 % | `/windows` |

## 128 介绍办公应用和工具

通常，在安装 Linux 发行版时，你必须选择特定的应用程序组进行安装。你 Linux 系统上具体的应用程序列表取决于你在安装过程中所做的选择。

```
k3b - A sophisticated kde k3 burning application
k3b-i118n - Internationalized (i18n) files for k3b
k3libs - The kde k3 burning application library - runtime files
k3libs-dev - The kde k3 burning application library - development files
```

接下来，输入 `apt-get install k3b`，几分钟后，你就会在 Debian 系统上安装好 K3b。这种安装（或升级）软件的便利性就是为什么 Debian 用户如此推崇 `apt-get` 的原因，尽管它是一个命令行工具。

## 介绍办公应用和工具

文字处理器、电子表格、演示文稿软件、日历、计算器——这些都是办公基础工具。大多数 Linux 发行版都带有 LibreOffice 应用程序套件和工具。你可以逐一尝试所有的程序，看看哪一个更合你。每个应用程序的使用都非常直观。虽然用户界面的细微差别对你来说可能是新的，但在使用几次后你就会适应它。本节介绍了以下应用程序，以及一些适用于 Linux 的商业应用程序：

- `LibreOffice` 套件：一个类似于 Microsoft Office 的办公套件，包含 `Writer` 文字处理器、`Calc` 电子表格程序、`Impress` 演示文稿、`Draw` 绘图和插图应用，以及数学公式编辑器 `Math`。
- `Kontakt`：KDE 中的个人信息管理应用。
- `Calculators`：GNOME 计算器和 KDE 计算器。
- `Aspell`：写检查器。

## LibreOffice.org 办公套件

`LibreOffice.org` 不仅仅是一个网站，还是类似于 Microsoft Office 等主流办公套件的办公套件。它的主要组件是 `Writer` 文字处理器、`Calc` 电子表格和 `Impress` 演示文稿程序。

## 介绍办公应用和工具 129

你可以通过点击面板图标或从主菜单选择，从大多数 GUI 桌面轻松启动 `LibreOffice.org`——无论是整个套件还是单个应用程序。例如，在 Ubuntu 中，你可以点击桌面图标打开 LibreOffice 套件的初始窗口。你可以从主窗口创建新文档或打开现有文档（也可以是 Microsoft Office 文件）。

### Writer

在 `LibreOffice.org` 中选择文件；新建；文档，将会在主窗口中带有一个空白文档启动 `LibreOffice.org`。使用 `Writer` 非常简单——如果你熟悉 Microsoft Word，那么在 `Writer` 中寻找应该不会遇到困难。你可以在空白文档中输入文本、进行格式化并保存文本。

你也可以打开在 Windows 上用 Microsoft Word 准备的文档。图 5-1 显示了在 LibreOffice 中打开的 Microsoft Word 文档。

![](img/71f80d7808bf5b5ad1239cc29be7bab2_148_0.png)

> 图 5-1：你可以在 LibreOffice Writer 中准备文档。

保存文档时，`Writer` 默认以 LibreDocument 格式保存，扩展名为 `.odt` 的文件。

如果你需要用 Microsoft Word 启动 `Writer` 文档，可以将文档保存为多种格式，包括 Microsoft Word 和富文本 (`.rtf`) 格式。

`Writer` 使用简单直观。如果你需要帮助，可以通过选择 `Writer` 菜单中的帮助（或在较新版本中按 F1）获取在线帮助。这将弹出带有 `Writer` 帮助信息的帮助窗口。然后你可以点击链接查看特定的帮助信息。

## 130 介绍办公应用和工具

### Calc

`Calc` 是 LibreOffice 应用程序套件中的电子表格程序。要启动 `Calc`，请从主菜单的办公类别中选择电子表格，或从任何 LibreOffice 窗口选择文件::新建;;电子表格。`Calc` 显示其主窗口，看起来类似于基于 Windows 的电子表格（如 Microsoft Excel）。（`Calc` 可以读取和写入 LibreOffice 格式的电子表格。）

使用 `Calc` 的方法与 Microsoft Excel 相同。你可以在单元格中输入内容、使用公式并格式化单元格。（例如，你可以指定值的类型和小数点后的位数。）图 5-2 显示了 `Calc` 中一个典型的电子表格。

![](img/71f80d7808bf5b5ad1239cc29be7bab2_149_0.png)

图 5-2：使用 LibreOffice Calc 准备你的电子表格。

在准备电子表格时，使用与 Microsoft Excel 相同的格式。例如，使用公式 `SUM(D2:D6)` 来加单元格 D2 到 D6 的内容。要将单元格 D2 设置为 A2 和 C2 内容的乘积，在 D2 中输入 `=A2*C2`。要了解 `LibreOffice.org` 中的可用函数，请从菜单选择帮助;;LibreOffice Org Help（或在较新版本中按 F1）。这将打开 LibreOffice 帮助窗口，你可以按类别浏览函数并点击函数以阅读更多信息。

## 介绍办公应用和工具 131

要保存电子表格，选择文件；另存为。会弹出一个对话框，你可以在其中指定文件格式、目录位置和文件名。保存文档时，`Calc` 默认以 LibreOffice 电子表格格式保存为扩展名为 `.ods` 的文件。

`LibreOffice.org Calc` 可以文件保存为多种格式，包括 Microsoft Word 和富文本 (`.rtf`) 格式。

如果你想与他人共享电子表格，可以以逗号分隔的值格式输出。

![](img/71f80d7808bf5b5ad1239cc29be7bab2_150)

### Impress

`Impress` 类似于 PowerPoint；它允许你为各种目的创建幻灯片。要启动 `Impress`，请从主菜单的办公类别中选择演示，或从任何 LibreOffice 窗口选择文件::新建;;演示。

当你第一次打开 `Impress` 时，程序会提示你选择样式和模板。要打开现有文档，选择你要打开的文件。图 5-3 显示了一个典型的演示文稿。

![](img/71f80d7808bf5b5ad1239cc29be7bab2_150_1)

图 5-3：在 LibreOffice Impress 中准备演示。

`Impress` 窗口显示幻灯片，左侧是幻灯片大视图。具体外观取决于你选择的文档类型和模板。你可以开始向幻灯片添加文本和图形。

## 132 介绍办公应用和工具

要插入新幻灯片，从菜单选择插入；幻灯片。会出现一个空白幻灯片。然后你可以在该幻灯片上添加文本和图形。保存演示文稿选择文件；保存。对于新文档，你需要提供文件名和要保存的目录。

如果你想与使用 PowerPoint 的人分享演示文稿，请将其保存为 PowerPoint 格式。

![](img/71f80d7808bf5b5ad1239cc29be7bab2_151_0)

### 日历

KDE 带有 `Contact`——这是一个将现有的 KDE 应用程序（如 `KMail` 阅读器和 `KOrganizer` 日历程序）集成在一起图形个人信息管理应用。你可以从面板图标或主菜单启动 `Contact`。（菜单的位置取决于 Linux 发行版。）
