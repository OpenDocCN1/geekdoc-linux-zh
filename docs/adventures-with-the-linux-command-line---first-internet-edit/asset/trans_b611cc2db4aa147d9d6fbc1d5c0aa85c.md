

# 脚本的缩进设置

为了我们的目的，我们将使用方法 2 并在 `sh.vim` 文件中添加以下行，将制表符设置为 2 个空格。这是某些 shell 脚本编码标准中的常用设置。

```vim
setlocal tabstop=2
setlocal shiftwidth=2
setlocal expandtab
setlocal softtabstop=2
setlocal autindent
setlocal smartindent
```

除了制表符，我们还包含了 `autindent` 和 `smartindent` 设置，我们在编写代码块时需要。

在 `sh.vim` 文件中添加缩进设置后，我们将向 shell 脚本中添加更多行（输入这些内容以观察行为）：

```bash
# /bin/bash

# 这是一个演示 vim 特性的 shell 脚本。
# 它实际上并没有做什么，只是展示了我们能做什么。

# 常量
A=1
B=2

if [ "$A" == "$B" ]; then
  echo "This shows how smartindent works.\n  echo "This shows how autindent works.\n  echo "A and B match."
else
  echo "A and B do not match."
fi

afunction() {
  cmd1
  cmd2
}

if [ -e file ]]; then
  cmd1
  cmd2
fi
```

当我们在脚本中输入这些额外行时，我们注意到 vim 现在可以根据需要自动提供缩进。当 `smartindent` 选项为函数和 if 等某些程序结构提供缩进时，`autindent` 选项会导致 vim 重复上一行的缩进。这在编码时节省了大量时间，并确保我们的代码保持整洁。

如果我们发现其他人正在编辑一个现有脚本，且其缩进方案与我们当前的设置不同，vim 可以转换该文件。通过输入实现：

```vim
:retab
```

166 Vim，充满活力

该文件的制表符将被调整以匹配我们当前的缩进风格。

帮助主题：'tabstop' 'shiftwidth' 'expandtab' 'softtabstop' 'autoindent' 'smartindent'

# 强力移动

正如我们在 TLCL 中学到的，vim 有许多移动命令可以用来快速在文档中导航。这些命令可以用许多实用的方式使用。

以下是常用移动命令列表。其中一些是复习，另一些是新的。

- h 向左（也可以用左箭头）
- l 向右（也可以用右箭头）
- j 向下（也可以用下箭头）
- k 向上（也可以用上箭头）
- 0 行首第一个字符（也可以用 Home 键）
- 行内第一个非空白字符
- $ 行尾最后一个字符（也可以用 End 键）
- f(char) 向右移动到当前行中 char 的下一次出现处
- t(char) 向右移动直到（即：紧邻）行中 char 的下一次出现处
- r 重复上一个 f 或 t 命令
- g 跳到最后一行。如果指定了计数，则跳到该行
- w 向前（单词）到下一个单词的开头
- b 向后（单词）移动到上一个单词的开头
- e 向前到单词末尾
- ) 向前进到下一个句子的开头
- ( 向前进到下一个段落的开头
- { 向后移动到上一个段落的开头

记住，每个命令之前都可以跟一个计数，表示执行命令的次数。

# 操作符

移动命令通常与操作符结合使用。移动命令决定了操作符影响文本的范围。以下是最常用的操作符列表：

- c 修改（即删除后插入）
- d 删除/剪切
- y 圈取（即复制）
- t 切换大小写
- g 转小写
- g 转大写
- q 格式化文本（我们很快会涉及的话题）
- ? ROT13 编码（用于混淆文本）
- > 向右移动（即缩进）
- < 向左移动

我们可以使用视觉模式轻松地演示移动命令。将光标移动到脚本第 3 行的开头并输入：

Vim，充满活力 167

vf.

这将选择从行首到第一个句子末尾的文本。
再次按 v 取消视觉模式。接下来，回到第 3 行开头并输入：

v)

选择第一个句子。再次取消视觉模式并输入：

v)

选择整个段落（任何由空行分隔的文本块）。按 }\ag 将选定内容缩进到下一个段落。

# 文本对象选择

除了传统的 vi 移动命令外，vim 还增加了一个名为*文本对象选择*的相关功能。这些命令仅与操作符配合使用。命令如下：

- 选择整个（所有）文本对象。
- 选择文本对象的内部（in）。

文本对象有：

- 单词 (Word)
- 句子 (Sentence)
- 段落 (Paragraph)
- 标签块（例如 HTML 中使用的 `<a>...</a>`）
- { 包闭块
  { 包闭块（也可以使用 b）
  { 包闭块（也可以使用 B）
- "双引号字符串"
- '单引号字符串'

这种这种工作方式非常有趣。例如，如果我们把光标放在一个单词上并输入：

caw

（"change all word" 的缩写，修改整个单词，删除它并切换到插入模式）。文本对象也适用于视觉模式。尝试一下：移动到第 11 行，将光标放在引号字符串内部并输入：

vi"

引号字符串的内部将被选中。如果我们输入：

va"

则整个字符串（包括引号）被选中了。

帮助主题：motion.txt text-objects

# 文本格式化

假设我们想在脚本开头添加一个许可头。这将由文件顶部的一个注释块组成，包含版权声明的文本。

我们将移动到脚本的第 3 行并添加文本，但在开始之前，让我们告诉 vim 文本行的长度应该是多少。首先我们询问 vim 当前的设置：

```vim
:set tw=75
```

Vim 将响应：

```text
textwidth=0
```

"tw" 是 text 的缩写，行长度设置。值为 0 意味着 vim 没有对行长度实施限制。我们将 textwidth 设置另一个值：

```vim
:set tw=75
```

现在，当行长度超过该值时，vim 将自动换行（在单词边界）。

# 段落格式化

通常我们在编写代码时不想设置文本宽度（尽管将行长度保持在 80 个字符以内是一个良好的习惯），但那时将很有用。

所以让我们添加文本。输入以下内容：

```bash
# This program is free software: you can redistribute it/or modify it
# under the terms of the General Public License as published by the
# Free Software Foundation, either version 3 or (at your
# option) any later version.
```

```bash
# This program is distributed in the hope that it will be useful,
# WITHOUT ANY WARRANTY; without even the implied of
# MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE. See the Vim
# Public License at <http://www.vim.org/licenses/> for more details.
```

注意到 vim 的魔法。每当行长度达到文本宽度时，vim 会开始新行并包含注释符号。这是为 shell 脚本设置的，理解某些 shell 语法并尝试提供帮助。非常方便。

现在假设我们对这些行的长度不满意，或者编辑了文本导致某些行太长或太短，无法保持我们格式良好的文本。如果我们能重新格式化我们的注释块该有多好？嗯，我们可以。非常简单。

为了演示，我们将文本宽度更改为 65 个字符：

```vim
:set tw=65
```

现在将光标放在注释块内部并输入：

ggip

（意味着“格式段落”）稍后我们将展示如何将这四个键序列减少到单个键。

# 注释块

我们可以在这个注释块上执行一个技巧。当我们格式化段落时，观察发生了什么。预料成功，块被重新格式化为新的格式！稍后我们将展示如何将这四个键序列减少到单个键。 (注：此处原文中似乎有重复的句子，翻译时已根据语境调整)

*注：由于原文文本中存在重复，翻译时已进行了逻辑处理。*

