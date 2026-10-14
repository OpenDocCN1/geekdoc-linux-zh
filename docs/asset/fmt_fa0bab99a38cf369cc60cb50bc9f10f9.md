
`Rmdir` will only remove empty directories, to remove directories containing sub-directories, or even files, you’ll need to use the `rm` command with the `-R` option. For example, on the `Temp/finance` directories, use `rm -R Temp`. A quick `ls` reveals that the parent folder and all of its contents are removed. Careful when using this command.

![](img/f80199d101da92d953f18eaa6205b48e_58_5.png)

## 终端中的有趣事情

尽管操作系统很严肃，Linux 社区对于一点乐趣也绝不陌生。多年来，开发者们在终端中创建并插入了各种有趣和奇特的元素。

### 终端乐趣

接下来的两个部分你将完全在终端中工作，所以开始活动一下手指吧。毕竟，全部工作不玩耍……正如俗话所说。

#### STEP 1

我们要用的第一个命令是 `sl`，它默认未安装，所以输入：`sudo apt-get install sl`。命令可以用 `sl` 运行，执行后会显示一辆蒸汽机车在屏幕上行驶（因此得名 `sl`）。输入 `LS`，注意大写，也有效。

![](img/f80199d101da92d953f18eaa6205b48e_59_0.png)

#### STEP 3

如果你曾想让电脑读出随机的命运给你，那么你很幸运。大多数发行版需要你安装 `fortune` 应用，然而 Linux Mint 有所不同，它已预先加载。你只需在终端中输入命令 `fortune`，然后尽情享受。

![](img/f80199d101da92d953f18eaa6205b48e_59_1.png)

#### STEP 2

星球大战的粉丝在终端中也能得到满足。通过 `telnet` 命令链接到远程服务器，你可以观看《Episode IV：新希望》以 ASCII 形式播放。要查看这一奇观，输入：`telnet towel.blinkenlights.nl`。

![](img/f80199d101da92d953f18eaa6205b48e_59_2.png)

#### STEP 4

`rev` 命令确实很有趣，一开始看起来像是操作系统中相当无用的添加。然而，它可以用来创建看似不可破解的密码。输入：`rev`，然后输入一些文本，下一次按下 Enter 时，你输入的内容会被反转。按 Ctrl+C 退出。

![](img/f80199d101da92d953f18eaa6205b48e_59_3.png)

#### STEP 5

如果你卡在要算出某个特定数字的所有可能因子，只需输入 `factor` 后跟该数字即可。例如，`factor 7` 输出不多，而 `factor 60` 则显示更多。

![](img/f80199d101da92d953f18eaa6205b48e_60_0.png)

#### STEP 6

在相当酷和真的很奇怪之间有一条细线。让 ASCII 牛重复文本给你听可能更偏向后者。输入 `cowsay` 后跟你想要的任何文本，例如：`cowsay Linux Mint is ace!`。事实上，你甚至可以通过牛输出 `ls` 命令，输入：`ls | cowsay`。

![](img/f80199d101da92d953f18eaa6205b48e_60_1.png)

#### STEP 7

为了进一步扩展牛元素，甚至还有一个图形化的，即非终端的，牛可用。用以下命令安装：`sudo apt-get install xcowsay`，然后安装完成后输入类似 `cowsay` 的内容，例如：`xcowsay BDM Publications`。

![](img/f80199d101da92d953f18eaa6205b48e_60_2.png)

#### STEP 8

如果你出于某种原因真的想扩展整个牛主题，那么将 `fortune` 命令通过管道传输到它：`fortune | cowsay`；对于图形化牛的等价物：`fortune | xcowsay`。此外，还有 `cowthink`。试试：`cowthink ...This book is awesome`。

![](img/f80199d101da92d953f18eaa6205b48e_60_3.png)

#### STEP 9

