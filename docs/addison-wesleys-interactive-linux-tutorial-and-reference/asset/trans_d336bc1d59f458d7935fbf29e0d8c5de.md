
图 11-5 命令 <2W> 之后的光标位置

-   d. 按下 <25> 将光标向右移动二十五个字符。图 11-6 显示了移动后的光标位置。

![](img/cc8b9fd5970716027fba0d0a45c13900_197_1.png)

图 11-6 命令 <25> 之后的光标位置

-   e. 按下 <4b> 将光标向左移动四个小词。图 11-7 显示了移动后的光标位置。

![](img/cc8b9fd5970716027fba0d0a45c13900_197_2.png)

图 11-7 命令 <4b> 之后的光标位置

-   f. 按下 <4w> 将光标移动到图 11-6 所示的位置。

-   g. 按下 <4B> 将光标向左移动四个大词。图 11-8 显示了移动后的光标位置。

![](img/cc8b9fd5970716027fba0d0a45c13900_197_3.png)

图 11-8 命令 <4B> 之后的光标位置

-   h. 按下 <3e> 将光标向前移动到第三个词的末尾。图 11-9 显示了移动后的光标位置。

    移动（the）光标：逐个词而非 word_by_word。

![](img/cc8b9fd5970716027fba0d0a45c13900_198_0.png)

-   i. 按下 <4b> 将光标向左移动回到图 11-8 所示的位置。

    > （问题：如果 <3e> 将光标从括号移动到“r”，为什么不是命令 <3b> 能够逆转该过程并将光标移回括号？为什么我们需要使用 <4b> 而不是 <3b>？答案在本练习的最后。）

-   j. 按下 <3E> 将光标向前移动到第三个大词的末尾。图 11-10 显示了移动后的光标位置。

    移动（the）光标；逐个词而非 word_by_word。

![](img/cc8b9fd5970716027fba0d0a45c13900_198_1.png)

在练习 23 的步骤 h 和 i 中，为什么 **<3b>** 没有逆转 **<3e>** 的效果？“后退一个词”的 **<b, B>** 和“词尾”的 **<e, E>** 命令将其视为包含在移动中的第一个词。练习 23 中的步骤 h 将光标定位在“cursor”的“i”上。命令 **<b>** 将光标向左移动到当前所在词的开头。因此，第一个 **<b>** 将光标定位在字母“c”上；第二个 **<b>** 将光标定位在“)”上；第三个 **<b>** 将光标定位在“the”的“t”上；第四个 **<b>** 将光标向左移动回到步骤 h 之前的起始位置：即“c”。

在接下来的一系列练习中，您将练习那些关注屏幕而不是字符和单词的命令。

-   24. 关闭 vi。
-   25. 重新打开 **vi** 并打开文件 **supply**。图 11-11 显示了文件的顶部。请注意状态栏中的信息。

```text
writing -- markers.
writing -- pencils.
writing -- pens.

correction fluid
correction pens
correction tape

staplers -- desktop
staplers -- electric
staplers -- specialty
"supply" 33 lines, 395 characters
```

# 图 11-11 带有状态栏信息的 *supply* 文件

-   26. 清除状态栏。
    -   a. 按下 <Ctrl-l> 以清除状态栏。
-   27. 向下滚动半屏。
    -   a. 按下 <Ctrl-d> 向下滚动半屏。您的屏幕看起来可能如图 11-12 所示。

![](img/cc8b9fd5970716027fba0d0a45c13900_200_0.png)

图 11-12 <Ctrl-d> 后的屏幕显示

您的屏幕显示可能与图 11-12 中看到的有所不同。对此最简单的解释是存在许多可能的终端配置。如果您的 **vi** 终端显示为二十五行，那么半屏是十二或十三行。如果您的 **vi** 终端显示为五十行，那么半屏是二十五行。**<Ctrl-d>** 向下滚动半屏。这意味着您可以预期屏幕显示会发生变化，正如练习 27 中您看到的那样。但是，如果您正在编辑的文件小到足以在一屏内显示，**<Ctrl-d>** 不会改变屏幕显示，而是将光标移动到屏幕的大致中间位置。

-   28. 向上滚动半屏。
    -   a. 按下 **<Ctrl-u>**。您的屏幕将与图 11-11 相似，但没有状态栏显示。

