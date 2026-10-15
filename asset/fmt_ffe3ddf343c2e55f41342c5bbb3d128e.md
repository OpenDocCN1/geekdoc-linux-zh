
32. 假设第 12 行有 22 个字符，第 11 行有 10 个字符。如果你在第 12 行的第六个字符并连续执行以下命令，光标在哪里？

a. `j`

b. `h`

c. `h`

33. 假设第 12 行有 22 个字符，第 11 行有 30 个字符。如果你在第 12 行的第六个字符并连续执行以下命令，光标在哪里？

a. `k` b. `h`

34. 假设文件有 70 行。缓冲区的大小是多少行？

35. 假设文件有 70 行。如果屏幕只能显示 24 行，当你打开 `vi` 时，看到的最后一行行号是多少？

36. 假设文件有 70 行。如果屏幕只能显示 24 行，在发生以下事件后，屏幕上看到的最后一行行号是多少？

a. `$ vi filename` c. `ctrl+b`

b. `ctrl+y` d. `ctrl+d`

37. 如果你觉得对文件进行所有编辑都应该放弃，以下哪个命令不会影响你的原始文件？

a. `:w` c. `:q!`

b. `:q` d. `:wq`

# 第 2 章 · vi 编辑器

38. 如果你想保存所有编辑内容并退出 `vi`，你会使用以下哪一个命令？

- a. `:w` c. `:q!`
- b. `:q` d. `:wq`

39. 如果你想保存所有编辑内容但不退出 `vi`，你会使用以下哪一个命令？

- a. `:w` c. `:q!`
- b. `:q` d. `:q`

# 实验课程

以下每个章节都使用一个或多个实际操作练习。在完成每个章节后，我们将编写一份报告，解释每一步的结果并回答提出的任何问题。

## 第一节实验

1. 登录系统。
2. 使用 `vi` 编辑器创建一个名为 `gtysbr.txt` 的文件，其中包含以下段落，并保持对齐和格式。

> Four score and seven years ago our fathers brought forth upon this continent
>
> a new country, conceived in liberty, and dedicated to the idea that
>
> all men are created equal. Now we are engaged in a great war, We have
>
> testing whether our nation, or any nation so conceived and dedicated
>
> can last. We met on a great battlefield of war. We have
>
> come to dedicate a portion of that field as a final resting-place for
>
> those who here gave their lives that that nation might live.

3. 在创建过程中纠正你的输入错误。
4. 保存文件。
5. 退出系统。

## 第二节实验

1. 登录系统。
2. 打开第一节实验中创建的文件。
3. 将之前输入的段落修改为如下所示。你应该添加一些文本、更改一些文本并删除一些文本。

> Four score and seven years ago our fathers brought forth upon this continent
>
> a new nation, conceived in liberty, and dedicated to the proposition that
>
> all men are created equal. Now we are engaged in a great civil war,
>
> testing whether that nation, or any nation so conceived and dedicated,
>
> can endure. We met on a great battlefield of war. We have
>
> come to dedicate a portion of that field as a final resting-place for
>
> those who here gave their lives that nation might live.
>
> It is very fitting and proper that we should do this. But in a
>
> larger sense, we cannot dedicate nor consecrate nor can we hollow
>
> this ground. The brave men, who died here, who struggled have
>
> consecrated far above our power to add or detract. The world will little note, nor long remember what we say here, but it can never forget what they did here.

4. 将新文件保存为名为 `gtsyrbgII.txt`。
5. 退出系统。

## 第三节实验

1. 登录系统。
2. 打开第二节实验中创建的文件。
3. 将之前输入的段落修改为如下所示。你应该添加一些文本、更改一些文本并删除一些。

Four score and seven years ago our fathers brought forth on this continent a new nation, conceived in liberty, and dedicated to the proposition that all men are created equal. We are engaged in a great civil war, testing whether that nation, or so conceived and so dedicated, can endure. We are met on a great battlefield of that war. We have come to dedicate a portion of that field as a final resting-place for those who gave their lives that this nation might live.

It is altogether fitting and proper that we should do this. But in a larger sense, we cannot dedicate, we cannot consecrate, we cannot hallow this grave. The living and dead, who struggled here consecrated far above our poor power to add or detract. The world will little note, nor long remember what we say here, but it can never forget what they did here.

It is for us the living, to be dedicated here to the unfinished work which they fought here thus so highly advanced. It is for us, to be dedicated to the great task remaining before us, that from these honored dead we take increased devotion to that cause for which they gave the last full measure of devotion: that we highly resolve that these dead shall not have died in vain; that this nation, under God, shall have a new birth of freedom, and that government of the people, by the people, shall not perish from the earth.

Abraham Lincoln

美国第16任总统

宾夕法尼亚州，格蒂斯堡

1863年11月19日

4. 在同一文件中保存更改。
5. 退出系统。

# 文件系统

UNIX 对文件的解释比大多数操作系统的解释要更宽泛¹。在 UNIX 中，文件可以是任何可以读取数据的源，也可以是任何可以写入数据的目的。因此，作为输入源的键盘是一个文件；作为输出目的的显示器是一个文件；作为另一个输出目的的打印机是一个文件；存储在磁盘上的文档（数据的源或目的）也是一个文件。

## 3.1 文件名
