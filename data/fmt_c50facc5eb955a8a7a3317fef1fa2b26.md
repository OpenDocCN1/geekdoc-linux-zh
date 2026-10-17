
```
File Edit View Search Terminal Help
daviddavid-mint --scripts $ vim helloworld.sh
daviddavid-mint --scripts chmod +x helloworld.sh
daviddavid-mint --scripts $ ls
helloworld.sh
daviddavid-mint --scripts ./helloworld.sh
```

```
File Edit View Search Tools Documents Help
### helloworld.sh
#!/bin/bash
echo Hello World!
```

![](img/9eddebb0cf792a0bbe16478be74a68e1_68_0.png)

第 6 步 `#!/bin/bash` 行告诉系统应该使用什么解释器。（`#` 表示注释行，在这种情况下是你要写的注释）。Bash 命令中的感叹号 (`!`) 意味着它会被脚本忽略，注释会被跳过，并强制脚本将该行作为命令执行。这被称为 Hash-Bang。

第 9 步虽然这并不特别令人兴奋，但“Hello World”现在显示在终端中了。`echo` 命令用于在终端中响应其他变量，随着学习的深入，你将使用 `echo` 命令进行其他输出。

```
File Edit View Search Tools Documents Help
### helloworld.sh
#!/bin/bash
echo Hello World!
```

```
File Edit View Search Tools Documents Help
### helloworld.sh
#!/bin/bash
echo Hello World! This is my first script in Linux Mint
```

第 7 步你可以通过点击 `File > Save` 保存此文件并退出回到终端。输入 `ls` 将显示文件中的脚本。要使其变为可执行并能够运行，你需要修改它的权限。使用 `chmod +x helloworld.sh` 执行。你应该为你创建每一个脚本都这样做。

第 10 步将 `echo` 想象成旧的 BASIC `print` 命令。它可以显示文本、数字或存储在系统中的任何变量（例如当前系统日期）。尝试一下：`echo Hello World! Today is $(date +%A).` `$(%A)` 正在调用存储当前星期几的变量。

```
File Edit View Search Tools Documents Help
daviddavid-mint --scripts vim helloworld.sh
daviddavid-mint --scripts $ ls
helloworld.sh
daviddavid-mint --scripts chmod +x helloworld.sh
daviddavid-mint --scripts $ ls
```

```
File Edit View Search Tools Documents Help
Hello World is Today $(date +%A)
#!/bin/bash
echo Hello World is Today $(%A)
```

## 创建 Bash 脚本 – 第二部分

之前我们查看了创建第一个 Bash 脚本 Hello World 并添加了一个系统变量。现在你可以扩展这些内容，看看当你开始尝试创建自己的变量时可以做什么。

### 变量

就像在其他任何编程语言中，Bash 脚本也可以存储和调用系统中的某些变量，无论是通用的还是自定义的

- **第 1 步**让我们从创建一个名为 `hello.sh` 的新脚本开始：`vim hello.sh`。在里面输入 `#!/bin/bash`，然后是 `echo Hello $1`。保存并退出。`chmod +x hello.sh`

- **第 3 步**现在的输出将是 Hello。这是因为 Bash 自动为用户分配了变量，并将它们传递给脚本。`$1` 持有“David”。你可以通过输入内容来更改变量：`./hello.sh`

- **第 2 步** 现在脚本是可执行的，使用 `./hello.sh` 运行它。现在，终端会显示简单的 'Hello'。但是，如果你带有变量执行命令，就很有趣了。尝试 `./hello.sh David`。

- **第 4 步** 你可以重命名变量，触发响应的变量；甚至可以使用以下内容修改脚本：`firstname=$1`, `echo Hello $surname`。将每个语句放在新行。保存脚本并回到终端。![](img/9eddebb0cf792a0bbe16478be74a68e1_69_0.png)

第 5 步 当你运行脚本时，可以使用自定义变量：`./hello.sh David`。自然地使用你自己的来更改变量。当我们只是打印内容时，让我们看看两个变量的使用。

第 8 步 让我们扩展一下。创建一个新脚本 `greetings.sh`。在截图中，保存它并使用 `chmod` 命令使其变为可执行文件。你可以看到脚本现在增加了一些内容。

| File Edit View Search Tools Documents Help |

|---|---|

| daviddavid-mint --scripts ./greetings.sh David |

| daviddavid-mint --scripts ./greetings.sh Linux Mint |

```bash
greetings.sh
#!/bin/bash
echo "Hello, what is your name?"
read firstname
echo -n "Thank you, and what is your surname?"
read surname
clear
echo Hello $firstname$surname, how are
```

第 6 步 创建名为 `addition.sh` 的新脚本，使用与 `hello.sh` 相同的格式，但更改变量。在这里我们使用 `firstnumber` 和 `secondnumber` 命令通过增加整数来执行简单的算术。和是 `$((firstnumber+secondnumber))`。保存脚本并使其可执行 (`chmod +x addition.sh`)。

第 9 步 我们为 `echo` 命令添加了 `-n`，这会让光标留在同一行。`read` 命令将用户的输入存储到变量中，稍后返回到 `echo`。

| File Edit View Search Tools Documents Help |

|---|---|

| Hello David, how are you today? |

```bash
addition.sh
#!/bin/bash
firstnumber=1
secondnumber=2
echo the sum is $((firstnumber+secondnumber))
```

第 7 步 现在运行 `addition.sh`，我们可以输入两个数字：`./addition.sh 1 2`。结果将是 3，终端显示 'The sum is 3'。尝试不同的数字看看发生什么。你也可以将脚本重命名为 `multiplication.sh` 和 `subtraction`

第 10 步 作为最后的细节，让我们包含最后部分使用的 `date` 变量。脚本的最后一行读取：`echo Hello $firstname$surname, how are you $(date)?` 输出应该显示当前的星期几，从系统变量调用它。

| File Edit View Search Tools Documents Help |

|---|---|

| daviddavid-mint --scripts ./addition.sh 1 2 |

| daviddavid-mint --scripts ./addition.sh 34 45 |

| The sum is 3 |

| The sum is 79 |

```bash
greetings.sh
#!/bin/bash
echo "Hello, what is your name?"
read firstname
echo -n "Thank you, and what is your surname?"
read surname
clear
echo Hello $firstname$surname, how are you $(date)
```

## 创建 Bash 脚本 - 第三部分

在之前的页面中，我们查看了一些非常基础的脚本：向屏幕输出文本、获取用户输入并存储以及包含系统变量。现在是循环

### IF, THEN, ELSE

在大多数编程结构中，会有需要循环你创建的命令来创建更好的功能。

- **第 1 步** 让我们现在查看 If, Then Else 语句，它们在正确执行时会比较一组指令。创建一个新脚本 `greeting2.sh` 并在编辑器中输入文本