-   29. 向前滚动一整屏。
    -   a. 按下 **<Ctrl-f>**。您的屏幕可能看起来如图 11-13 所示。（请记住我们在前面提示中关于您的屏幕与图 11-13 之间可能存在差异的解释。）

```text
folders - hanging file
folders - specialty file

Post-It notes -- pads
Post-It notes -- pop up
Post-It notes -- printed

Reorder 2/2
```

![](img/cc8b9fd5970716027fba0d0a45c13900_201_0.png)

-   a. 按下 <Ctrl-b>。您的屏幕将与图 11-11 相似。

-   31. 本练习将让您练习将光标定位在特定行上。
    -   a. 按下 <7G> 将光标移动到第七行。注意，这是一个大写的“G”。光标应位于读取“correction fluid”的行上。
    -   b. 按下 <G> 将光标移动到文件的最后一行。
    -   c. 按下 <1G>（数字“1”）将光标移动到文件的第一行。

-   32. 本练习中的命令重新定位光标，但不会更改屏幕显示。
    -   a. 按下 <L> 将光标移动到屏幕的最低点。
    -   b. 按下 <M> 将光标移动到屏幕的中点。
    -   c. 按下 <H> 将光标移动到屏幕的最高点。

-   33. 本练习中的命令在保持光标在当前行的同时更改屏幕显示。
    -   a. 修改您在练习 31 中使用的命令，将光标移动到第九行。文本显示为“correction tape”。
    -   b. 使用一个按键将光标移动到单词“tape”的开头。
    -   c. 按下 <Ctrl-e> 八次。您会看到屏幕向上移动，而光标仍保持在第九行。您的屏幕应看起来与图 11-14 相似。

```text
correction tape

staplers -- desktop
staplers -- electric
staplers -- specialty

tape -- masking
tape -- Scotch
tape -- specialty
```

图 11-14 按下 <Ctrl-e> 八次后的屏幕显示

-   d. 光标看起来不在第 9 行。按下 <Ctrl-g> 在状态栏中显示光标所在行的行号。光标在第 9 行吗？
-   e. 再按下一次 <Ctrl-e>。屏幕再向上移动一行，但光标保持在屏幕顶部。您的屏幕应看起来与图 11-15 相似。

```text
staplers -- desktop
staplers -- electric
staplers -- specialty

tape -- masking
tape -- Scotch
tape -- specialty

folders -- file
```

图 11-15 <Ctrl-e> 改变了光标所在的行

**f.** 按下 `Ctrl-g` 再次获取状态栏显示。您的屏幕应看起来与图 11-16 相似。

```text
staplers -- desktop
staplers -- electric
staplers -- specialty


tape -- masking
tape -- Scotch
tape -- specialty


folders -- file
"supply" line 10 of 33 -- 30% -- col 1
```

![](img/cc8b9fd5970716027fba0d0a45c13900_204_0.png)

**g.** 按下 `<Ctrl-y>` 五次。您会看到屏幕向下移动，而光标保持在同一行。

**h.** 按下 `Ctrl-g` 以刷新状态栏信息。您可以看到屏幕显示已更改，但光标所在的行没有变化。您的屏幕应看起来与图 11-17 相似。

```text
correction fluid
correction pens
correction tape

staplers -- desktop
staplers -- electric
staplers -- specialty

tape -- masking
"supply" line 10 of 32 -- 31% -- col 1
```

图 11-17 <Ctrl-y> 更改了屏幕显示，但光标保持在同一行

> 要记住 <Ctrl-e> 表示“向上”而 <Ctrl-y> 表示“向下”，只需记住 <Ctrl-y> 意味着“向下”。如何记忆？“y”的尾巴指向哪个方向？

-   34. 本练习中的命令移动当前行——即光标所在的行。
    -   a. 将光标移动到第 29 行。您的屏幕应看起来与图 11-18 相似。

```text
staplers -- specialty

\ 
tape -- Masking
tape -- Scotch
tape -- specialty

\ 
folders -- file
folders -- hanging file
folders -- specialty file

\ 
Post-It notes -- pads
Post-It notes -- pop up
Post-It notes -- printed
```

# 图 11-18 光标位于第 29 行

-   b. 刷新状态栏信息以确认光标位于第 29 行。
-   c. 清除状态栏显示。
-   d. 按下 <z.>（z 后跟一个点）将当前行移动到屏幕中间。注意 "z" 和后面的点之间没有空格。您的屏幕应看起来与图 11-19 相似。

