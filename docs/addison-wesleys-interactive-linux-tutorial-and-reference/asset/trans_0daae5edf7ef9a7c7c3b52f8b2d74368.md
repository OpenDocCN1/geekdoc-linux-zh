
- **userid (用户ID)** Linux 系统中的每个用户必须拥有其独特的标识符，通常是其姓名的某种形式。这被称为用户 ID（userid）。
- **variable** 计算机内存中的一块区域，充当用于存储你创建的值（内容、数据或信息）的存储单元。
- **who** 一个报告当前登录用户的命令。
- **wildcard** 代表其他字符的一个字符。
- **write** 一个向当前登录用户发送在线消息的命令。
- **X-Window System** 大多数 Linux 图形用户界面（GUI）所基于的系统。

## 现场尝试！

### 答案密钥

### 模块 8 安全

在本节中，你可以找到我们在“现场尝试！”练习中省略的分步说明。

1. 切换到你的主目录。
   - a. 输入 `cd`
   - b. 按 `<Enter>`
2. 创建一个名为 newdir 的新目录。
   - a. 输入 `mkdir newdir`
   - b. 按 `<Enter>`
3. 列出你的主目录，并记录 newdir 的权限。
   - a. 输入 `ls -l`
   - b. 按 `<Enter>`
10. 为用户添加 newdir 的写权限。
   - a. 输入 `chmod u+w newdir`
   - b. 按 `<Enter>`
11. 列出你的主目录，并检查练习 10 中的操作结果。
   - a. 输入 `ls -l`
   - b. 按 `<Enter>`
12. 移除其他用户（others）对 newdir 的执行权限。
   - a. 输入 `chmod o-x newdir`
   - b. 按 `<Enter>`
13. 列出你的主目录，并检查练习 12 中的操作结果。
   - a. 输入 `ls -l`
   - b. 按 `<Enter>`
14. 为其他用户（others）添加写权限；移除组（group）对 `newdir` 的读权限。
   - a. 输入 `chmod g-r,o+w newdir`
   - b. 按 `<Enter>`
   输入用户类别的顺序无关紧要。第 14 题描述了先对“其他用户”执行的操作，然后是对“组”执行的操作。你在上面步骤 a 中看到的内容将“组”放在了“其他用户”之前。该命令行也可以写为 `chmod o+w,g-r newdir`。
15. 列出你的主目录，并检查练习 14 中的操作结果。
   - a. 输入 `ls -l`
   - b. 按 `<Enter>`
16. 移除用户（user）的读权限；为组（group）添加 `newdir` 的读权限。
   - a. 输入 `chmod u-r,g+r newdir`
   - b. 按 `<Enter>`
17. 列出你的主目录，并检查练习 16 中的操作结果。
   - a. 输入 `ls -l`
   - b. 按 `<Enter>`
18. 将 `newdir` 的权限更改为对所有用户可读和执行。
   - a. 输入 `chmod a=rx newdir`
   - b. 按 `<Enter>`
19. 列出你的主目录，并检查练习 18 中的操作结果。
   - a. 输入 `ls -l`
   - b. 按 `<Enter>`

### 模块 9 Shell 脚本

1. 在你的目录 practice 下创建一个子目录。将此新目录命名为 scripts。
   - a. 输入 `cd $HOME/practice`
   - b. 按 `<Enter>`
   - c. 输入 `mkdir scripts`
   - d. 按 `<Enter>`
2. 切换到目录 scripts。
   - a. 输入 `cd scripts`
   - b. 按 `<Enter>`
4. 检查你的工作。使用 `cat` 读取文件 list。
   - a. 输入 `cat list`
   - b. 按 `<Enter>`
6. 列出你的目录 scripts，以确保文件 list 的模式包含读和执行权限。
   - a. 输入 `ls -l`
   - b. 按 `<Enter>`
9. 脚本 list2 是一个文本文件。在标准输出上显示文件的内容。
   - a. 输入 `cat list2`
   - b. 按 `<Enter>`
10. 使脚本 list2 对所有用户可执行。
   - a. 输入 `chmod a+x list2`
   - b. 按 `<Enter>`
11. 当你将目录列表通过管道传递给 `less` 时，`<Enter>` 会滚动屏幕一行。`<Space Bar>` 会滚动一整屏。
13. 通过在标准输出上显示文件 ren 的内容来检查你的工作。
   - a. 输入 `cat ren`
   - b. 按 `<Enter>`
14. 使脚本 ren 对所有用户可执行。
   - a. 输入 `chmod a+x ren`
   - b. 按 `<Enter>`
