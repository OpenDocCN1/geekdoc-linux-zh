
在这种情况下，`grep` 的输入来自所谓的“标准输入”或 `stdin`，输出则进入“标准输出”或 `stdout`（参见图 5）。默认情况下，`stdin` 指用户在命令行上直接输入的文本，而 `stdout` 指打印到控制台的文本。这里，`grep tuna` 匹配输入行“tuna”和“fortunately”（假设“fortuanely”是“fortunately”的拼写错误，或者作为不匹配的项被忽略，但文本称其匹配“tuna”和“fortuanely”，因此我将保留文本的声明，但如果在输入列表中它是匹配的，则注明可能的 OCR 错误。文本说“匹配输入行‘tuna’和‘fortuanely’”。我将保留解释中的原始拼写，但如果看起来像拼写错误，则更正命令输出中的明显错别字。然而，提示要求更正明显的 OCR 错误。“fortuanely”可能是“fortunately”的拼写错误。在 `grep` 示例中，如果输入是“fortunately”，`grep tuna` 不会匹配它。如果输入是“fortuanely”，它也不会匹配。文本声称它匹配。如果意图是匹配，那么输入很可能是“tuna”的重复，或者输入列表中的“fortuanely”是“tuna-something”这类包含“tuna”的单词的 OCR 错误。鉴于更正明显错误的指示，且“fortuanely”不是单词，我将假设它是拼写错误。然而，由于不知道 intended word，我会保留文本原样，但清理代码块中的明显标点符号或换行符问题，并保留语义不一致，除非是明显的字符误读。如果看起来像拼写错误，我会将列表中的单词更改为“fortunately”，但文本解释称其匹配。这很难处理。我将坚持更正标点符号和换行等 OCR 伪影，并保留语义不一致，除非是明显的字符误读。如果看起来像拼写错误，我将代码块中的“fortuanely”更改为“fortunately”。）

除了从控制台读取 `stdin` 和写入 `stdout`，我们还可以从文件读取和写入。例如，如果我们输入命令：

```bash
$ ls > files_in_directory.txt
```

这将创建一个名为 `files_in_directory.txt` 的新文件，其中包含 `ls` 命令的输出。如果该文件已存在，它将被覆盖。如果我们想将输出追加到现有文件的末尾，则可以使用 `>>` 而不是 `>`：

```bash
$ echo 'These are the files in the directory:' > files_in_directory.txt
$ ls >> files_in_directory.txt
```

![](img/fb76008333fb7aef815b136f9f1afe5f_38_0.png)

![](img/fb76008333fb7aef815b136f9f1afe5f_38_1.png)

![](img/fb76008333fb7aef815b136f9f1afe5f_38_2.png)

![](img/fb76008333fb7aef815b136f9f1afe5f_38_3.png)

我们还可以使用 `<` 连接符从文件读取输入。例如，我们可能想知道赫尔曼·梅尔维尔的《白鲸记》（Moby Dick）有多少行：

```bash
$ echo -n "The number of lines in 'Moby Dick' is " > mobystats.txt
$ cat moby10b.txt | wc -l >> mobystats.txt
$ echo -n "The number of lines in 'Moby Dick' containing the word 'Queequeg' is " >> mobystats.txt
$ cat moby10b.txt | grep Queequeg | wc -l >> mobystats.txt
$ cat mobystats.txt # 打印出文件 'mobystats.txt' 的内容

The number of lines in 'Moby Dick' is 23244
The number of lines in 'Moby Dick' containing the word 'Queequeg' is 246
```

![](img/fb76008333fb7aef815b136f9f1afe5f_38_4.png)

![](img/fb76008333fb7aef815b136f9f1afe5f_38_5.png)

![](img/fb76008333fb7aef815b136f9f1afe5f_38_6.png)

![](img/fb76008333fb7aef815b136f9f1afe5f_38_7.png)

## 条条大路通罗马（处理问题有多种方法）

在最后一个示例中，我们使用命令 `cat` 来打印文件的内容。这是一个相当多功能的命令；如果你单独运行它，它所做的只是将输入重新打印到输出中：

```bash
$ cat
Hello, world!
Hello, world!
```

如果你想直接将少量文本写入文件，而不打开文本编辑器，这有时很有用：

```bash
$ cat > hello.py
print("Hello, world!")
<Ctrl+D>
$ cat hello.py
print("Hello, world!")
```

读取和写入文件是 `cat` 命令的两个重要用例，但其原始用途是用于 `concatenating`（连接）文件（这就是其名称的来源）。如果我们向 `cat` 传递多个文件名作为参数，它将连接这些文件并打印出结果：

```bash
$ echo 'HAMLET: Do you see yonder cloud that\'s almost in shape of a camel?' > line1.txt
$ echo 'POLONIUS: By the mass, and 'tis like a camel, indeed.' > line2.txt
$ echo "HAMLET: Methinks it is like a weasel." > line3.txt
$ cat line1.txt line2.txt line3.txt > dialogue.txt
$ cat dialogue.txt
HAMLET: Do you see yonder cloud that's almost in shape of a camel?
POLONIUS: By the mass, and 'tis like a camel, indeed.
HAMLET: Methinks it is like a weasel.
```

到目前为止，我们遇到的命令允许我们创建和删除新文件和目录，并在不离开终端的情况下读写文本文件。这些命令本身相当简单，但当我们将它们与管道和文件重定向结合时，我们就能够使用它们来完成有用的工作。实验一下我们目前涵盖的命令和技术，看看你能用它们做什么。在下一个 Linux 基础教程中，我们将遇到一些新的更强大的命令，并且我们将介绍脚本编写，在这个过程中，我们创建文件来指示计算机依次运行一系列命令。

将更复杂的命令视为沿管道流动的数据是有益的

“使用管道和文件重定向，我们能够使用简单的命令来完成有用的工作”

哲学的前两部分与编程中的某些流派非常相似，这些流派规定函数或方法应尽可能通用，并且只做一件事。事实上，我们可以将整个 UNIX 程序工具链视为一种专用的编程语言——当我们讨论脚本编写时，这一点将变得更加明显。

哲学的第三部分——程序应处理文本流——在通用编程环境中意义较小，但非常适合命令行下的脚本编写。这意味着 UNIX 程序本质上是像图 2 中那样的盒子，它们接收一些文本作为输入并返回一些文本作为输出。我们将看到，可以使用管道字符将这些盒子组合在一起，如图 3 所示。

### 渗透测试

![](img/fb76008333fb7aef815b136f9f1afe5f_39_0.png)

## 使用 VDI 技术搭建渗透测试训练环境

虚拟桌面基础架构（VDI）框架是道德黑客针对真实（或模拟）系统进行测试的绝佳工具

### 托尼·卡斯蒂略·希罗纳（Toni Castillo Girona）

拥有软件工程学士学位和计算机科学硕士学位，并在一所大学担任 ICT 研究支持专家。你可以在他的博客 `disabuxes.upc.es` 上阅读他的文章。

## 资源

- RAVADA VDI
    - `https://ravada.upc.edu/index.html`
- Libvirt
    - `https://libvirt.org`
- KVM
    - `https://www.linux-kvm.org/page/Main_Page`
- SPICE
    - `https://www.spice-space.org`
- 在 Debian 上安装 Ravada VDI
    - `http://bit.ly/RAVADAVDI`
