
# 插图标题和引用

在许多文档类（如 `article`）中，LaTeX 会从文档开始对插图进行编号。在其他文档类（如 `book`）中，LaTeX 根据它们所在的节或章节对插图编号。例如，在书中，第 1 节的第一个插图编号为 1.1，第 1 节的第二个插图为 1.2，第 2 节的第一个插图为 2.1，依此类推。

## 文本格式-创建和查看排版文档 253

要在排版文档中配合插图显示文本描述或标题，你必须首先将图像封装在 `\begin{figure}` 和 `\end{figure}` 命令中。然后你可以为插图配上 `\caption` 命令，其中包含括在花括号 `{}` 内的标题文本。8.29 展示了插图的标题规范。LaTeX 会自动为标题加上相应的插图编号。`caption` 和 `label` 命令之间的缩进是为了提高插图内的可读性。此步骤也涉及将图像封装在 `\begin{figure}` 和 `\end{figure}` 命令中。如果图像规范已经在这些命令封装，例如用于标题，你可以使用同一个封装。在这些命令之间，指定 `\label` 命令，后跟图像的引用 `{}` 内部。

### 列表 8.29 用于引用的插图标题和标签

```
\begin{figure}

\includegraphics[width=3in]{network_present.eps}

\caption{当前网络}

\label{present_network}

\end{figure}
```

一旦插图标记了标签，你就可以在文档的任何地方通过在该点指定括在花括号 `{}` 内的图像标识符来引用该插图。LaTeX 会在该引用点处排版插图的编号。列表 8.30 的第一行说明了如何在句子中引用网络图。这句话可以作为引言第二段的开头。注意文本和引用规范之间使用 `-`，以确保引用紧接在后续文本之后。

### 列表 8.30 引用插图和章节标签

```
Figure-\ref{present-network} 展示了 XYZ 目前的网络基础设施。
```

你还可以将这种标记和引用的技术用于文档的其他组件，如章节、节、子节或表格（我们很快就会学习）。例如，为了在引言第二段的延续中引用方法论、结果和分析章节的章节编号，首先如列表 8.31 所示为这些章节添加标签（为了简洁，你

## UNIX/Linux 简介

（只会看到受影响的行并用省略号表示中间行）。你也可以以类似的方式为其他文档组件指定引用标签。

### 列表 8.31 为章节指定引用标签

```
\section{Methodology}\label{methodology}

...

\section{Results}\label{results}

...

\section{Analysis}\label{analysis}
```

一旦指定了标签，你就可以按照列表 8.32 所示的方式引用该标签。为了简单，它使用章节名称本身命名标签，但如果你愿意，也可以给标签起其他名称。

### 列表 8.32 引用图片和插图（在列表 8.30 添加）

图--\ref{present-network} 展示了 XYZ 当前的网络基础设施。我们在章节--\ref{methodology} 中解释我们的研究方法，在章节--\ref{results} 中展示我们的发现，并在章节--\ref{analysis} 中给出我们的建议。

在运行 `late` 时，引用标签时可能会收到警告信息，如图 8.7 所示。此消息表示所引用的名称未与标签关联。如果你尝试引用章节（如列表 8.32 所示），但没有像列表 8.31 所示那样标记章节，就会看到类似于图 8.7 的消息。在这种情况下，LaTeX 仍然会创建排版文档，你会在排版文档中引用未定义标签的地方看到一个 `?`。要修复这些情况，首先要确认引用的标签已定义且拼写正确。然后再次运行 LaTeX（即在运行 `dvips` 或 `pdpdf` 之前）以尝试修复缺失的引用。在进行“正向”引用标签时，再次运行 LaTeX 特别有用，即引用在文档中引用点之后才定义的标签。

`LaTeX Warning: Reference 'methodology' on page 1 undefined on input line 35.`
`LaTeX Warning: Reference 'results' on page 1 undefined on input line 35.`
`LaTeX Warning: Reference 'analysis' on page 1 undefined on input line 36.`

图 8.7 未定义引用的 LaTeX 消息。

## 文本格式化——创建和查看排版文档 255

![](img/e3ac56d195b48617d5ae42cd57458af3_266_0.png)

当你正向引用标签时，可能需要运行 `latex` 来解析该标签。

### 图片位置

当仅使用 `\includegraphics` 导入图片时（如列表 8.26 所示），LaTeX 将在源文件中指定的点处排版图片。另一方面，当导入的图片被包含在 `\begin{figure}` 和 `\end{figure}` 之间时，LaTeX 将在文档中靠近导入点的“最佳”位置排版图片。排版文档中的实际位置可能与源文件中的指定位置匹配或不匹配。这种行为看起来很奇怪，但它通常很有帮助，因为 LaTeX 免去了作者指定物理布局的麻烦，从而了排版文档中拥挤的文本或区块。

尽管 LaTeX 最终决定了在 `\begin{figure}` 和 `\end{figure}` 中导入的图片的排版位置，但你可以对其放置提出建议。这些建议可以是该图片的 `\begin{figure}` 命令后紧跟的 `[]` 括号内的位置选项。放置选项包括：当前页顶部 `t`、当前页底部 `b`、新页 `p` 或此处 `h`。你还可以指定多个放置选项，LaTeX 将尝试按照指定的顺序满足请求。例如，给定列表 8.33 所示的放置选项，LaTeX 首先尝试将图片放在文档中指定的点处，然后放在页面顶部，最后放在页面底部。请记住，放置选项只是 LaTeX 尝试满足的建议。如果认为其他地方是图片的更好位置，LaTeX 仍然可能将图片放在别处。

#### 列表 8.33 建议图片位置

```
\begin{figure}[htb]

\includegraphics[width=3in]{network_present.eps}

\caption{Present network}

\label{present_network}

\end{figure}
```

### 子图

你也可以拥有子图，或者在单个图片规格内包含多个图片。要使用子图，文档必须在文档开头附近的文档类指定之后，使用命令包含 `subfigure` 包，如列表 8.34 所示。

#### 列表 8.34 包含对子图的支持

```
\usepackage{subfigure}
```

一旦包含了 `subfigure` 包，就可以在感兴趣的图片规格中使用 `\subfigure` 命令。在 `\subfigure` 之后，你可以将一个包含在 `[]` 括号内的用于子图的可选标题。在可选标题之后，有一组 `{}` 大括号括了用于子图的 `\includegraphics` 命令，其工作原理如前所述。如果你想对子图使用文本引用，也可以在这些大括号内指定一个可选的 `\label` 命令。注意，子图没有 `\caption` 命令，因为标题现在被指定为 `\subfigure` 命令的一个选项。

列表 8.35 展示了如何将文件 `internal-rtt.eps` 和 `external-rtt.eps` 中的图片作为两个子图导入，每个图都有标题和标签。请记住，如果你想让子图并排，你可能需要调整它们的大小。

#### 列表 8.35 导入子图

```
\begin{figure}[htb]

\subfigure[Internal rtt]{

  \includegraphics[width=2in]{internal-rtt.eps}

  \label{internal-rtt}

}

\subfigure[External rtt]{

  \includegraphics[width=2in]{external-rtt.eps}

  \label{external-rtt}

}
\end{figure}
```
