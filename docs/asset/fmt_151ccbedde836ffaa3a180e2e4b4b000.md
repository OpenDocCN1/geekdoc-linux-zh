
文稿是我们工作生活中不可或缺的一部分。当你需要展示想法、团队表现时，你的演示稿就是你最好的工作。虽然制作演示稿是视觉化表达想法的极佳方法，但当制作所有演示稿的工具基于 GUI 时，可能会出现控制问题。虽然有很多选项和按钮，但大多数选项在 90% 的演示中都没有被使用。因此，侧边编辑花费的时间比应该的要得多。

另一个大问题也存在：我们大多数人都在某个时候遇到过这个问题。你向演示稿中添加内容，但它隐藏在某处，直到你打开编辑器。在一个有很多问题的领域，很少有创新这很奇怪。我们需要一种新方法来创建和展示你的演示文稿 - Hovercraft。它用 Python 编写，基于 `impress.js` 和 `reStructuredText`。它让你用记事本创建演示文稿并在浏览器中展示它们。

## 资源

- Python 3.2 或以下版本
- `www.python.org/downloads/`
- `libxml2` 和 `xs`
- `www.libxml.org/downloads.html`
- Hovercraft 文档
- `https://github.com/regbro/hovercraft`

## 使用 Hovercraft 设计演示文稿

使用 `impress.js` 和 `reStructuredText` 在记事本中编写演示文稿

## 教程

![](img/df15b709d7e8fa8f2cd7af7eb08775e_44.png)

**01 `impress.js`**

如前所述，Hovercraft 基于 `impress.js` 和 `reStructuredText`。首先了解更多 `impress.js`。`impress.js` 是一个开源库，帮助你制作精美的演示文稿。它使用了 `CSS3` 变换。`impress.js` 能够实现的一些惊人效果：完成后，`impress.js` 的结果基本上是 HTML。你可以在这里查看：`github.io/impress.js`

你可能会想，如果 `impress.js` 能够完成一切，还需要 Hovercraft？因为 `impress.js` 需要使用 HTML 和 CSS 来创建演示文稿。Hovercraft 将 `impress.js` 的功能与 `reStructuredText` 的帮助相结合，生成纯文本文件，然后被解释为 HTML。对于初学者，`reStructuredText` 是一种标记系统。简单来说，它允许根据定义的语法在任何文本编辑器中编写。没有步骤！它被广泛用于文档生成器。它的目标是简单且无干扰，以便理解。要理解 `reStructuredText` 如何工作，让我们看看标记规则。

**02 `reStructuredText`**

Hovercraft 的另一个重要组件是 `reStructuredText`。现在你已经了解了组件，让我们看看安装。Hovercraft 用 Python 编写，并使用 Python 3.2 或更高版本。你还需要 `pip` 包管理器来安装包。我们使用最新版本 Python 3.4 的 `libxml`。你需要单独安装 Hovercraft。如果你在 Windows 或 Linux 上，从这里下载：`bits.org`。

| 纯文本 | 典型结果 |
| :--- | :--- |
| *强调* | 强调 |
| **强调** | **强调** |
| *内联* | 内联 |
| 标题 | 副标题 |

## 教程

## 创建演示文稿

要创建演示文稿，使用 GEdit/Leafpad/Vim 或任何文本编辑器并开始你的内容。只需记住文本需要结构化。例如，定义幻灯片头部，你需要解析为标题的文本。现在，使用两个不同的行来定义副标题。创建项目符号或编号列表需要在右侧缩进并在文档中编写。关于如何样式你的演示稿有更多信息。

保存文件后，用 `.rst` 扩展名打开它。然后可以使用命令 `hover presentation <targetid>` 查看你创建的文件。Hovercraft 会在 `output` 文件夹中创建一个 HTML 文件。这就是所有的工作：现在你有了 Hover presentation。

## 05 样式演示文稿

Hovercraft 还演示了一些 `reStructuredText` 功能，在步骤 2 的参考指南中有详细说明。值得注意的是它们的工作方式简单：

- `reStructuredText` 中的过渡用于分隔幻灯片。过渡是带有一个或多个连线的线 `------`，所以需要在幻灯片的末尾添加过渡。
- Hovercraft 只有在找到过渡后才制作第一张幻灯片。之前的任何内容都属于演示文稿。

