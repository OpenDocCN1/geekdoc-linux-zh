
非常有用的结果。然而，如果你需要的格式与 `Asci Doc` 的 `a2x` 命令不同，则所有的变体都需要进行训练。

`a2x` shell 脚本允许用户快速自动地将源代码转换为各种输出格式，特别是 `PDF`。

通常情况下，你会从发行版的仓库安装 `Asciidoctor`。但是，如果缺少某些组件（例如 `asciidoctor-epub3`），你可以在 `ad-system` 中制作的文档中使用 `Ruby` 自身的 `gem` 安装设置来导入缺失的组件；或者，直接从 `Ruby` 仓库调整 `gem` 的语言和格式，例如输出结果以及文档类型。这些指令被写在紧接文档头之后的的行注释中。

```
$ gem install asciidoctor-epub3
```

调用 `a2x <file>` 将使用所有可用选项翻译文档。该工具将 `gem` 安装在 `~/.gem/ruby/2.7.0/bin/` 中。你必须将此路径包含系统环境变量 `PATH` 中。

在某些情况下，例如 `asciidoc-epub3` 示例，目前还没有官方必要的包，你将收到错误消息。如果存在仍在开发中的包，你可以使用 `--pre` 选项进行测试：

```
$ gem install asciidoctor-epub3 --pre
```

在这种情况下，将执行安装，并同时添加 `Asci Doc` 和 `Asciidoctor` 扩展。

## 差异

`Asci Doc` 和 `Asciidoctor` 在某些细节上有所不同。

对于简单的文档，这顶多是一个次要问题。然而，如果你充分利用每种软件的功能，差异就会变得更加明显。你可以在寻找 `In search for the (Asciidoctor only)` 字符串的示例，它指定了这些功能适用于 `Asciidoctor`。在大多数情况下，`Asciidoctor` 的功能超过了 `Asci Doc` 支持的内容，但得益于内置的兼容模式，

### 表 1：Asciidoctor 命令行选项

| 选项 | 效果 |
| --- | --- |
| `-b <Format>` | 创建输出为 `HTML5`（默认）、`XHTML5`、`DocBook 5`、`manpage` 或通过适当的插件输出——如 `PDF`、`LaTeX` 或 `EPUB` |
| `-d <Type>` | 除了经典的 `article`（默认）、`book` 和 `manpage` 之外，`Asciidoctor` 更倾向于为包含的代码输出，例如单代码块、段落或类似内容 |
| `-o <File>` | 将输出保存为指定的名称 |
| `-D <Directory>` | 将结果保存到指定的目录中 |
| `-s` | 抑制头部和页脚（针对包含的文档） |
| `-n` | 章节的自动编号 |
| `-a <Attribute>` | 设置 `Asci Doc` 属性（覆盖文档中现属性） |
| `-B <Base>` | 定义附加代码的基目录；默认是当前目录 |
| `-V` | 警告级别，根据此生成错误代码：`WARN`, `ERROR`, `INFO`, |
| `--failure-level <Level>` | `FATAL`（默认） |
| `-S` | 设置安全级别；禁用潜在不安全的结构，如 `include::` |

## UI 宏

