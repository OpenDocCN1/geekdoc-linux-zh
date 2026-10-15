
![](img/383b23573296234863a9f25dc7161abc_57_2.png)

# 创建和删除目录

与在终端中创建文件一样，你也可以创建和删除目录（如果你愿意也可以称为文件夹）。目录构成了文件系统的结构；如果没有逻辑目录，文件系统将陷入彻底的混乱。

## 管理文件夹

如何在终端中创建和删除文件夹是 Mint（实际上是整个 Linux）的一项需要掌握的重要技能。以下是你可以尝试的基础知识。

步骤 1：打开终端后，执行 `cd ~` 以确保你在自己的主目录。现在输入 `ls` 查看你当前位于主目录中的文件夹。你会发现文件夹在 Mint 中以青色（浅蓝色）标记。让我们从创建一个目录开始。输入：`mkdir testdir`。

步骤 2：如果你现在再次输入 `ls`，你会发现新目录 `testdir` 已经与主区域的其他文件夹一起被创建。显然 `mkdir` 命令是创建目录的，你已经猜出它代表 Make Directory。

步骤 3：如果你再次输入命令 `mkdir testdir`，你将收到一条消息：`mkdir: cannot create directory 'testdir': file exists`。不言而喻，在当前目录下只能有一个唯一命名的目录。但是，由于 Linux 是大小敏感的，你可以拥有 `Testdir`、`testDIR` 等。

![](img/383b23573296234863a9f25dc7161abc_57_0.png)

步骤 4：你可以在已经创建的目录内创建子目录。例如，通过 `cd testdir/` 进入目录以列出文件夹结构。自然那里什么都没有，因为你刚刚创建了该目录。现在通过 `cd ..` 返回主目录并输入 `mkdir reports`。返回测试目录，`cd testdir/` 并 `ls`。

![](img/383b23573296234863a9f25dc7161abc_57_1.png)
![](img/383b23573296234863a9f25dc7161abc_57_2.png)

### 步骤 5

创建目录的命令是逻辑性的，因此你会创建目录。但是，如果你想在一个命令中创建目录和任何子目录，请确保你在 `cd -` 位置并使用 `mkdir -p`。

### 步骤 8

现在我们已经创建了一些目录，让我们来看看删除它们。如果文件夹为空，使用 `rmdir`。如果它包含文件，你必须使用递归标记 `rm -r`。

```
File Edit View Search Terminal Help
File: Test2.txt
This is entered using the cat command from the Terminal. Cool, isn't it. Pressing Ctrl+D now...
```

![](img/383b23573296234863a9f25dc7161abc_56_0.png)
![](img/383b23573296234863a9f25dc7161abc_56_1.png)

# 使用终端

## 在终端中可以做的事情

尽管操作系统是严肃的，但 Linux 社区对乐趣并不陌生。多年来，开发者们在终端中创建并插入了各种有趣的元素。

## 终端乐趣

在接下来的章节中，你将完全在终端中工作，所以热一下你的手指。毕竟，只工作不玩……正如俗说。

- 我们将使用的第一个命令是 `sl`，它默认没有安装，所以执行 `sudo apt-get install sl`。该命令可以通过 `sl` 运行，执行会在屏幕上显示一辆蒸汽机。输入 `LS` 也有效。

- 如果你曾想让电脑为你读一段随机运势，那么你就好运了。大多数干扰需要安装 `fortune` 应用，而 Linux Mint 的不同之处在于它已经预加载。你只需要在终端中输入 `fortune` 命令并享受即可。

- 星球大战粉丝甚至在终端方面也能获得满足。通过 `telnet` 命令连接到远程服务器，你可以看到以 ASCII 格式出的《第四部：新希望》。要查看这一盛景，请输入 `telnet towel.blinklights.nl`。

- `rev` 命令确实有趣，起初似乎是操作系统中一个相当没用的添加。它可以用于创建一些看似不可破解的密码。输入 `rev`，现在输入一些文本，当你按回车时，所有内容都会反转。按 `Ctrl+C`。

## 在终端中玩的趣事

第 5 步如果你正苦于尝试任何数字的所有可能因子，只需输入 `factor`。例如，`factor 7` 提供的不多，而 `factor 60` 就会显示出来。

```
File Edit View Search Terminal Help
daviddavid-mint ~ $ factor 7
7: factor 60
60: factor $ 
daviddavid-mint ~
```

![](img/383b23573296234863a9f25dc7161abc_60_0.png)

第 6 步，相当酷炫与非常怪异之间只有一线之隔。让一只 ASCII 牛牛重复文本可能属于后者。使用 `cowsay`，Linux Mint 是 ascii 的！事实上，你可以通过以下方式让奶牛输出 `ls` 命令：`ls | cowsay`

第 7 步，为了跟随奶牛，有一个图形化的（即非终端的）奶牛可以安装，通过 `sudo apt-get install cowsay` 安装它，安装后运行带有 `cowsay` 的内容，例如：`cowsay Publications`。

第 9 步我们必须承认，`toilet` 命令并没有带给人多少信心。不过，它并没有开始时那么糟糕。通过运行 `apt-get install toilet` 来安装它。然后你可以输入类似 `toilet` 的内容。或者通过它列出当前文件夹的目录：`ls | toilet`

```
File Edit View Search Terminal Help
< Linux Mint is ascii:
$ ls
ls
/ #
```

daviddavid-mint ~ ls | cowsay

$ 通过 toilet 绘制命令：

$ Pictures Templates Test Views

daviddavid-mint ~ $
```

```
File Edit View Search Terminal Help

daviddavid-mint ~ $ toilet David

$ toilet

# # # # #

# # # # #

# # # # #

# # # # 

daviddavid-mint ~ $
```

第 10 步扩展 `toilet`，你可以通过它生成一些不错的位置。例如，尝试：`toilet -f mon12 David`。你可以输入 `toilet --help` 来查看进一步扩展的命令行参数列表。

```
File Edit View Search Terminal Help

daviddavid-mint ~ $ toilet -f mon12 David

# # # # # # 

# # # # # 

# # # # # # 

# # # # 

daviddavid-mint ~ $
```

```
File Edit View Search Terminal Help

daviddavid-mint ~ $ toilet -f mon12 David

# # # # # # 

# # # # # 

# # # # # # # 

# # # # 

daviddavid-mint ~ $
```
