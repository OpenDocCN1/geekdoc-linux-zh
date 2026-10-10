

![](img/c8827ea52a0796def3f6891892ed9d3a_305_0.png)

图 15.2 部分折叠的缓冲区

# 键盘和菜单命令

折叠模式命令的默认前缀是 Ctrl-c @，这是我不愿意使用的前缀。在寻找多余的 Emacs 键绑定以将其征用为折叠模式的前缀时，我偶然发现了 Ctrl-v。默认绑定运行向上滚动命令，而该命令恰好也是 Page Up 键调用的命令。由于我从不使用 Ctrl-v，尽量偏好单键输入，Ctrl-v 似乎是一个很好的候选项。如果你愿意这样做，你需要先在 `~/.emacs` 文件中用这一行取消当前的绑定：

```elisp
(define-key global-map [(control v)] nil)
```

这一行需要在 `~/.emacs` 文件中位于你的折叠模式初始化行之前。现在你可以自由地为 Ctrl-v 前缀分配新含义。这可以通过 Customize 完成。按下 M-x 并输入

`customize-group`

在提示时，输入

`folding`

在生成的 Customize 缓冲区中可以更改几个折叠设置。默认前缀键是第一个设置。

但既然你已经在捣鼓你的 `~/emacs` 文件了，与其使用 Customize，你可以直接在刚才显示的 `define-key` 行之后添加另一行，这将永久更改前缀：

```elisp
(defconst folding-mode-prefix-key (control v))
```

即使是菜单也会捕捉到这一变化，因为它们在每次启动折叠模式时都会从头生成。

图 15.3 是在进行此更改后 Fld 菜单的屏幕截图，展示了可用的众多折叠相关命令。

如果你保留了默认的折叠模式前缀，每个命令将以 Ctrl-c @ 作为前缀，而不是 Ctrl-v。

在启动折叠模式后，花些时间研究 `folding.el`，你将会熟悉在折叠文件中导航的感觉。创建你自己的文件并不困难，只要你记得保持打开和关闭折叠标记平衡即可。

折叠模式内置支持大多数编程语言使用的特定注释字符。请注意，图 15.2 中的折叠指示符以分号（Emacs Lisp 注释字符）为前缀，但该模式仍然识别折叠。以双斜杠（表示 C++ 注释）为前缀的大括号将在 C++ 源文件中被识别为折叠。可以使用如下语句将新的注释字符添加到列表中：