| 快捷键 | 目的 |
| --- | --- |
| `F11` | 切换全屏 |
| `Ctrl + T` | 打开新标签页 |
| `Ctrl + Shift + N` | 新无痕窗口 |
| `Ctrl + \` | 用于转义字符 |
| `Ctrl + ]` | 跳转到关键词 |
| `Ctrl + +` | 增大缩比例 |

`Asciidoctor` 可以处理任何用 `Asci Doc` 格式化过的内容。尽管如此，现在已支持用于快捷键的 `UI` 宏（图 1）。同样有趣的是，`Asciidoctor` 没有提供命令 `a2x` 的对应项，参见框，“`Asci Doc` 的 `a2x` 命令”。或者，你可以在 shell 提示符处指定选项。作为一个特殊功能，`a2x` 有 `--epubcheck` 选项来自动化调用 `a2x` 工具的过程，该工具可以识别 `EPUB` 文档中的潜在问题。以程序代码的形式。这允许句子交换、注释和其他操作，就像在任何编程语言中一样。

## PDF 选项

与 `AsciiDoc` 一，`Asciidoctor` 通常面向 `HTML`，这使其更容易转换为基于它的格式，包括 `AsciiDoc` 和 `EPUB`。`AsciiDoc` 的经典结构在多程度上通过命令行控制。与其非常相似的重要选项汇总在表 1 中。不带选项的命令和调用将具有 `.adoc` 扩展名的文件翻译为 `HTML5`：

```
$ asciidoctor tst.adoc
```

创建 `PDF` 有几种方法，它们可能会导致非常不同的结果。如果你倾向于创建书籍之类的线性文档，你可能更喜欢 `PDF`。

生成一些 `HTML` 输出，在浏览器中调用它并将其导出为 `PDF`。这种方法提供了相当广泛的后续编辑。默认情况下，工具在转换期间会抑制消息。它只向你显示严重错误，例如缺少嵌入图像。但不如此。或者，你可以通过 `a2x` 使用 `DocBook 5` 工具链。`Asciidoctor` 允许你直接用 `Asciidoctor` 创建 `PDF`，但结果往往不理想。从 `Asci Doc` 切换到 `Asciidoctor` 时需要考虑一些差异，这些差异总结在用户手册的第 9 章 [9]。

这并不总是按预期工作，但过程非常快。缺点是没有有意义的错误消息，错误往往长时间无法被发现。例如，在语法方面，现在斜体文本仅有 `_<Text>_` 语法，代码使用 `<Text>`，代码中的字面文本使用 `+{Text}+`。双引号在 `Asci Doc` 或 `Asciidoctor` 中使用 `"<Text>"` 创建，单引号使用 `'<Text>'`。

另一种选择是使用 `LaTeX`。你可以通过 `LaTeX` 自己的工具传统方式创建。对于标题，`= <Title>` 语法（异步）仍然有效，但不是对称的形式 `= <Title> =` 或使用下划线的形式。标题下划线会自动导致兼容模式。手册中的第 9.8 提供了额外的 `LaTeX` 知识以及通常的手动调整。无论你选择哪种路径，请记住交互元素在转换过程中几乎总是丢失。

## 结论

`Asciidoctor` 证明它是 `AsciiDoc` 的合格继任者。它的速度和附加插件以及对 `AsciiFX` [10] 的直接支持使其成为一个良好但更复杂的替代方案。那么现在没有理由使用 `Asci Doc` 了吗？这取决于。例如，对于电子书运行良好的工具链是不容忽视的，而且结果有时比 `Asciidoctor` 生成的结果更紧凑。

图 1：这些用于快捷键的 `UI` 宏在 `Asciidoctor` 中可用，但在 `AsciDoc` 中不可。

点击块 点击块显示标题但不显示正文。点击标题将显示正文。再次点击标题隐藏正文。

点击块的标题显示为蓝色。

### 示例

**问题**

光速是多少？

**答案**

```
Last updated 2020-07-31 10:44:39 +0200
```

由于经典的 `AsciiDoc` 围绕 `Asciidoctor` 构建，它看起来是一个更灵活的应用程序，这使得它对于以后使用 `Asciidoctor` 变得非常有价值。你可以更轻松地掌握切换到 `iDoc`。

`图 2：` `HTML` 输出格式中的交互式结构（如点击块）仅由 `Asciidoctor` 支持。此示例取自原始文档，点击“`Answer`”将显示源代码中给出的答案。

## Info

| `ID` | `Type` | `Link` |
| :--- | :--- | :--- |
| `1` | `AsciiDoc` | `https://asciidoc.org` |
| `2` | `Asciidoctor PDF` | `https://asciidoc.org` |
| `3` | `Asciidoctor projects` | `https://github.com/asciidoctor/projects/` |
| `4` | `Asciidoctor syntax` | `https://github.com/asciidoctor/syntax-quick-reference/` |
| `5` | `Asciidoctor manual` | `https://asciidoctor.org/user-manual/` |
| `6` | `Asciidoctor specifics` | `https://github.com/asciidoctor/asciidoctor-latex/` |
| `7` | `Asciidoctor` | `https://github.com/asciidoctor/asciidoctor-pdf/` |
| `8` | `Asciidoctor syntax` | `https://github.com/asciidoctor/asciidoctor-epub/` |
| `9` | `Asciidoctor manual` | `https://asciidoctor.org/docs/user-manual/` |
| `10` | `AsciidoctorFX` | `https://asciidoctorfx.com/` |

## 即将推出
