

用丹麦语替换法语的查询：

可能并不完全明显，但 emacs 在光标之前找到了一个匹配项，并提示我下一步该怎么做。这里的选择在表 12.3 中进行了总结。

| Command | Meaning |
|---|---|
| y | Change this occurrence of the pattern. |
| n | Don’t change this occurrence but look for another. |
| q | Don’t change this occurrence. Leave query-replace completely (you can also use Escape to do this). |
| ! | Change this occurrence and all others in the file. |

## TABLE 12.3 Options During Query and Replace

我选择通过按下 ! 来对本文件中的此项以及所有其他可能的变化进行修改，屏幕随之变化，告诉我没有更多匹配项：

Click here to view code image

```
Whenever any reference (however slight) is made here to the condition of the Danish people before or during the Revolution, it is truly made, on the faith of the most trustworthy witnesses. It has been one of my hopes to add --**Emacs: dickens.note        (Fundamental)--Top----- Done
```

在 emacs 中搜索很笨拙，特别是由于终端可能带来的流程控制问题。然而，使用 query-replace 命令进行搜索和替换非常出色；它比 vi 的替代方案更好、更强大。正如我之前所说，你对 emacs 的评价完全取决于你偏好的功能。

## Task 12.5: Using the emacs Tutorial and Help System

与 vi 不同，事实上与大多数 Unix 不同，emacs 包含自己的 extensive 内置文档和一个教程来帮助你学习如何使用该程序。正如我之前所说，你可以通过按下 C-h 来访问帮助系统。连续按下两次 C-h 会调出通用帮助菜单屏幕。还有一个名为 info 的信息浏览器，可通过 C-h i 访问，并且你可以通过按下 C-h t 启动教程系统。

emacs 爱好者坚持认为编辑器是无模式的，但事实上它确实有模式。你刚才就使用了一个——query-replace 模式。要获取你当前正在使用的模式的帮助，可以使用 C-h m。

+   1. 大胆地，我按下 C-h，整个屏幕被以下内容替换：

Click here to view code image

```
You have typed C-h, the help character. Type a Help option:
A  command-apropos. Give a substring, and see a list of commands (functions interactively callable) that contain that substring. See also the apropos command.
```

```
B  describe-bindings. Display table of all key bindings.
C  describe-key-briefly. Type a command key sequence;
    it prints the function name that sequence runs.
F  describe-function. Type a function name and get documentation of it.
I  info. The info documentation reader.
K  describe-key. Type a command key sequence;
    it displays the full documentation.
L  view-lossage. Shows last 100 characters you typed.
M  describe-mode. Print documentation of current major mode,
    which describes the commands peculiar to it.
N  view-emacs-news. Shows emacs news file.
S  describe-syntax. Display contents of syntax table, plus explanations
T  help-with-tutorial. Select the Emacs learn-by-doing tutorial.
V  describe-variable. Type name of a variable;
    it displays the variable's documentation and value.
W  where-is. Type command name; it prints which keystrokes
    invoke that command.
---*Emacs: *Help*          (Fundamental)--Top----
A B C F I K L M N S T V W C-x  b C-d C-n C-w or Space to scroll: _
```

现在该怎么办？从这一点开始，有十七种可能的选择，如表 12.4 所示。

| Command | Meaning |
|---|---|
| A | List all commands matching the specified word. |
| B | List all key mappings. |
| C | Describe any key sequence pressed instead of doing it. |
| F | Describe the specified function. |
| I | Start the info browser. |
| K | Fully describe the result of a particular key sequence. |
| L | Show the last 100 characters you typed. |
| M | Describe the current mode you're in. |
| N | Show the emacs news file. |
| S | List a command syntax table. |
| T | Start the emacs tutorial. |
| V | Define and describe the specified variable. |
| W | Indicate what keystroke invokes a particular function. |
| C-x b | Display emacs copyright and distribution information. |
| C-d | Display emacs ordering information. |
| C-n | Display recent emacs changes. |
| C-w | Display the emacs warranty. |

## TABLE 12.4 emacs Help System Command Options

2. 我选择 K 然后按下 M-< 来查看该命令到底做什么。输入 K 后发生的第一个事情是帮助信息表消失，被我的原始文本取代，然后提示出现在底部：

