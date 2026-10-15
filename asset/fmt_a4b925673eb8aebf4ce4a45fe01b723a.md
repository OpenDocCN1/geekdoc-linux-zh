
如果你更喜欢使用鼠标而不是键盘来插入 HTML 标签，这个包可能正合你意。Heiko Münkler 编写了 `hm—html-menus`，作为一个 HTML 新手可以使用的包，同时具备足够多的功能来吸引 HTML 老手。最新版本 `5.9` 已有几年历史，但它与 GNU Emacs 和 XEmacs 都兼容良好。XEmacs 包维护者对其进行了一些修改，使该模式能很好地集成到新的打包方案中。按照第 12 章的说明安装 XEmacs 包。

安装 GNU Emacs 只需将本书 CD-ROM 上的 Lisp 文件复制过来即可。你可以在目录 `/cdr/m/packages/hm—html-menus` 中找到所需的文件。将文件安装到你的 `site-lisp` 目录中，并将 Info 文档文件安装到 `/usr/local/info`。你也可以从 `ftp://ftp.tnt.uni-hannover.de/pub/editors/xemacs/contrib` 获取该包。

激活此包并将其设为 HTML 文件的默认模式，需要在 `~/.emacs` 文件中添加相当大的一堆 Lisp 代码。我想你不想重新输入必要的代码，所以我把它放在了一个名为 `config.el` 的文件中，你可以在 CD-ROM 上的 `/cdr/m/packages/hm—html-menus` 目录中找到。你可以从该文件或随包附带的 `hm—html-menus` Info 文件中复制粘贴。如果你已安装 `html-helper-mode`，需要用分号注释掉该模式的激活行。

![](img/c8827ea52a0796def3f6891892ed9d3a_246_0.png)

图 13.4 `bm—html` 鼠标菜单

与 `html-helper` 不同，此包的大多数功能位于鼠标按钮菜单中，而不是菜单栏菜单中。图 13.4 显示了主鼠标菜单和其中一个子菜单。

此包比 `html-helper-mode` 有更多的标签键绑定，但其中许多绑定较长，难以记忆和使用。例如，表格标签的绑定是 `Ctrl-c Ctrl-s Ctrl-t t`。这就是我前面建议此包给偏好鼠标而非键盘命令的用户的原因。从菜单中选择比输入如此复杂的命令更快。

不知何故，XEmacs 包维护者在将 `hm—html-menus` 变成官方 XEmacs 包时更改了许多键绑定。如果你同时使用 GNU Emacs 和 XEmacs，这可能会令人烦恼和困惑。

`hm—html-menus` 以一种巧妙的方式处理反复出现的用标签包围选定文本区域的需求。注意图 13.4 中，菜单标题是“HTML Region Expert Menu”；如果你选择了一些文本，标题会变为“HTML Region Expert Menu”；从菜单中选择的任何标签现在都会包围选定的区域。

`hm—html-menus` 包含一个模板次要模式，名为 `tmpl-minor-mode.el`，可用于任何主要模式的模板扩展。当你创建一个新 HTML 文件时，此次要模式会发挥作用。你会在 `minibuffer` 中被提示模板文件的位置。输入你安装 `hm—html-menus` 的目录，它将在未来的会话中记住。该包附带一个示例模板，但你需要编辑它或将其作为模型来编写自己的模板。

## psgml 和 HTML

`psgml` 是由 Lennart Ståfflin 开发的一个大型且复杂的包，旨在帮助使用 SGML 文档的编写者。由于 HTML 是 SGML 的子集，它也是

虽然 XEmacs 对 HTML 的支持更好，但使用 `pshtml` 来编写 HTML 文档也是可行的。

随附的此软件包并未专门配置为用于处理 HTML 文档，但将 `hm-html-menus` 作为次要模式与 `pshtml` 结合使用，可以提供一个相当有效（尽管复杂）的 HTML 编辑环境。`pshtml` 具有文件解析功能。换句话说，它可以通读文件并检查语法错误。它还可以与 `sgmls` 外部解析器配合使用。

在 XEmacs 中安装 `pshtml` 只需获取预配置的软件包即可，具体步骤详见第 12 章。XEmacs 版本的 `pshtml` 与发布版本有很大不同。`hm-lhelp.el` 模式的大量部分已被整合进去；总体而言，该模式更适合进行 HTML 编辑。

