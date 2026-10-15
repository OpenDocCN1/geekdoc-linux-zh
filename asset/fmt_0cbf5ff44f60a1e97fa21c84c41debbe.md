
# 模块 9 Shell 脚本基础与练习

1. 在你的目录 `practice` 下创建一个子目录。将此新目录命名为 `scripts`。
   - a. 输入 `cd $HOME/practice`
   - b. 按 `<Enter>`
   - c. 输入 `mkdir scripts`
   - d. 按 `<Enter>`

2. 切换到目录 `scripts`。
   - a. 输入 `cd scripts`
   - b. 按 `<Enter>`

4. 检查你的工作。使用 `cat` 读取文件 `list`。
   - a. 输入 `cat list`
   - b. 按 `<Enter>`

6. 列出你的目录 `scripts`，以确保文件 `list` 的模式包含读和执行权限。
   - a. 输入 `ls -l`
   - b. 按 `<Enter>`

9. 脚本 `list2` 是一个文本文件。在标准输出上显示文件的内容。
   - a. 输入 `cat list2`
   - b. 按 `<Enter>`

10. 使脚本 `list2` 对所有用户可执行。
    - a. 输入 `chmod a+x list2`
    - b. 按 `<Enter>`

11. 当你将目录列表通过管道传递给 `less` 时，`<Enter>` 会滚动屏幕一行。`<Space Bar>` 会滚动一整屏。

13. 通过在标准输出上显示文件 `ren` 的内容来检查你的工作。
    - a. 输入 `cat ren`
    - b. 按 `<Enter>`

14. 使脚本 `ren` 对所有用户可执行。
    - a. 输入 `chmod a+x ren`
    - b. 按 `<Enter>`

15. 对于这个练习，创建一个文件以便与脚本 `ren` 配合使用。将该文件命名为 `thisfile`。使用以下文本作为文件内容："This is the text for a practice file."（或者你可以自己编造一些文本。）使用 `cat` 和重定向来创建文件。
    - a. 输入 `cat > thisfile`
    - b. 按 `<Enter>`
    - c. 输入 `This is the text for a practice file.`
    - d. 按 `<Ctrl-D>`

16. 列出你的工作目录 `scripts`，以确保 `thisfile` 存在。
    对于图 9-5：
    - a. 输入 `ls`
    - b. 按 `<Enter>`
    
    对于图 9-6：
    - a. 输入 `ls -l`
    - b. 按 `<Enter>`

17. 运行脚本 `ren`。将该新文件的名称从 `thisfile` 更改为 `thatfile`。
    - a. 输入以下任一命令：
      - `ren`
      - 或 `./ren`
      - 或 `. ren`
      - 或 `sh ren`
      具体取决于你的系统要求。
    - b. 按 `<Enter>`
    - c. 输入 `thisfile`
    - d. 按 `<Enter>`
    - e. 输入 `thatfile`
    - f. 按 `<Enter>`

18. 列出目录 `scripts`，以确保文件名已被更改。
    - a. 输入 `ls`
    - b. 按 `<Enter>`

19. 切换到目录 `catalog`。使用双点表示法（`..`）进行此切换。
    - a. 输入 `cd ../catalog`
    - b. 按 `<Enter>`

21. 通过在标准输出上显示脚本 `srch` 的内容来检查你的工作。
    - a. 输入 `cat srch`
    - b. 按 `<Enter>`

22. 使文件 `srch` 对所有用户可执行。
    - a. 输入 `chmod a+x srch`
    - b. 按 `<Enter>`

23. 运行脚本 `srch`。针对问题“你想查找什么？”，回答 `pens`、`file` 或 `specialty`。
    - a. 输入以下任一命令：
      - `srch`
      - 或 `./srch`
      - 或 `. srch`
      - 或 `sh srch`
      具体取决于你的系统要求。
    - b. 按 `<Enter>`
    - c. 输入以下任一命令：
      - `pens`
      - 或 `file`
      - 或 `specialty`
    - d. 按 `<Enter>`

