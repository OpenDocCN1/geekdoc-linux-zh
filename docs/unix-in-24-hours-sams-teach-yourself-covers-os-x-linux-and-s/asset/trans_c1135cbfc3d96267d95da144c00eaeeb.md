

command.

+   1. 退回 emacs 并定位光标。它应该在屏幕顶部：

Click here to view code image

```
A Tale of Two Cities

Preface

When I was acting, with my children and friends, in Mr Wilkie Collins’s
drama of The Frozen Deep, I first conceived the main idea of this
story. A strong desire was upon me then, to
embody it in my own person;
and I traced out in my fancy, the state of mind of which it would
necessitate the presentation
to an observant spectator, with particular
care and interest.

As the idea became familiar to me, it gradually shaped itself into
its present form. Throughout its execution, it has had complete
possession of me; I have so far verified what
is done and suffered in these pages,
as that I have certainly done and suffered it all myself.

Whenever any reference (however slight) is made here to the condition
of the French people before or during the Revolution, it is truly
made, on the faith of the most trustworthy
witnesses. It has been one of my hopes to add
--Emacs: dickens.note          (Fundamental)--Top-----
```

使用 C-n 四次向下移动四行。你的光标现在应该停在 drama 的 d 上：

Click here to view code image

```
Preface

When I was acting, with my children and friends, in Mr Wilkie Collins’s
drama of The Frozen Deep, I first conceived the main idea of this
story. A strong desire was upon me then, to
embody it in my own person;
and I traced out in my fancy, the state of mind of which it would
```

+   2. 接下来，使用 M-e 命令移动到该句子的末尾（emacs 要求用两个空格分隔句子）：

Click here to view code image

```
story. I fought the impulse to write this novel vociferously, but, dear reader,\
I felt
the injustice of the situation too strongly in my breast to deny_ A
strong
des\
ire was upon me then, to
embody it in my own person;
and I traced out in my fancy, the state of mind of which it would
necessitate the presentation
```

你可以看到当行变得太长时 emacs 会换行（在 felt 和 the 之间），并且由于行仍然太长无法显示，其中几行以反斜杠结尾。反斜杠并不是文件的一部分；借助它，emacs 在表示这些行比能显示的更长。

### 3. 现在尝试通过按 Backspace 向后移动几个字符。

糟糕！如果你的系统和我一样，Backspace 键根本不会将光标向后移动一个字符。相反，它会启动 emacs 帮助系统，你会突然面对一个看起来像这样的屏幕：

Click here to view code image

```
You have typed C-h, the help character. Type a Help option:
A command-apropos. Give a substring, and see a list of commands
(functions interactively callable) that contain
that substring. See also the apropos command.
B describe-bindings. Display table of all key bindings.
C describe-key-briefly. Type a command key sequence;
it prints the function name that sequence runs.
F describe-function. Type a function name and get documentation of it.
I info. The info documentation reader.
K describe-key. Type a command key sequence;
it displays the full documentation.
L view-lossage. Shows last 100 characters you typed.
M describe-mode. Print documentation of current major mode,
which describes the commands peculiar to it.
N view-emacs-news. Shows emacs news file.
S describe-syntax. Display contents of syntax table, plus explanations
T help-with-tutorial. Select the Emacs learn-by-doing tutorial.
V describe-variable. Type name of a variable;
it displays the variable’s documentation and value.
W where-is. Type command name; it prints which keystrokes
invoke that command.
--**-Emacs: *Help* (Fundamental)--Top-----
A B C F I K L M N S T V W C-h C-h C-h C-d C-n C-w or Space to scroll: _
```

要退出帮助屏幕（你将在本小时稍后了解更多关于它的内容），请按 Escape，你的屏幕应该会被恢复。状态行显示你正在查看的文件。但请注意：你并不总是查看想要处理的文件。

将光标向后移动几个字符的正确键是 C-b。用它向后退，然后用 C-f 再次向前移动到原始光标位置。

+   4. 使用 emacs 的 move-to-end-of-file 命令 M-> 检查文件的最后几行是否没有改变。（想想文件重定向来记住文件移动命令。）现在屏幕看起来像这样：

