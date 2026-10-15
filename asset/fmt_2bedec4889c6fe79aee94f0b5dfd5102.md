
有关 GNU 项目及其目标的信息，请输入 `C-h G`。

![](img/69b363a7d7f58dc8d0b8c78c0052826f_142_2.png)

# Linux 工具包
第一部分

## 图 8.3
Emacs 具有吸引人的界面。

菜单栏
工具栏
编辑窗口

![](img/69b363a7d7f58dc8d0b8c78c0052826f_143_0.png)

状态栏
缓冲区

如果你想查看一个教程，可以输入 `C-h t`。每当你检查文件时，你都可以输入一条消息说明了什么变化或你做了什么，或者简单地为其添加额外信息，你可以使用以下 `rcs` 命令：

- 意味着按下并释放 Ctrl 键
- `C-x` 意味着按下并释放 Ctrl 键
- `M-x` 意味着按下并释放 Alt 键，如果按键不方便
- `M-x` 意味着按下并释放 Alt 键
- `M-x` 意味着按下并释放 Alt 键

# 在 Emacs 中创建程序
第 8 章

> 提示
退出任何版本的 Emacs，输入 `C-x`。

## 移动

任何程序员编辑器的真理在 Emacs 上同样适用：在学习 Emacs 上投入的时间在开发过程中将获得数倍回报。本章提供了足够的信息让你能够开始使用 Emacs，并介绍了许多增强其作为 C 开发环境用途的功能。然而， Emacs 太大了，在一个章节内无法涵盖。完整的教程是《Sams Teach Yourself Emacs in 24 Hours》。更多详细信息，请参阅由自由软件基金发布的《GNU Emacs Manual》和《GNU Emacs Lisp Reference Manual》，以及 O'Reilly 出版的《Learning GNU Emacs and Writing GNU Emacs Extensions》。

虽然起初看起来很奇怪，但随着你习惯 Emacs，你会发现移动更快。以下列表描述了如何移动：

- `M-b` 将光标移动到单词开头
- `M-f` 将光标移动到单词末尾
- `M-a` 将光标移动到行首
- `M-e` 将光标移动到行尾
- `C-n` 将光标移动到下一行
- `C-p` 将光标移动到上一行
- `C-M` 将光标移动到屏幕底端
- `C-U` 将光标移动到屏幕顶端
- `C-v` 将光标向上翻页
- `C-M` 将光标向下翻页
- `C-<` 将光标移动到文件开头
- `C->` 将光标移动到文件末尾
- `M-a` 将光标移动到句子开头
- `M-e` 将光标移动到句子末尾
- `M-s` 将光标移动到段落开头
- `M-;` 将光标移动到段落末尾
- `C-` 将光标移动到缓冲区开头
- `C-$` 将光标移动到缓冲区末尾
- `C-b` 将光标移动到字符开头
- `C-f` 将光标移动到字符末尾
- `C-w` 将光标移动到单词开头
- `C-d` 将光标移动到单词末尾
- `C-k` 删除从光标到行尾的内容
- `C-l` 删除从光标到行尾

## 总结

在本章中，你学习了 RCS，即版本控制系统。`ci` 和 `co` 及其它们的各种选项和参数；RCS 的基础命令。RCS 关键字允许你识别代码和编译程序中的字符串，这些字符串稍后可以通过 `ident` 命令提取。你还学习了其他有用但较少使用的 RCS 命令，包括 `rcsdiff`、`rsclean`、`rcsmerge` 和 `log`。

# 在 Emacs 中创建程序
第 8 章

为了方便剪切（yanking）和撤销（undo），Emacs 会维护一个包含最后 30 次删除内容的剪切环（kill ring）。要查看其效果，首先删除一些文本，移动到其他地方，然后输入 `C-y` 剪切最近删除的内容。接着输入 `M-y`，它会将刚才剪切的文本替换为上一次删除的内容。要继续在剪切环中向后循环，继续输入 `M-y`。

## 搜索与替换

Emacs 默认的搜索程序是不区分大小写的增量搜索，通过 `C-s` 调用。当你输入 `C-s` 时，最小缓冲区（minibuffer）会提示你输入搜索字符串，如图 8.4 所示。

图 8.4
增量搜索的最小缓冲区提示。

```c

/* read-char Search Name - 这是一个注释 */

int char;

while((char = getchar()) != '\n') {

	str[count++] = char;

}

return count;

int count_spaces(const char *str) {

for (int i=0; str[i] != '\0'; i++) { /* 这是一个较长的注释 */

	count++;

}

return count;

}

/* line-increment char *str - is-line-for-
line.c

	search */
```