## 模块 10 vi 入门

3. 切换到你的目录 `catalog`。
   - a. 输入 `cd $HOME/practice/catalog`
   - b. 按 `<Enter>`

## 模块 11 vi 光标移动

5. 退出 `vi`。
   - a. 输入 `:q`
   - b. 按 `<Enter>`
     或者
   - a. 输入 `:q!`
   - b. 按 `<Enter>`

7. 关闭 `vi`。
   - a. 输入 `:q`
   - b. 按 `<Enter>`
     或者
   - a. 输入 `:q!`
   - b. 按 `<Enter>`

1. 切换到你的目录 `catalog`。
   - a. 输入 `cd $HOME/practice/catalog`
   - b. 按 `<Enter>`

4. 退出 `vi`。
   - a. 输入 `:q`
   - b. 按 `<Enter>`

> 如果当你尝试退出 `vi` 时收到错误消息，请使用命令 `:q!` 来关闭程序。我们在 `vi` 高级命令模块的 CBT 中介绍了其他退出选项。

5. 使用文件 `supply` 重新打开 `vi`。
   - a. 输入 `vi supply`
   - b. 按 `<Enter>`

10. 退出 `vi`。
    - a. 输入 `:q`
    - b. 按 `<Enter>`

12. 使用文件 `word_by_word` 打开 `vi`。
    - a. 输入 `vi word_by_word`
    - b. 按 `<Enter>`

14. 使用一次击键将光标移回行首。
    - a. 按 `<0>`

17. 使用一次击键将光标移至行尾。
    - a. 按 `<$>`

20. 使用一次击键将光标移回行首。
    - a. 按 `<0>`

22. 将光标移回第一行的第一个字符。
    - a. 按 `<k>`

24. 关闭 `vi`。
    - a. 输入 `:q`
    - b. 按 `<Enter>`

25. 使用文件 `supply` 重新打开 `vi`。
    - a. 输入 `vi supply`
    - b. 按 `<Enter>`

33. 此练习中的命令在保持光标当前行的同时改变屏幕显示。
    - a. 输入 `<9G>`
    - b. 按 `<w>`

34. 此练习中的命令移动当前行——即光标所在的行。
    - a. 输入 `<29G>`
    - b. 按 `<Ctrl-g>`
    - c. 按 `<Ctrl-l>`

35. 关闭 `vi`。
    - a. 输入 `:q`
    - b. 按 `<Enter>`

## 模块 12 vi 基本操作

1. 切换到你的目录 `practice`。
   - a. 输入 `cd $HOME/practice`
   - b. 按 `<Enter>`

2. 打开 `vi` 创建一个名为 `nowtime` 的新文件。
   - a. 输入 `vi nowtime`
   - b. 按 `<Enter>`

10. 在此练习中，你将使用 `<R>`、`<u>` 和 `<U>`。
    - e. 保存文件。
      - (1) 按 `<w>`
      - (2) 按 `<Enter>`

11. 在此练习中，你将使用 `<cw>` 向前更改一个小单词。
    - a. 使用文件 `nowtime` 打开 `vi`。
      - (1) 输入 `vi nowtime`
      - (2) 按 `<Enter>`

19. 在此练习中，你将删除单词。
    - i. 撤销删除。
      - (1) 按 `<u>`
    - k. 撤销删除。
      - (1) 按 `<u>`
    - n. 撤销删除。
      - (1) 按 `<u>`

21. 在此练习中，你将删除句子和段落。
    - e. 将光标移至行尾。
      - (1) 按 `<$>`
    - l. 在当前行下方创建一个空行。
      - (1) 按 `<o>`

24. 不保存文件即退出 `vi`。
    - a. 按 `:q!`
    - b. 按 `<Enter>`

## 模块 13：使用 vi 进行查找、复制和移动

1. 切换到你的 `practice` 目录。
   - a. 输入 `cd $HOME/practice`
   - b. 按 `<Enter>`