```elisp
(folding-add-to-marks-list 'major-mode *e({[`"*e{]}]`*) )
```

| 命令                       | 快捷键      |
|----------------------------|-------------|
| 进入折叠                   | (C-v x)     |
| 退出折叠                   | (C-v X)     |
| 显示折叠                   | (C-v S)     |
| 隐藏折叠                   | (C-v H)     |
| 显示整个缓冲区             | (C-v G)     |
| 折叠整个缓冲区             | (C-v G)     |
| 显示子树                   | (C-v +)     |
| 隐藏子树                   | (C-v -)     |
| 显示折叠名称               | (C-v =)     |
| 移动到上一个               | (C-v \|)    |
| 移动到下一个               | (C-v SP)    |
| 选择折叠                   | (C-v P)     |
| 折叠/展开区域              | (C-w B)     |
| 打开或关闭区域内的折叠     | (C-v F)     |
| 打开顶层折叠               | (C-v L)     |
| 注释折叠内的文本           | (C-v >)     |
| 转换为打印/临时缓冲区      | (C-v D)     |
| 转换为主要模式折叠         | (C-v 2)     |
| 移动区域内的折叠内注释     | (C-w /)     |
| 插入折叠 URL 引用          | (C-v )      |
| 切换进入和退出模式         | (C-v )      |
| 切换显示和隐藏             | (C-v )      |
| 关闭折叠模式               | (C-v )      |

![](img/c8827ea52a0796def3f6891892ed9d3a_306_0.png)

这一行适用于一个假设的主要模式，该模式使用 @ 字符作为注释指示符。

如果你想查看某种特定语言是否受支持，请按“help-on-variables”帮助键，即 Ctrl-h v。

响应提示时输入

```elisp
folding-mode-marks-alist
```

将打开一个窗口，显示折叠模式识别的众多注释字符。

# 在线字典的接口

Dict 项目（http://www.dict.org）为计算机用户提供了一个免费的客户端/服务器字典系统。它通过运行作为后台进程的服务器守护程序来处理来自诸如 dict 等客户端软件的请求，dict 是发行版的一部分。

Dict 是一个命令行程序。你输入 `dict word`，单词被传递给 dictd 服务器，该服务器在一个或多个使用名为 dictzip 的专用压缩程序压缩的字典文件中查找该单词。定义随后被传递给诸如 less 等分页器，在那里可以阅读定义。整个过程几乎是瞬间完成的。

Dict 从中提取定义的压缩字典文件都是公共领域文件，包括大约 1913 年版的未删节版梅里安-韦伯斯特字典和完整的 WordNet 数据库。其他还包括地名集、圣经字典和两部计算机术语汇编。

这些字典文件可以是 Internet 上远程 Dict 服务器上的，也可以是你自己机器上的本地文件。Linux 发行版提供了客户端、服务器和字典文件的软件包。

Dict 系统本身就值得一用，但不久之后，一些 Emacs 用户开始编写允许在 Emacs 内部访问这些字典的模式。其中一位用户是 Torsten Hilbrich；他编写了一个功能丰富的模式，称为 `dictionary.el`。该模式并没有作为 Emacs 对 dict 客户端程序的前端，而是取代了它，直接联系 dict 服务器。

# 安装 Dictionary.el

安装包括解包 `dictionary-1.2.1.tar.gz` 文件，将 “.el” 文件复制到你的 site-lisp 目录，并对文件进行字节编译。将这些行粘贴到你的 `~/.emacs` 文件中将激活该模式：

```elisp
(auto-load 'dictionary-search "dictionary"
  "Ask for a word and search it in all dictionaries" t)
(auto-load 'dictionary-lookup-definition "dictionary"
  "Search the word at point in all dictionaries" t)
(auto-load 'dictionary-match-words "dictionary"
  "Ask for a word and search all matching words in the dictionaries" t)
(auto-load 'dictionary "dictionary"
  "Create a new dictionary buffer" t)

(global-set-key [(control c) (d)] 'dictionary-lookup-definition)
(global-set-key [(control c) (s)] 'dictionary-search)
(global-set-key [(control c) (m)] 'dictionary-match-words)

(setq dictionary-server "localhost")
```

最后一行使你的机器成为默认的字典服务器。如果你想使用远程服务器，请用服务器的 IP 地址替换 "localhost"。可以根据你的设置更改键绑定。

字典模式提供几个功能命令。`dictionary-lookup-definition` 查找光标位置的单词，然后打开字典缓冲区并显示找到的定义。一种变体称为 `dictionary-search`，在 minibuffer 中显示当前点的单词，允许你在按 Enter 之前进行编辑。`dictionary-match-words` 提示你输入部分单词，然后显示包含该模式的单词列表，按字典排序。列表中的每个单词都是可点击的链接，用于获取定义。

图 15.4 显示了一个典型的字典窗口。

在字典窗口的顶部有几个通过鼠标激活的按钮，用于运行各种字典模式命令；结果将在窗口中显示。

如果你按下 M-x 并输入

`dictionary`

将显示一个空的字典窗口。

![](img/c8827ea52a0796def3f6891892ed9d3a_309_0.png)

你可以使用空的字典窗口访问命令按钮。

字典窗口中的一个按钮可用于选择默认字典，可以随时更改。图 15.5 显示了由此按钮调起的选项菜单。

字典模式是写作者的一大助力。你不仅可以有使用 `ispell` 检查单词拼写，使用此模式你还可以快速查阅定义。

![](img/c8827ea52a0796def3f6891892ed9d3a_309_1.png)

