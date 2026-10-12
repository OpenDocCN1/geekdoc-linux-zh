
遗憾的是，`MathLex` 并没有以 `.deb` 或 `.rpm` 等发行版格式打包。在 Linux 机器上安装它最简单的方法是通过 `Yarn` 包管理器进行本地构建 [2]。要在你的计算机上获取 `MathLex` 的副本，请通过 `git` 或单个 `ZIP` 压缩包下载源代码。代码进入文件夹后，从命令行进入该目录并输入以下命令：

```
yarn
yarn build
```

如果运气好，安装应该在一两分钟内完成。然而，在 `Ubuntu` 上，我遇到了“No scenarios; must have at least one.”的 `Yarn` 错误。结果 `Ubuntu`（可能的其他 Linux 发行版）没有安装开发者推荐的默认 `Yarn` 版本。相反，它安装了位于 `cmdtest` 包中的另一个版本。你可以移除该包，然后按照 `Stack Overflow` 的说明安装原始版本 [3]。

## 使用 `MathLex`

使用 `MathLex` 写公式最困难的部分是了解你需要的所有数学以及 `MathLex` 的所有功能。关于学习 `MathLex` 语法，`Yarn` 会在 `build` 目录下放置一个名为 `index.html` 的文件（`index.html` 是图 1 和图 2 所示的 `HTML` 页面）。

除了图 2 顶部 `Syntax` 和 `Topic` 链接外，`HTML` 页面底部包含许多示例公式，你可以将其加载到输入框并修改（图 4），转换为 `SVG` 等格式（图 5），甚至使用它们来学习 `MathLex` 的原生格式（图 6）。得益于这些提示和示例，加上图 2 中的渲染框和解析框会随着你的输入而变化，在演示中尝试编写公式显然是最快捷、最有效的方法。

图 3：`MathLex` 还支持 `MathML` 标记语言和 `MathJax` 库。

图 4：根据你的需求，你可以将公式渲染为多种格式。

图 5：图中所示公式的 `SVG` 版本。

图 6：出于学习或文档目的，你还可以查看 `MathLex` 使用的纯源码。

47 深度 `MathLex` `LINUX-MAGAZINE.COM` 第 274 期 2023 年 9 月

![](img/8db7a58bef2f490a3db3c4fd35de2457_47_0.png)

学习 `MathLex` 语法的有效方法。

我在演示中发现的一个令人困惑点是，某些标记（`MathLex` 术语中的分隔符）可以带冒号也可以不带冒号。例如，在手写数学中，某些变量的绝对（即没有正负号）是通过将该变量放在两个竖线之间来表示的。不出所料，`MathLex` 允许你通过将变量封装管道字符内来指定其绝对值（例如 `|X|`）。但对于 `MathLex` 来说，即使是 `|:X:|` 也是完全有效的语法。你唯一不能做的是混合这些形式（即你不能写 `|:X|`）。记住这一点，一切都会正常。

## 在网页上使用 `MathLex`

列表 1 列出了图 7、8 和 9 所示的自定义 `MathLex` 页面的源代码，它概述了在任何网页上轻松使用 `MathLex` 所需的内容。为了获得图 7 所示的可运行 `MathLex` 界面，我将演示文件 `index.html` 的相关部分复制到一个空文件中，将其以 `.html` 扩展名保存，并重写了头部和其他一些字符串。

请注意列表 1 中，为了可读性，我缩短了第 6、8 和 35 行加载的字体和 `JavaScript` 库的长 `URL`。实际 `URL` 可能会根据你使用的 `MathLex` 版本而异。

关于库，列表 1 有两点需要注意。首先，你必须包含演示 `index.html` 文件的完整头部（第 1 到 11 行），但不要像我为了可读性那样缩短 `URL`。

其次，将演示文件夹中所有包含 `MathLex` 样式表的文件以及其实际源代码连同你的 `HTML` 页面一起复制。我在本文中使用了 2021 年 4 月版本的 `MathLex`，因此在列表 1 中，这些文件是第第 7 和 9 行调用的样式表，以及 `JavaScript` 文件 `mathlex.js` 和 `index.js`（第 34 和 36 行）。如果你使用的是较新版本，请检查 `index.html` 文件的头部和底部是否有你应该包含的其他文件。

列表 1 的其余部分通过与图 7 到 9 的比较很容易理解。第 12 行生成标题“让 `Linux Magazine` 试试 `MathLex` 吧!",第 16 到 18 行生成文本输入区域，最初填充了第 17 行所示的占位符，你可以在那里编写公式（图 8）。相同的公式在第 20 行的 `div` 元素中渲染，其初始值也可以通过更改括号内的文本进行自定义。

最后，从第 22、26 和 30 行开始的三对 `div` 元素是 `HTML` 标记，它们（连同头部）渲染了 `MathLex` 显示 `LaTeX` 代码、`Sage` 代码以及其自身的语法树的三个框（图 9）。页面的最后部分（第 34 到 36 行）加载了 `MathLex` 源代码以及 `jQuery` 库 [4]，这使得整个页面具有交互性。

**图 7：** 要创建自己的支持 `MathLex` 的网页，只需从 `MathLex` 演示中获取正确的代码并进行自定义即可。

**图 8：** 列表 1 生成的自定义页面工作原理与原始演示相同。注意交互式渲染器如何在公式完成且无错误之前以红色显示它们。

```html
01 <!doctype html><html lang="en">
02 <head>
03 <meta charset="utf-8">
04 <title>MathLex Demo</title>
05 <link rel="stylesheet" href="css/normalize.min.css">
06 <link rel="stylesheet" href="//fonts.googleapis.com...">
07 <link rel="stylesheet" href="css/style.min.css">
08 <script src="https://cdnjs.cloudflare.com..."></script>
09 <link href="main.css" rel="stylesheet">
10 </head>
11 <body>
12 <h1>Let's try MathLex for Linux Magazine!</h1>
13 
14 <div role="main">
15 
16 <div class="inbox"><a class="delete-icon" href="#" title="clear">clear</a>
17 <textarea class="expand" id="math\_input" name="math" placeholder="Linux Magazine test: just enter any formula here..."></textarea>
18 </div>
19 
20 <div id="math\_output">\[\mathrm{\\LaTeX\ Output\for\ LM\ readers}\]</div>
21 
22 <div class="outbox"><label for="tex\_output">Translated LaTeX Code</label>
23 
24 <div id="tex\_output"><code>Output LaTeX Code</code></div></div>
25 
26 <div class="outbox"><label for="sage\_output">Translated Sage Code <span class="highlight">Incomplete</span></span>></label>
27 
28 <div id="sage\_output"><code>Output Sage Code</code></div></div></div
29 
30 <div class="outbox"><label for="ast\_output">Interpreted Syntax Tree</label>
31 
32 <div id="ast\_output"><code>Output Syntax Tree</code></div></div>
33 
34 <script src="../mathlex.js"></script>
35 <script src="http://code.jquery.com/..."></script>
36 <script src="index.js"></script>
37 </body>
</</html>
```

**列表 1：自定义 `MathLex` 页面**

![](img/8db7a58bef2f490a3db3c4fd35de2457_48_0.png)

## 结论

在实验了几个小时的 `MathLex` 后，我认为 `Barry` 成功地让以数字形式输入复杂公式变得更容易。我向任何处理数学公式的人推荐此工具。

如果你正在提高自己的 `JavaScript` 技能，可以帮助更新 `MathLex`。现在的许多开发者更倾向于使用 `jQuery` 以外的库。`Barry` 提到“如果能让 `MathLex` 跟上现代开发（也许 `TypeScript`？）那就非常好” [5]。