2. 使用 `vi` 打开文件 `nowtime`。
   - a. 输入 `vi nowtime`
   - b. 按 `<Enter>`

4. 在这个练习中，你将搜索 `"is"`。
   - a. 按 `<G>`
   - b. 按 `<$>`

5. 在这个练习中，你将搜索 `"right."`。
   - a. 按 `<1G>`

6. 在这个练习中，你将使用 `<yws>` 向前复制一个小单词。
   - a. 按 `<1G>`
   - b. 按 `<u>`

8. 在这个练习中，你将使用 `<y2>` 向前移动（yank）两个句子。
   - a. 按 `<0>`
   - b. 按 `<3k>`
   - c. 按 `<G>`
   - d. 按 `<o>`

9. 在这个练习中，你将使用 `<y2l>` 向前移动（yank）两个段落。
   - c. 按 `<Ctrl-I>`
   - d. 按 `<G>`
   - f. 按 `<u>`

10. 在这个练习中，你将使用 `put`（放置）命令在删除命令后插入文本。
    - b. 按 `<$>`
    - d. 按 `<0>`
    - e. 按 `<3j>`
    - h. 按 `<2h>` 或按两次 `<h>`。
    - i. 在 `"time"` 和 `"yet"` 之间插入一个空格。
      - (1) 按 `<i>`
      - (2) 按 `<Space Bar>`（空格键）
      - (3) 按 `<Esc>`

11. 在这个练习中，你将使用 `<yy>` 移动整行。
    - a. 将光标向上移动一行。
      - (1) 按 `<^K>`
    - c. 将光标移动到文件顶部。
      - (1) 按 `<^G>`
    - d. 在第一行上方创建一个空行。
      - (1) 按 `<^O>`
      - (2) 按 `<Esc>`

12. 不保存文件退出 `vi`。
    - a. 输入 `<^D^D>`
    - b. 按 `<Enter>`

## 模块 14：`vi` 高级命令

1. 切换到你的 `practice` 目录。
   - a. 输入 `cd $HOME/practice`
   - b. 按 `<Enter>`

2. 打开 `vi` 创建一个名为 `one-nine` 的新文件。
   - a. 输入 `vi one-nine`
   - b. 按 `<Enter>`

3. 创建文件 `one-nine`。你的屏幕应该看起来像图 14-1。完成文件创建后，保存它。
   - a. 按 `<i>` 使 `vi` 进入插入模式。
   - b. 输入 `One.`（注意末尾的句号。）
   - c. 按 `<Enter>`
   - d. 输入 `Two.`
   - e. 按 `<Enter>`
   - f. 输入 `Three.`
   - g. 按 `<Enter>`
   - h. 输入 `Four.`
   - i. 按 `<Enter>`
   - j. 输入 `Five.`
   - k. 按 `<Enter>`
   - l. 输入 `Six.`
   - m. 按 `<Enter>`
   - n. 输入 `Seven.`
   - o. 按 `<Enter>`
   - p. 输入 `Eight.`
   - q. 按 `<Enter>`
   - r. 输入 `Nine.`
   - s. 按 `<Esc>`
   - t. 按 `<w>`
   - u. 按 `<Enter>`

6. 在这个练习中，你将循环浏览编号缓冲区。
   - a. 按 `<j>`
   - b. 在当前行下方创建两个空行。
     - (1) 按 `<o>`
     - (2) 按 `<Enter>`
     - (3) 按 `<Esc>`

9. 在这个练习中，你将创建文件 `pressrel.text`。
   - e. 
     - (1) 按 `<i>` 使 `vi` 进入插入模式。
     - (2) 输入：
       > Robert Johnsons, VP NASR Sales, has announced the formation of a company task force whose goal will be to evaluate the utilization of telecommunication resources. AA Named to the task force today were:
     - (3) 按 `<Esc>` 退出插入模式并返回命令模式。