要将 `hm-html-menus` 用作次要模式（假设你已安装了 `hm-html-menus` 软件包），请将以下行插入到 `~/.emacs` 文件中：

```
(add-hook 'html-mode-hook 'hm-html-minor-mode)
```

请分别尝试使用启用和未启用 `hm-html-menus` 作为次要模式的 `pshtml`；两者结合使用可能超出了你的实际需求。图 13.5 显示了同时启用两种模式时的菜单布局。

这是一个包含三个部分的复杂菜单和子菜单阵列。靠近左侧的新增项目是 `pshtml` 菜单：Modify（修改）、Move（移动）、Markup（标记）和 DTD。在编写 HTML 时，你可以忽略这些菜单下的大部分项目，因为它们涉及的是 SGML 而非特定的 HTML。DTD 菜单适用于 HTML 文件。

![](img/c8827ea52a0796def3f6891892ed9d3a_247_0.png)

> DTD（文档类型定义）是一种对应于特定类型 SGML 文档的文本文件。DTD 定义了可以在像 HTML 这样的标记语言中使用的有效元素。SGML 解析器（例如 `pshtml` 中包含的那个）会解析（读取并吸收）HTML DTD，并在验证 HTML 文件时使用这些信息。你可以将验证视为一种帮助你编写正确 HTML 的错误检查。

HTML 已经演变成一种执行起来相当随意的语言。网络浏览器可以处理并显示格式错误或是不完整的 HTML。为了利用 `pshtml` 的验证功能，HTML 文件的第一行应声明 DTD，因为 HTML 有几个版本，因此可能存在多个 DTD。第一行应该类似于以下内容：

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional/EN">
```

本书中讨论的所有 HTML 模式都在其新文件的默认模板中包含这样一行。

组成 XEmacs `pshtml` 软件包的文件中，包括了一套针对不同版本 HTML、Docbook（一种用于技术文档的 SGML 软件包）以及 XML 的 DTD。当你使用 `pshtml` 检查你的 HTML 文件时，会参考其中某一个文件。

沿着菜单栏向右看，你会找到 `hm-html` 次要模式菜单，它与 `hm-html-menus` 作为主要模式时显示的菜单类似。此菜单中最有用的项目包括用于设置鼠标菜单技能级别（新手或专家）的切换项，以及将当前缓冲区加载到网络浏览器中的项目。当 `hm-html-menus` 作为 `pshtml` 下的次要模式时，其鼠标菜单与 `hm-html-menus` 主要模式的鼠标菜单相同（参见图 13.4）。

最后两个新菜单属于 `pshtml` 的 HTML 模式。图 13.6 中的 HTML 菜单包含几个实用功能，其中一些与 `hm-html-menus` 菜单上的项目重复，例如文件预览功能。此菜单中的 Validate（验证）项会根据相应的 DTD 检查你的文件，并指出任何语法错误。这是 `pshtml` 的强项。

图 13.7 中的 Insert（插入）菜单是一系列嵌套菜单，充满了标签插入命令。这些命令是从 `html-helper-mode` 中引入的，但具有不同的键绑定。此菜单与原始 `html-helper` 菜单的一个显著区别是，每个菜单项旁边没有显示键绑定。这很遗憾，因为在 `html-helper-mode` 和 `hm-html-menus` 中显示键绑定都是一种方便的学习辅助。你可以按 `C-h b`（模式键绑定帮助键）查看 `pshtml` 键绑定的列表。

![](img/c8827ea52a0796def3f6891892ed9d3a_248_0.png)

![](img/c8827ea52a0796def3f6891892ed9d3a_249_0.png)

图 13.7 插入菜单

与前两个描述的 HTML 模式不同，基于 XEmacs `pshtml` 的 HTML 模式没有附带任何特定文档。`pshtml` 本身有一套全面的 Info 文件，但重点在于通用的 SGML，并未提及 HTML 编辑。你可以通过尝试和错误来学习此模式。选择各种菜单项，看看它们的用途是否对你有用。最终，你会在学习忽略其他命令的同时，发展出一套有用的命令工具包。

此 HTML 模式的主要优势在于其验证和错误检查能力。与其他 HTML 模式相比，其标签插入菜单更难使用，而且对于面向键盘的用户来说，键绑定过长。使用此模式的一种可能方法是在其他 HTML 模式之一中进行大部分编辑，然后使用 `pshtml-html` 来检查你的文件。