15. 对于这个练习，创建一个文件以便与脚本 ren 配合使用。将该文件命名为 thisfile。使用以下文本作为文件内容："This is the text for a practice file."（或者你可以自己编造一些文本。）使用 cat 和重定向来创建文件。
   - a. 输入 `cat > thisfile`
   - b. 按 `<Enter>`
   - c. 输入 This is the text for a practice file.
   - d. 按 `<Ctrl-D>`
16. 列出你的工作目录 scripts，以确保 thisfile 存在。
   对于图 9-5：
   - a. 输入 `ls`
   - b. 按 `<Enter>`
   对于图 9-6：
   - a. 输入 `ls -l`
   - b. 按 `<Enter>`
17. 运行脚本 ren。将该新文件的名称从 thisfile 更改为 thatfile。
   - a. 输入以下任一命令：
     `ren` 或
     `./ren` 或
     `. ren` 或
     `sh ren`
     具体取决于你的系统要求。
   - b. 按 `<Enter>`
   - c. 输入 thisfile
   - d. 按 `<Enter>`
   - e. 输入 thatfile
   - f. 按 `<Enter>`
18. 列出目录 scripts，以确保文件名已被更改。
   - a. 输入 `ls`
   - b. 按 `<Enter>`
19. 切换到目录 catalog。使用双点表示法（..）进行此切换。
   - a. 输入 `cd ../catalog`
   - b. 按 `<Enter>`
21. 通过在标准输出上显示脚本 srch 的内容来检查你的工作。
   - a. 输入 `cat srch`
   - b. 按 `<Enter>`
22. 使文件 srch 对所有用户可执行。
   - a. 输入 `chmod a+x srch`
   - b. 按 `<Enter>`
23. 运行脚本 srch。针对问题“你想查找什么？”，回答“pens”、“file”或“specialty”。
   - a. 输入以下任一命令：
     `srch` 或
     `./srch` 或
     `. srch`
     `sh srch`
     具体取决于你的系统要求。
   - b. 按 `<Enter>`
   - c. 输入以下任一命令：
     `pens` 或
     `file` 或
     `specialty`
   - d. 按 `<Enter>`

### 模块 10 vi 入门

3. 切换到你的目录 catalog。
   - a. 输入 `cd $HOME/practice/catalog`
   - b. 按 `<Enter>`

### 模块 11 vi 光标移动

5. 退出 vi。
   - a. 输入 `:q`
   - b. 按 `<Enter>`
     或者
   - a. 输入 `:q!`
   - b. 按 `<Enter>`
7. 关闭 vi。
   - a. 输入 `:q`
   - b. 按 `<Enter>`
     或者
   - a. 输入 `:q!`
   - b. 按 `<Enter>`
1. 切换到你的目录 catalog。
   - a. 输入 `cd $HOME/practice/catalog`
   - b. 按 `<Enter>`
4. 退出 vi。
   - a. 输入 `:q`
   - b. 按 `<Enter>`

> 如果当你尝试退出 vi 时收到错误消息，请使用命令 `:q!` 来关闭程序。我们在 vi 高级命令模块的 CBT 中介绍了其他退出选项。

5. 使用文件 supply 重新打开 vi。
   - a. 输入 `vi supply`
   - b. 按 `<Enter>`
10. 退出 vi。
   - a. 输入 `:q`
   - b. 按 `<Enter>`
12. 使用文件 **word_by_word** 打开 vi。
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
24. 关闭 vi。
   - a. 输入 `:q`
   - b. 按 `<Enter>`
25. 使用文件 **supply** 重新打开 vi。
   - a. 输入 `vi supply`
   - b. 按 `<Enter>`
33. 此练习中的命令在保持光标当前行的同时改变屏幕显示。
   - a. 输入 `<9G>`
   - b. 按 `<w>`
34. 此练习中的命令移动当前行——即光标所在的行。
   - a. 输入 `<29G>`
   - b. 按 `<Ctrl-g>`
   - c. 按 `<Ctrl-l>`
35. 关闭 vi。
   - a. 输入 `:q`
   - b. 按 `<Enter>`

### 模块 12 vi 基本操作

1. 切换到你的目录 *practice*。
   - a. 输入 `cd $HOME/practice`
   - b. 按 `<Enter>`
2. 打开 `vi` 创建一个名为 **nowtime** 的新文件。
   - a. 输入 `vi nowtime`
   - b. 按 `<Enter>`
10. 在此练习中，你将使用 `<R>`、`<u>` 和 `<U>`。
   - e. 保存文件。
     - (1) 按 `<w>`
     - (2) 按 `<Enter>`
11. 在此练习中，你将使用 `<cw>` 向前更改一个小单词。
   - a. 使用文件 **nowtime** 打开 `vi`。
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