10. 在这个练习中，你将创建文件 `members1.text`。
    - e. 输入以下文本。每个名字应占一行：
      - (1) 按 `<i>` 使 `vi` 进入插入模式。
      - (2) 输入 `Samantha Innick`
    
    ![](img/cc8b9fd5970716027fba0d0a45c13900_322_0.png)
    
      - (3) 按 `<Enter>`
      - (4) 输入 `Samuel Stephens`
      - (5) 按 `<Enter>`
      - (6) 输入 `Andrew Thomas`
      - (7) 按 `<Esc>`
    - f. 保存文件。
      - (1) 按 `<w>`
      - (2) 按 `<Enter>`

11. 在这个练习中，你将创建文件 `members2.text`。
    - e. 输入以下文本。每个名字应占一行：
      - (1) 按 `<i>` 使 `vi` 进入插入模式。
      - (2) 输入 `Charles Denton`
      - (3) 按 `<Enter>`
      - (4) 输入 `Wendy Franks`
      - (5) 按 `<Enter>`
      - (6) 输入 `Roberta Johnson`
      - (7) 按 `<Esc>`
    - f. 保存文件。
      - (1) 按 `<w>`
      - (2) 按 `<Enter>`

12. 在这个练习中，你将检查两个人员名单中的名字拼写。
    - a. 你认为 `Wendy` 的姓氏拼写为 `"Franks"`。将拼写改为 `"Frankes"`。
      - (1) 按 `<k>`
      - (2) 按 `<i>` 使 `vi` 进入插入模式。
      - (3) 输入 `e`
      - (4) 按 `<Esc>`
    - b. 经过进一步考虑，你决定原来的拼写是正确的。删除 `"e"`。
      - (1) 按 `<x>` 删除 `"e"`。

**实战演练！答案钥匙**

204

13. 在这个练习中，你将两个成员文件的内容放入命名缓冲区。
    - d. 确保光标位于文件的第一个字符上。
      - (1) 按 `<1G>`

14. 在这个练习中，你将打开文件 `pressrel.text` 并放入命名缓冲区 `"a"` 的内容。
    - c. 将光标移动到文件的最后一行。
      - (1) 按 `<G>`

15. 在这个练习中，你将把命名缓冲区 `"b"` 的内容添加到 `pressrel.text`。
    - b. 撤销放置操作。
      - (1) 按 `<u>`

16. 将 `"Samantha Innick"` 移动到一个单独的行。
    - a. 按 `<2j>` 使光标位于 `"Roberta JohnsonSamantha Innick"` 这一行。
    - b. 按 `<w>`
    - c. 按 `<l>` 将光标移动到 `"Samantha"` 中的 `"S"`。
    - d. 按 `<i>`
    - e. 按 `<Enter>`
    - f. 按 `<Esc>`

17. 保存文件并退出 `vi`。
    - a. 按 `<wq>`
    - b. 按 `<Enter>`

![](img/cc8b9fd5970716027fba0d0a45c13900_324_0.png)

## Linux Made Easy CBT 软件最终用户许可协议

本软件许可协议（以下简称“本许可”）是您与 Edutrends, Inc.（Edutrends）之间达成的协议。Edutrends 愿意仅在您接受本许可中包含的所有条款的条件下，向您授权 `enclosed software`。在安装、复制、下载、访问或以其他方式使用该软件之前，请仔细阅读本许可，因为使用该软件即表示您同意受本许可条款的约束。如果您不同意本许可的条款，Edutrends 不愿意向您授权该软件，您应尽快将未使用的软件退还给您获取软件的地方，您的款项将被退还。

### 1. 许可授权。

伴随本许可提供的软件（无论是通过 CD-ROM、软盘还是其他介质提供的，以下简称“软件”）及相关文档，由 Edutrends 根据本许可的条款向您授权使用。本许可允许您在单台计算机上使用该软件。您还可以在家用或便携式计算机上使用该软件的副本，只要该额外副本从未在您主要使用软件的计算机上运行该软件的同一时间运行。