`toilet` 命令并不让人很有信心，我们承认。然而，它没那么糟糕。先用以下命令安装：`sudo apt-get install toilet`。然后安装完成后，输入类似：`toilet David`。或者也许将当前文件夹的内容列出通过它：`ls | toilet`。

![](img/f80199d101da92d953f18eaa6205b48e_60_4.png)

#### STEP 10

扩展 `toilet` 命令，你实际上可以通过它生成一些看起来不错的图形。例如，试试这个：`toilet -f mono12 -f metal David`。你可以输入 `toilet --help`，获取命令行参数列表以进一步扩展。

![](img/f80199d101da92d953f18eaa6205b48e_60_5.png)

## 更多终端中的有趣事情

如果之前的有趣且相当古怪的终端事情清单让你想要更多，你很幸运。我们准备了另一批一些有用和一些不太有用的命令供你尝试。

### 更多乐趣，耶

由于终端会话已经打开，你的键盘数字键也暖和起来了，这里还有另外两页终端胡闹。

#### STEP 1

还记得老 ZX Spectrum 时代的计算，当时你可以输入 `10 print "Hello", 20 goto 10` 然后 Hello 会一直列在屏幕上？好吧，在 Linux Mint 中你可以做同样的事。只需输入 `yes` 后跟一些文本，例如 `yes Linux is ace`。它会一直持续直到你按下 Ctrl+C。

![](img/f80199d101da92d953f18eaa6205b48e_61_0.png)

#### STEP 3

让一只小白猫追着你的鼠标指针在桌面上跑听起来像是浪费时间。奇怪的是，它并不是。输入：`sudo apt-get install oneko`，然后输入 `oneko` 让猫出现。移动你的‘鼠标’光标在屏幕上，猫会追它。使用 Ctrl+C 退出操作。

![](img/f80199d101da92d953f18eaa6205b48e_61_1.png)

#### STEP 2

《黑客帝国》是有史以来被图形复制最多的电影之一；甚至有 Matrix 代码的版本可用于 Linux Mint。用以下命令安装：`sudo apt-get install cmatrix`。完成后输入：`cmatrix` 然后跟随白兔。Neo。不像真正的 Matrix，你可以按 Ctrl+C 退出。

![](img/f80199d101da92d953f18eaa6205b48e_61_2.png)

#### STEP 4

这一项比之前的更严肃一些。它被称为 Fork Bomb，它所做的基本上是不断复制自身，直到用完所有可用系统资源，从而导致你的电脑崩溃。你不必尝试它，但它很有趣。只需输入 `:(){ :|:& };` 并准备好重启。

![](img/f80199d101da92d953f18eaa6205b48e_61_3.png)

#### STEP 5

串联多个命令并将它们通过管道传输到其他命令正是脚本成为操作系统强大元素的原因。使用 `while` 命令，例如，结合 `toilet`，可以产生令人印象深刻的结果。

```
Enter: while true; do echo "$[date '+%D %T']" | toilet -f term -F border --metal"; sleep 1; done.
```

![](img/f80199d101da92d953f18eaa6205b48e_62_0.png)

#### STEP 6

会说话的电脑是 80 年代的风潮，输入：`espeak "Hello, this is Linux Mint!"` 让电脑重复引号内的文本给你听。确保你的音量已打开，并尝试以下：`ls > folders.txt && espeak -f folders.txt`。这将让 Mint 读回 `ls` 命令的内容。

```
espeak "Hello, this is Linux Mint!"
```

![](img/f80199d101da92d953f18eaa6205b48e_62_1.png)

#### STEP 7

咆哮的 ASCII 火不是你拥有的最有用的命令，但很有趣。用以下命令安装：`sudo apt-get install libaa-bin`，然后安装后使用：`aafire`。它并不真正温暖，但你明白了。为了扩展上述内容，输入：`sudo apt-get install bb caca-utils`，然后，`cacafire`。

```
sudo apt-get install libaa-bin
```

```
sudo apt-get install bb caca-utils
```

![](img/f80199d101da92d953f18eaa6205b48e_62_2.png)