在第一个幻灯片之前添加到演示文稿的每个 `impress.js` 字段都是 ![](img/df15b709d7e8fa8f2cd7af7eb08775e_45.png)

```
.. Sample.rst
   :title: Sample Presentation
   :author: John Doe
   :description: 用于演示目的的文稿
   :keywords: presentation, reStructuredtext, impress.js, tutorial
   :css: sample.css
```

这张幻灯片是关于如何使用 Hovercraft 制作演示文稿的简单教程。它将通过示例向你展示 Hovercraft 最。的功能。带有标点的行都会变成标题。每种类型的标点都会转换为不同级别的标题。字符的顺序定义了标题的级别。下一张幻灯片将为你提供更好的画面。

第一个标题

如果你喜欢，可以使用其他标点作为标题级别，但这不是唯一的。任何这些字符之一：

```
*
** =
*** ~
```

## Howcraft 将 `reStructuredText` 转换为 XML 然后使用 CSS 将其转换为 HTML

渲染在 `impress.js` `'data'` 标签的属性中。它用于设置过渡时长：`transition-direction`。

- 同样，添加到第一张幻灯片的任何 `impress.js` 字段都在所有幻灯片上渲染。这包括幻灯片的效果，所以你可以在步骤中可选地添加。
- `template`
- `css: css/presentation`

第三种方法涉及通过参数添加 CSS：

## 06 样式 - 添加外部文件

向演示文稿添加外部样式表的方法与 Hovercraft 完全相同。向幻灯片添加图像使用：

```
.. image:: path/to/image.png
   height:648
   width:800
```

同样，你可以添加外部 CSS，有两种不同的方法。第一种方法是通过模板的——每当你使用模板时，相应的 CSS 会自动包含它们。例如，如果你使用默认的 `hovercraft-extra-my.css`

`sample.out/`

你也可以包含一个带有 `of: id` 的单个幻灯片。将字段添加到幻灯片内容中使其像这样：

```
- id: slide-id
```

然后你可以此处添加自定义代码（到演示文稿已包含的任何 CSS）：

```
div-theme-id
   // Custom CSS here //
```

## 在 Hovercraft 中设计演示文

使用 `impress.js` 和 `reStructuredText` 在记事本中编写演示文

![](img/df15b709d7e8fa8f2cd7af7eb08775e7_46_0.png)

```
nitish@nitish-Ubuntu:~$ hovercraft -a sample.rst output/
nitish@nitish-Ubuntu:~$
```

## 08 演讲者控制台

模板是你重新定义演示文视觉效果和感受的方式。默认情况下，Hovercraft 有两个模板——第一个是用于创建演示文的默认模板，第二个是不带演讲者的模板。如果你对这些不满意，可以自己创建一个。请注意，Hovercraft 是通过将内容转换为 XML 并使用 XSLT 将 XML 转换为 HTML 来生成演示文的。因此，一个新模板需要一个模板 XML 文件、一个配置文件以及用于其他资源的 CSS。

配置文件定义了模板的内容。它只有一个 `[hovercraft]` 部分，包含一个你应该命名为 "template" 的子部分。你可以使用任何以 `.cfg` 作为扩展名的文件名。记住在使用 Hovercraft 命令时指定文件名，或使用默认名称。

通过配置文件的模板参数指定文件后，实际的 XSLT 模板执行 XML 到 HTML 的转换。你可以从 Hovercraft 文件夹中的 `templates` 文件夹获取模板 XML 并对其编辑。

## 07 特殊效果

Hovercraft 让你能够创建一些酷炫的效果，如旋转、缩放甚至 3D，这可以通过 `impress.js` 实现。你还可以在幻灯片之前添加字段，然后幻灯片会自动移动。现在让我们来看看各种效果及对应的设置：

- 使用 `impress.js` 的 `data-field` 可以实现平移，它用于指示垂直滑动。
- 你可以使用 `data-attribute` 来设置旋转角度。
- 缩放效果可以使用 `data-field` 实现。如果你将其设置为 1，则大于 1 的值表示缩小滚动，小于 1 的值表示放大滚动。
