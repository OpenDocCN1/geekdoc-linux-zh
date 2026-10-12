
# Linux 常用手册 (Developer's Library)

## Linux：短语表

### 目录

索引.........................................................................................................................48

索引.........................................................................................................................49

索引.........................................................................................................................49

索引.........................................................................................................................50

索引.........................................................................................................................51

索引.........................................................................................................................51

索引.........................................................................................................................52

索引.........................................................................................................................52

索引.........................................................................................................................53

索引.........................................................................................................................55

索引.........................................................................................................................55

索引.........................................................................................................................56

## 第一部分：入门

- 第 1 章：关于命令行你需要了解的
- 第 2 章：基础知识
- 第 3 章：学习命令
- 第 4 章：构建模块

### 第 1 章：关于命令行你需要了解的

在真正深入研究 `bash` shell 之前，你首先需要理解一些事情，它们对你阅读整本书会有帮助。这些是一些你必须知道的绝对规则，而且有些非常棘手，有些并不显而易见。但在理解了它们之后，你的 shell 行为某些方式就会变得通俗得多。

#### 一切皆文件

在 `Linux` 系统中，一切都是文件，这初看起来似乎是显而易见的。当然，文本文档是一个文件，`OpenOffice.org` 文档也是，别忘了还有图片、`MP3` 和视频。当然！

但目录呢？它是一个文件夹，是一种特殊的文件，包含了关于其他文件的信息。这些是由位驱动的。网络连接是文件。运行中的进程都是文件。

对于 `Linux` 来说，文件仅仅是位和字节的流。`Linux` 不在乎这些位和字节形成了什么；运行在 `Linux` 上的程序。对于 `Linux` 来说，文档和网络连接都是文件；你的文本编辑器知道如何处理文本文档，而你的网络应用程序识别网络连接。

在整本书中，我将提到“文件”。如果合适，请随时将其读为“文件”以及目录、子目录和系统上的其他一切。特别是，我将使用的许多命令在文档和目录上效果同样良好，请尽管在两者上尝试示例。

#### 文件名的最大长度

回想起使用 `MS-DOS` 的时代（颤抖！）的人记得，文件名不能超过八个字符，加上三个字母的扩展名，这让你拥有诸如 `RESUME1.DOC` 这样极具描述性的名称。相比之下，`OS` X 之前的限制扩展到 31 个字符，这听起来可能不错，但仍然使用一些看起来奇怪的名字。

（`Linux` 和 `Unix`）文件名的长度可达 255 个字符。对于文件名来说，这是一个荒谬的长度，如果你接近了那个数字，那么你的自画像应该出现在字典里“verbose”（详尽）一词旁边。你拥有最多 255 个字符，可以尽管写得描述性且准确，但不要过头。

事实上，将文件名保持在 80 个字符以下是一个好主意，因为那是你平均终端的宽度，你的文件名将在一行内显示而不会换行。但这只是建议，不是要求。用 200 多个字符描述一个文件的自由是你的；只需明智地使用它。

#### 名字大小写敏感

与 `Windows` 和 `Mac` `OS` 不同，`Linux` 在文件名方面是大小敏感的。你可以在运行 `Linux` 的电脑的同一个目录下找到这三个文件：

- `bookstoby.txt`
- `BooksToBuy.txt`
- `BooksStobuy.txt`

对于 `Linux` 文件系统来说，这是三个完全不同的文件。然而，如果你在 `Windows` 或 `Mac` `OS` 上，你将被强制命名或取消将 `BooksToBuy.txt` 添加到已包含 `bookstoby.txt` 的目录的尝试。

大小敏感也意味着命令和文件名必须完全输入以匹配它们的命令名或文件名。如果你想通过运行 `rm` 来删除文件，你不能输入 `RM` 或 `rm.txt`。如果你想删除 `bookstoby.txt` 却输入了 `rm BooksToBuy.txt`，你只是删除了错误的文件，或者什么都没删。

教训有两点：`Linux` 强制你做到精确，但精确是一件好事。同时，你获得了一种在其他操作系统中找不到的灵活性。要求的精确性和灵活性的结合是让 `Linux` 很有趣的原因之一，但对新用户来说，这地令人困惑。

#### 名字中应避免的特殊字符

每个操作系统在命名文件和目录时都有某些禁忌。如果你使用 `Mac` `OS`，冒号（`:`）是不允许的；另一方面，`Windows` 用户不能使用反斜杠（`\`）。`Linux` 也有它的禁用字符。在查看这些之前，这里是始终安全的字符：数字、字母（大写或小写）、点（`.`）和下划线（`_`）。键盘上的其他项目工作得完美，其他可能可行，但会产生复杂性，因为你的 shell 会尝试以各种方式解释它们，而有些根本无法工作。

`/` 永远不是选项；那个特定字符用于分隔目录和文件。假设你想保留一份想要购买的文件列表。你设法地将文件命名为 `to/buy.txt`（带有正斜杠）以将其区别于 `books/on_loan.txt` 和 `books/lost.txt`。现在当你尝试引用 `/home/scott/documents/books/to_buy.txt` 文件时，你的命令将无法运行，因为你的 shell 认为目录里有一个 `books` 目录，但它并不存在。

使用正斜杠，不如使用下划线（正如我在文件名的 `to_buy` 部分所的那样），或者将单词挤在一起（如 `booksToBuy.txt` 或 `BooksToBuy.txt`）。

你可以使用连字符，形成 `books-to-buy.txt`，但我发现下划线作为分隔符效果很好，同时比连字符更不显眼。如果你使用连字符，请不要将其放在文件名的开头。（注：此处原文存在大量重复错误，已根据逻辑清理）。

## 第一部分：快速入门

### 表 1.2. 通配符 * 及其匹配内容

| 命令 | 匹配项 |
| :--- | :--- |
| `rm libby1*.jpg` | `libby10.jpg` 到 `libby12.jpg`，以及 `libby1.txt` |
| `rm libby*.jpg` | `libby1.jpg` 到 `libby12.jpg`，但不包含 `libby1.txt` |
| `rm *txt` | `libby1.txt`，但不包含 `libby1.jpg` 到 `libby12.jpg` |
| `rm libby *` | `libby1.jpg` 到 `libby12.jpg`，以及 `libby1.txt`；目录中的所有文件 |



等待，原始的 OCR 在最后一行有一个拼写错误：“`libby12.jpg tRough`”。根据通配符逻辑，`rm libby *` 匹配所有以 `libby` 开头的内容。

`?` 匹配单个字符。表 1.3 显示了 `?` 的一些用法以及它们将匹配的内容。

### 表 1.3. 通配符 ? 及其匹配内容

| 命令 | 匹配项 |
| :--- | :--- |
| `rm libby1?.jpg` | `libby10.jpg` 到 `libby12.jpg`，但不包含 `libby1.txt` |
| `rm libby?.jpg` | `libby1.jpg` 到 `libby9.jpg`，但不包含 `libby10.jpg` |
| `rm libby?..*` | `libby1.jpg` 到 `libby9.jpg`，以及 `libby1.txt` |

`[ ]` 匹配一组单字符（例如 `[12]`）或由连字符分隔的字符范围（例如 `[1–3]`）。表 1.4 显示了 `[ ]` 的一些用法以及它们将匹配的内容。

### 表 1.4. 通配符 [] 及其匹配内容

| 命令 | 匹配项 |
| :--- | :--- |
| `rm libby1[12].jpg` | `libby11.jpg` 和 `libby12.jpg`，但不包含 `libby10.jpg` |
| `rm libby1[0–2].jpg` | `libby10.jpg` 到 `libby12.jpg`，但不包含 `libby1.jpg` |
| `rm libby[6-8].jpg` | `libby6.jpg` 到 `libby8.jpg`，但不包含其他内容 |

你将在整本书中使用所有的这些符号，所以现在介绍它们是很好的。它们会让在命令行中处理文件变得简单得多，你也会发现它们非常有帮助。

### 总结

你已经学习了对于新用户可能并不显而易见的 `Linux`，但当你开始使用 `shell` 和命令时，这些知识将大有用处。本章的细节在你开始应用后续章节的内容时可能会让你头疼。是否好奇为什么你不能复制带空格的目录、如何一次删除 1000 个文件，或者为什么你不能运行 `RM bookstobuy.txt`？这些都不是问题。通过提前掌握知识，你可以避免困扰过许多人的常见错误。

现在准备就绪，是时候进入并学习命令了。翻页，我们开始吧！

## 第 2 章：基础知识

本章介绍了你每天都会遇到几次的基本命令。把这些命令想象成木工放在工具箱顶部的锤子、螺丝刀和钳子。学习这些命令后，你就可以开始控制你的 `shell`，并发现关于文件、文件夹、数据和环境的各种有趣事情。

### 列出文件和文件夹

```bash
ls
```

`ls` 命令可能是人们发现使用最频繁的一个。毕竟，在操作和使用目录中的文件之前，你必须先知道有哪些可用文件。这就是 `ls` 发挥用场的地方，因为它列出了目录中找到的文件和子目录。

注意：`ls` 命令听起来可能很简单——只需显示文件即可——但这个极其灵活的命令有许多令人惊讶的变体，正如你将看到的那样。

输入 `ls` 会列出你当前所在目录的内容。当你首次登录 `shell` 时，你会发现自己处于主目录。输入 `ls`，你可能会看到如下内容：

```bash
$ ls
alias Desktop iso pictures program_files todo
bin documents music podcasts src videos
```

### 列出其他文件夹的内容

```bash
ls music
```

不需要进入某个目录就可以查看它有什么。假设你在主目录中，但想查看 `music` 目录里有什么。只需输入 `ls` 命令，后面跟上想要查看内容的文件夹名称，你就会看到：

```bash
$ ls music
Buddy_Holly Clash Donald_Fagen new
```

在上一个示例中使用了相对路径，但绝对路径同样有效。

```bash
$ ls /home/scott/music
Buddy_Holly Clash Donald_Fagen new
```

当你不想每次想查看目录内容时都在系统中四处移动时，指定相对路径或绝对路径的能力非常有用。不确定你是否还有那个老虎·伍兹下推杆？试试这个（`~` 类似于一个别名，代表你的主目录）：

```bash
$ ls -videos
Ubuntu_Falk.mpeg nerdtv_1_andy_hertzfeld
airhorn_surprise.wmv nerdtv_2_max_levchin/apple_navigator.mov nerdtv_3_bill_joy
b-ball-e-mail.mov RPG_Nodes.mpeg
carwreck.mpg tiger_woods_did_it.wmv
```

是的，它是。

### 使用通配符列出文件夹内容

```bash
ls ~//*
```

你刚刚学会了如何在充满文件的目录中找到文件，但有一种更快的方法。如果你知道视频格式以 `.wmv` 结尾，你可以使用通配符来显示具有特定扩展名的文件。（等待，这里的 OCR 很乱，让我们根据上下文修复它）：

“如果你知道视频格式以 `.wmv` 结尾，你可以使用通配符来显示具有特定扩展名的文件。”

```bash
$ ls ~/videos/*.wmv
Ubuntu-Talk.wmv nerdtv_1_andy_hertzfeld
airhorn_surprise.wmv nerdtv_2_max_levchin/apple_store.wmv nerdtv_3_bill_joy
b-ball-e-mail.wmv carwreck.mpg
tiger_woods_did_it.wmv
```

还有另一种更快的方法，也涉及通配符：

```bash
$ ls ~//*tiger*
tiger_woods_did_it.wmv
```

### 查看子文件夹中的文件列表

```bash
ls -R
```

你可以用一个命令查看多个子目录的内容。假设你是一个需要安装程序的 `Linux` 用户，几天前在到处寻找以确保万无一，运行以下命令（除了 `ls -R`，你可以使用 `ls --recursive`）：

```bash
$ ls -R /iso
iso:
debian-13-netinst.iso knoppix
iso/knoppix:
ubuntu-V4.0.2-DVD.iso
iso/ubuntu:
ubuntu-5.10-install.iso
```

### 以单列查看内容列表

```bash
ls -
```

到目前为止，你一直在使用 `ls` 的默认输出。注意 `ls` 按字母顺序分列打印目录内容，为了可读性，每列之间至少有两个空格。但如果你想以不同的方式查看内容呢？如果多列不是你的心菜，你可以改为单列查看内容，使用 `ls -1`（注：原文为 `ls -`，推测为误，应为 `-1`）。

到此为止，你学习了对于新用户可能并不明显的 `Linux`，但当你开始使用 `shell` 和命令时，这些知识将大有用处。本章的细节在你开始应用后续章节的内容时可能会让你头疼。是否好奇为什么你不能复制带空格的目录、如何一次删除 1000 个文件，或者为什么你不能运行 `RM bookstobuy.txt`？这些都不是问题。通过提前掌握知识，你可以避免困扰过许多人的常见错误。

现在准备就绪，是时候进入并学习命令了。翻页，我们开始吧！

## 第 2 章：基础知识

本章介绍了你每天都会遇到几次的基本命令。把这些命令想象成木工放在工具箱顶部的锤子、螺丝刀和钳子。学习这些命令后，你就可以开始控制你的 `shell`，并发现关于文件、文件夹、数据和环境的各种有趣事情。

### 列出文件和文件夹

```bash
ls
```

`ls` 命令可能是人们发现使用最频繁的一个。毕竟，在操作和使用目录中的文件之前，你必须先知道有哪些可用文件。这就是 `ls` 发挥用场的地方，因为它列出了目录中找到的文件和子目录。

注意：`ls` 命令听起来可能很简单——只需显示文件即可——但这个极其灵活的命令有许多令人惊讶的变体，正如你将看到的那样。

输入 `ls` 会列出你当前所在目录的内容。当你首次登录 `shell` 时，你会发现自己处于主目录。输入 `ls`，你可能会看到如下内容：

```bash
$ ls
alias Desktop iso pictures program_files todo
bin documents music podcasts src videos
```

### 列出其他文件夹的内容

```bash
ls music
```

不需要进入某个目录就可以查看它有什么。假设你在主目录中，但想查看 `music` 目录里有什么。只需输入 `ls` 命令，后面跟上想要查看内容的文件夹名称，你就会看到：

```bash
$ ls music
Buddy_Holly Clash Donald_Fagen new
```

在上一个示例中使用了相对路径，但绝对路径同样有效。

```bash
$ ls /home/scott/music
Buddy_Holly Clash Donald_Fagen new
```



当你不想每次想查看目录内容时都在系统中四处移动时，指定相对路径或绝对路径的能力非常有用。不确定你是否还有那个老虎·伍兹下推杆？试试这个（`~` 类似于一个别名，代表你的主目录）：

```bash
$ ls ~videos
Ubuntu_Falk.mpeg nerdtv_1_andy_hertzfeld
airhorn_surprise.wmv nerdtv_2_max_levchin/apple_navigator.mov nerdtv_3_bill_joy
b-ball-e-mail.mov RPG_Nodes.mpeg
carwreck.mpg tiger_woods_did_it.wmv
```

是的，它是。

### 使用通配符列出文件夹内容

```bash
ls ~//*
```

你刚刚学会了如何在充满文件的目录中找到文件，但有一种更快的方法。如果你知道视频格式以 `.wmv` 结尾，你可以使用通配符来显示具有特定扩展名的文件。（等待，这里的 OCR 很乱，让我们根据上下文修复它）：

“如果你知道视频格式以 `.wmv` 结尾，你可以使用通配符来显示具有特定扩展名的文件。”

```bash
$ ls ~/videos/*.wmv
Ubuntu-Talk.wmv nerdtv_1_andy_hertzfeld
airhorn_surprise.wmv nerdtv_2_max_levchin/apple_store.wmv nerdtv_3_bill_joy
b-ball-e-mail.wmv carwreck.mpg
tiger_woods_did_it.wmv
```

还有另一种更快的方法，也涉及通配符：

```bash
$ ls ~//*tiger*
tiger_woods_did_it.wmv
```

### 查看子文件夹中的文件列表

```bash
ls -R
```

你可以用一个命令查看多个子目录的内容。假设你是一个需要安装程序的 `Linux` 用户，几天前在到处寻找以确保万无一，运行以下命令（除了 `ls -R`，你可以使用 `ls --recursive`）：

```bash
$ ls -R /iso
iso:
debian-13-netinst.iso knoppix
iso/knoppix:
ubuntu-V4.0.2-DVD.iso
iso/ubuntu:
ubuntu-5.10-install.iso
```

### 以单列查看内容列表

```bash
ls -
```

到目前为止，你一直在使用 `ls` 的默认输出。注意 `ls` 按字母顺序分列打印目录内容，为了可读性，每列之间至少有两个空格。但如果你想以不同的方式查看内容呢？如果多列不是你的心菜，你可以改为单列查看内容，使用 `ls -1`（注：原文为 `ls -`，推测为误，应为 `-1`）。

到此为止，你学习了对于新用户可能并不明显的 `Linux`，但当你开始使用 shell 和命令时，这些知识将大有用处。本章的细节在你开始应用后续章节的内容时可能会让你头疼。是否好奇为什么你不能复制带空格的目录、如何一次删除 1000 个文件，或者为什么你不能运行 `RM bookstobuy.txt`？这些都不是问题。通过提前掌握知识，你可以避免困扰过许多人的常见错误。

现在准备就绪，是时候进入并学习命令了。翻页，我们开始吧！

## 第 2 章：基础知识

本章介绍了你每天都会遇到几次的基本命令。把这些命令想象成木工放在工具箱顶部的锤子、螺丝刀和钳子。学习这些命令后，你就可以开始控制你的 shell，并发现关于文件、文件夹、数据和环境的各种有趣事情。

### 列出文件和文件夹

```bash
ls
```

`ls` 命令可能是人们发现使用最频繁的一个。毕竟，在操作和使用目录中的文件之前，你必须先知道有哪些可用文件。这就是 `ls` 发挥用场的地方，因为它列出了目录中找到的文件和子目录。

注意：`ls` 命令听起来可能很简单——只需显示文件即可——但这个极其灵活的命令有许多令人惊讶的变体，正如你将看到的那样。

输入 `ls` 会列出你当前所在目录的内容。当你首次登录 shell 时，你会发现自己处于主目录。输入 `ls`，你可能会看到如下内容：

```bash
$ ls
alias Desktop iso pictures program_files todo
bin documents music podcasts src videos
```

### 列出其他文件夹的内容

```bash
ls music
```

不需要进入某个目录就可以查看它有什么。假设你在主目录中，但想查看 `music` 目录里有什么。只需输入 `ls` 命令，后面跟上想要查看内容的文件夹名称，你就会看到：

```bash
$ ls music
Buddy_Holly Clash Donald_Fagen new
```

在上一个示例中使用了相对路径，但绝对路径同样有效。

```bash
$ ls /home/scott/music
Buddy_Holly Clash Donald_Fagen new
```

指定相对路径或绝对路径的能力，当你不想每次想查看目录内容时都在系统中四处移动时，非常有用。不确定你是否还有那个老虎·伍兹下推杆？试试这个（`~` 类似于一个别名，代表你的主目录）：

```bash
$ ls -videos
Ubuntu_Falk.mpeg nerdtv_1_andy_hertzfeld
airhorn_surprise.wmv nerdtv_2_max_levchin/apple_navigator.mov nerdtv_3_bill_joy
b-ball-e-mail.mov RPG_Nodes.mpeg
carwreck.mpg tiger_woods_did_it.wmv
```

是的，它是。

### 使用通配符列出文件夹内容

```bash
ls ~//*
```

你刚刚学会了如何在充满文件的目录中找到文件，但有一种更快的方法。如果你知道视频格式以 `.wmv` 结尾，你可以使用通配符来显示具有特定扩展名的文件。（等待，这里的 OCR 很乱，让我们根据上下文修复它）：

“如果你知道视频格式以 `.wmv` 结尾，你可以使用通配符来显示具有特定扩展名的文件。”

```bash
$ ls ~/videos/*.wmv
Ubuntu-Talk.wmv nerdtv_1_andy_hertzfeld
airhorn_surprise.wmv nerdtv_2_max_levchin/apple_store.wmv nerdtv_3_bill_joy
b-ball-e-mail.wmv carwreck.mpg
tiger_woods_did_it.wmv
```

还有另一种更快的方法，也涉及通配符：

```bash
$ ls ~//*tiger*
tiger_woods_did_it.wmv
```

### 查看子文件夹中的文件列表

```bash
ls -R
```

你可以用一个命令查看多个子目录的内容。假设你是一个需要安装程序的 `Linux` 用户，几天前在到处寻找以确保万无一，运行以下命令（除了 `ls -R`，你可以使用 `ls --recursive`）：

```bash
$ ls -R /iso
iso:
debian-13-netinst.iso knoppix
iso/knoppix:
ubuntu-V4.0.2-DVD.iso
iso/ubuntu:
ubuntu-5.10-install.iso
```

### 以单列查看内容列表

```bash
ls -
```

到目前为止，你一直在使用 `ls` 的默认输出。注意 `ls` 按字母顺序分列打印目录内容，为了可读性，每列之间至少有两个空格。但如果你想以不同的方式查看内容呢？如果多列不是你的心菜，你可以改为单列查看内容，使用 `ls -1`（注：原文为 `ls -`，推测为误，应为 `-1`）。

到此为止，你学习了对于新用户可能并不明显的 `Linux`，但当你开始使用 shell 和命令时，这些知识将大有用处。本章的细节在你开始应用后续章节的内容时可能会让你头疼。是否好奇为什么你不能复制带空格的目录、如何一次删除 1000 个文件，或者为什么你不能运行 `RM bookstobuy.txt`？这些都不是问题。通过提前掌握知识，你可以避免困扰过许多人的常见错误。

现在准备就绪，是时候进入并学习命令了。翻页，我们开始吧！

## 第一部分：入门指南

| 表 2.1 符号与文件类型 |
| :--- |
| **字符** | **含义** |
| `*` | 可执行文件 |
| `/` | 目录 |
| `@` | 符号链接 |
| `` | FIFO |
| `=` | Socket |

### 以彩色显示内容

```bash
ls --color
```

除了使用 `-F` 选项时在文件和文件夹后附加符号外，你还可以请求 shell 以彩色显示内容，这为分类和区分项目提供了额外的方法。许多 `Linux` 安装版已经为 shell 开启了颜色，如果你的系统没有开启，只需使用 `--color` 选项即可。



# 第一部分：入门

## 查看文件类型与颜色

```
$ ls --color
adblock_filters.txt fixm3u pix2tn.pl
addext* flash.xml pop_login
address_book.csv getip procmail/
```

在这种设置下，可执行文件是绿色的，目录是蓝色的，普通文件是黑色的（这是我终端文本的默认颜色）。表 2.2 提供了常见颜色对应的完整列表（但请记住，这些颜色在特定的发行版中可能会有所不同）。

### 表 2.2 颜色与文件类型

| 颜色 | 含义 |
| :--- | :--- |
| 默认 shell 颜色 | 普通文件 |
| 绿色 | 可执行文件 |
| 蓝色 | 符号链接 |
| 品红色 | FIFO |
| 黄色 | Socket |
| 品红色 | 存档 (`.tar`, `.zip`, `.deb`, `.rpm`) |
| 品红色 | 图片 (`.jpg`, `.gif`, `.png`, `.tiff`) |
| 品红色 | 音频 (`.mp3`, `.ogg`, `.wav`) |

**提示**

想要查看系统中各种文件映射的颜色吗？输入 `dircolors --print-database`，然后仔细阅读结果。你也可以使用 `dircolors` 命令来更改这些颜色。

结合使用 `--color` 和 `-F`，你可以一眼看出目录中处理哪些文件。现在进入正轨了！

```
$ ls -F --color
adblock_filters.txt fixm3u* pix2tn.pl*
addext* flash.xml* pop_login*
address_book.csv getip* procmail/
```

## 列出权限、所有权及更多

### 长格式列表

```
ls -l
```

你现在已经学会了如何格式化 `ls` 的结果来让你了解更多目录的内容，但实际内容本身呢？你如何了解更多关于文件和文件夹的信息，例如它们的大小、所有者以及谁可以对它们操作？要获取这些信息，你需要使用 `-l` 选项（或 `--format=long`）。

```
$ ls -l /bin
total 2951
-rw-r---- 1 scott 15058 2005-10-03 18:49 adblock_filters.txt
-rwx-xr-x 1 scott 33 2005-04-09 09:45 addext
-rw-r---- 1 scott 245015 2005-10-15 22:38 backup
-drwxr-xr-x 9 scott 1080 2005-02-22 14:42 bin_on_bacon
-rw-r--r-- 1 scott 27641 2005-10-14 13:50 calendar.ics
-drwxr-xr-x 1 root 190 2005-04-09 09:45 convertsize
-drwxr-xr-x 2 scott 48 2005-04-09 09:45 credentials
```

`-l` 选项代表 `long`（长格式），如你所见，它提供了关于目录所在文件的丰富数据。让我们从左到右讨论你看到的内容。

最右侧第一个是最容易的项目：列出的项目名称。想让 `ls` 显示更多相关信息吗？配合 `-l` 使用 `-F` 选项，例如：`ls -lF`。颜色也可以通过 `ls --color` 轻松获取。

向左移动看到，你会看到日期和时间。这是文件最后修改的时间，包括日期（年-月-日）然后是时间（24小时制军事时间）。

再向左侧是一个表示项目大小的数字，单位是字节（bytes）。对于目录大小，这有点复杂；之前的读者说 `bin_on_bacon` 是 1080 字节，或者略多于一千字节，但它内部包含了 887KB 的内容。根据 `ls -l`，`credentials` 目录是 48 字节，但它内部什么都没有！这是怎么了？

记得在第1章“关于命令行你需要了解的知识”中，你学过目录只是包含其内容列表的特殊文件。在这里，`credentials` 的内容仅仅是所有目录都指向父目录的 `.`，所以它是 48 字节；而 `bin_on_bacon` 包含了关于 30 多个项目的信息，使其大小增加到 1080 字节。

左边接两列分别是文件的所有者和所属组。如你在之前的列表所示，几乎每个文件都属于用户 `scott` 和组 `scott`，除了 `addext` 和 `convertsize`，它们属于 `root`。

**提示**

想要让 `ls` 显示更多相关信息吗？配合 `-l` 使用 `-F` 选项，例如：`ls -lF`。颜色也可以通过 `ls --color` 轻松获取。

```
-rw-r--r-- 1 scott 1026 2005-09-25 00:11 .audacity
drwxr-xr-x 1 scott 592 2005-10-18 11:22 .Azureus
-rw------  1 scott 8800 2005-10-18 19:55 .bash_history
```

**注意**

从本章的这一点起，如果 `scott` 是文件的所有者和组，我将从列表中删除该日期。

### 反序列出内容

```
ls -r
```

如果你不喜欢 `-l` 使用的默认字母顺序，可以通过添加 `-r`（或 `--reverse`）来反转该顺序。

```
$ ls -lar /
-rw-w------ 8800 2005-10-18 19:55 .bash_history
drwxr-xr-x 592 2005-10-18 11:22 .Azureus
-rw-r--r-- 1026 2005-09-25 00:11 .audacity
drwx------ 72 2005-09-16 19:14 .aptitude
drwxr-xr-x 200 2005-07-28 01:31 alias
```

**注意**

请记住这是 `-r`，而不是 `-R`。`-r` 表示反转（reverse），而 `-R` 表示递归（recursive）。

当你使用 `-l` 时，输出是根据文件和文件夹名称按字母排序的；添加 `-r` 会反转输出，但它仍然是基于文件名的。请记住，在你使用 `ls` 的任何时候，几乎都可以添加 `-r`，以反转你所输入的命令和选项的默认输出。

### 按文件扩展名排序内容

```
ls -X
```

文件名并不是你用于字母顺序排序的唯一依据。你也可以按文件扩展名进行字母顺序排序。换句话说，你可以告诉 `ls` 将所有 `.doc` 结尾的文件分在一起，然后是以 `.jpg` 结尾的文件，最后以 `.txt` 结尾的文件结束。使用 `-X` 选项（或 `--sort-extension`）；如果你想反转排序，添加 `-r` 选项（`--reverse`）。

```
$ ls -X /src
drwxr-xr-x 320 2005-10-06 22:35 backups
drwxr-xr-x 1336 2005-10-09 18:51 fonts
-rw-r--r-- 298301 2005-06-20 02:15 install.tar.gz
-rw-r--r-- 6683923 2005-09-24 22:41 DuckDoom.zip
```

文件夹会列在列表中（毕竟它们没有扩展名），随后是具有扩展名的文件。特别注意 `install.tar.gz`；它有两个扩展名，但最后的扩展名 `.gz` 才是 `ls` 使用的。

### 按日期和时间排序内容

```
ls -t
```

字母很棒，但有时你需要按日期和时间对目录内容进行排序。要这样做，请配合 `-l` 使用 `-t`（或 `--sort=time`）；要反转排序，请配合 `-l` 使用 `-tr`（或 `--sort=reverse`）。

```
$ ls -lat /
--rw----------- 8800 2005-10-18 19:55 .bash_history
drwx------ 368 2005-10-18 23:12 .gnupg
drwxr-xr-x 2760 2005-10-18 23:14 bin
drwx------ 168 2005-10-19 00:13 .Skype
```

除了最后一项外，所有这些项目都是在同一天内被修改的；如果不使用 `-r` 选项并反转结果，最后一项将会排在第一。

**注意**

注意你在上一个命令中使用了四个选项：`-lat`。你本可以使用 `-l -a -t -r`，但谁想输入所有的连字符呢？将它们全部合并成一个巨大的选项更快更方便。然而，选项的长版本（那些以两个连字符开头并由一个或两个单词组成的）不能合并，必须分开输入，例如 `-la --sort=time --reverse`。

### 按大小排序内容

你也可以按大小排序，而不是按文件名、扩展名或日期时间排序。要按大小排序，使用 `-lS`（或 `--sort=size`）。

```
$ ls -laS /
-rw-r--r-- 109578 2005-10-19 11:53 .session-errors
--rw-r-- 40122 2005-04-20 11:00 .nessurc
-rxr-r-- 15465 2005-10-12 15:45 .vimrc
--rxr-r-- 8757 2005-10-19 08:43 .bash_history
```



当你按大小排序时，最大的项目排在前面。要反向排序，让最小的排在顶部，请使用 `-r`。

### 以 K、M 和 G 表示文件大小

`ls -h`

在上一节中，该行意味着文件约为 KB，但将字节转换为等值的 KB 或兆字节并不总是方便的。大多数时候使用 `-h` 选项（或 `--human-readable`）更易理解。

```
$ ls -lh /
100K 2005-10-19 11:44 .session-errors
--rw-r-- 40K 2005-04-20 11:00 .nessurc
-rxr-r-- 16K 2005-10-12 15:45 .vimrc
--rxr-r-- 8K 2005-10-19 08:43 .bash_history
```

在这个示例中，使用 `-h` 用于千字节；如果文件很大，你会看到 `M` 表示兆字节或 `G` 表示吉字节。有些人可能会奇怪 `1024` 字节是如何变成 `1K` 的，所以除以 `1024` 得到千字节。一个兆字节实际上是 `1048576` 字节，而吉字节是 `1073741824` 字节，所以类似的转换适用于这些。

注意

```
alias ls='ls -F'
alias ll='ls -l'
alias la='ls -a'
alias lr='ls -R'
```

### 显示当前目录路径

`pwd`

当然，当你列目录内容时可能会发现自己不知道在哪里。怎么知道？答案是 `pwd` 命令，它的意思是 `print directory`。

注意

单词 `print directory` 的意思是“打印到屏幕”，而不是“发送到打印机”。

`pwd` 命令显示当前工作目录的全绝对路径。它不是经常使用的东西，但当你感到困惑时它非常有用。

```
$ pwd
/home/scott/music/new
```

### 切换目录

`cd`

通过指定路径列出任何目录是可能的，但你通常想进入一个新目录。这就是 `cd` 命令的用场，另一个 shell 爱好者经常使用的命令。`cd` 命令非常简单：只需输入 `cd`。

`~`

你应该了解一些 `cd` 的便捷快捷方法。无论你在哪里，只需输入 `cd` 就会回到主目录。这是一个棒的节省时间的工具，你会经常使用它。或者，如果你愿意，可以使用 `cd ~`，因为 `~` 就像“我的主目录”的快捷方式。

```
$ pwd
/home/scott/music
cd ~
$ pwd
/home/scott
```

### 切换到上一个目录

另一个有趣的可能性是 `cd -`，它可以带回到上一个目录并运行 `pwd` 命令，打印你新的（还是旧的？）位置。你可以从这个示例看到它的作用。

```
$ pwd
/home/scott
cd music/new
$ pwd
/home/scott/music/new
cd -
/home/scott
```

当你想要进入一个目录执行某些操作然后返回原始目录时，使用 `cd -` 非常有用。`pwd` 提供的额外信息只是确保你在你在的地方。

### 将文件修改为当前时间

`touch`

`touch` 命令并不是经常使用的，但当你阅读这本书时会需要它，所以现在涵盖它是很好的。有趣的是，`touch` 存在的主要原因——更新文件的访问和修改时间——并不是使用该命令的主要原因。相反，你将依赖于它的次要用途！

注意

只有当你拥有该文件的写权限时，才能对文件使用 `touch` 命令并更改时间。否则，`touch` 会失败。

要同时更新文件（或文件夹）的访问和修改时间，只需运行 `touch` 命令。

```
$ ls -l ~/
848 2005-10-19 11:36 src
drwxr-xr-x 1664 2005-10-18 12:07 todo
drwxr-xr-x 632 2005-10-18 12:25 videos
-rw------      239 2005-09-10 23:12 wireless.log
$ ls -l ~/
848 2005-10-19 11:36 src
drwxr-xr-x 1664 2005-10-18 12:07 todo
drwxr-xr-x 632 2005-10-18 12:25 videos
-rw-r--r-- 239 2005-10-19 14:00 wireless.log
```

### 将文件更改为任何所需时间

`touch -t`

请记住，你不限于当前的日期和时间。相反，你可以选择任何你日期和时间，只要你使用此选项和模式：`-t [[CC]YY]MMDDhhmm[.ss]`。该模式在表2.4中解释。

表2.4. 更改文件时间的模式

| 字符 | 含义 |
| :--- | :--- |
| `CC` | 四位年份的前两个字符 |
| `YY` | 二位年份：<br>-如果是 `00-68`，假设前两位数字是 `20`<br>-如果是 `69-99`，假设前两位数字是 `19`<br>-如果为空， |
| `MMDD` | 月份和日期 |
| `hhmm` | 小时和分钟 |
| `.ss` | 秒（可选） |

| 字段 | 格式 | 范围 |
| :--- | :--- | :--- |
| 月份 | `MM` | `0112` |
| 日期 | `DD` | `0131` |
| 小时 | `hh` | `0123` |
| 分钟 | `mm` | `0059` |
| 秒 | `ss` | `0059` |

如果你要使用的数字通常不是两位，那么包含零非常重要，否则你的模式将无法工作。这里是使用 `-t` 选项的一些 `touch` 命令示例，可以帮助你开始。

```
$ ls -l
--rw-r--r-- 239 2005-10-19 14:00 wireless.log
$ touch -t 1970021607011 wireless.log
$ ls -l
--rw-r--r-- 239 1970-02-16 07:01 wireless.log
$ touch -t 9212310000 wireless.log
$ ls -l
--rw-r--r-- 239 1992-12-31 00:00 wireless.log
$ touch -t 340501720324 wireless.log
$ ls -l
--rw-r--r-- 239 2034-05-17 02:34 wireless.log
$ touch -t 10191730022 wireless.log
$ ls -l
--rw-r--r-- 239 2005-10-19 17:03 wireless.log
```

首先你设定了 `wireless.log` 的当前日期时间为 `2005-10-19 14:00`。然后你回到了大约 `35` 年前，即 `1970-02-16 07:01`，然后向前进入未来到 `2034-05-17 02:34`，那时 Linux 计算机将统治世界，人类将在和平与开源财产中生活，然后回到我们现在的时代。

你应该从这个演示中汲取几个教训。通过指定完整的四位年份（`1970`）、月份（`02`）、日期（`16`）、小时（`07`）和分钟（`01`），你回到了三十以前。你不需要指定秒。之后，如果你再次提供五位年份，例如 `9212310000` 在 `6999` 的范围内，因此 `touch` 假设你指的是 `19` 为基础世纪；而在 `340501720324` 中介于 `0` 和 `68` 之间，因此使用 `20` 作为基础世纪。最后一次使用 `touch` 时，完全没有指定年份，只有月份（`10`）、日期（`19`）、小时（`17`）和分钟（`03`），所以 `touch` 知道你指的是当前的 `2005` 年。通过理解如何操作 `touch`，你可以在需要时更改文件的时间戳。

### 创建新空文件

`touch`

但这并不是人们使用 `touch` 的主要原因。如果你尝试对一个不存在的文件使用 `touch` 命令，它会产生一个有趣的效果：它使用你指定的名称创建一个空文件。

```
$ ls -l ~/
drwxr-xr-x 848 2005-10-19 11:36 src
drwxr-xr-x 632 2005-10-18 12:25 videos
```

```
$ touch test.txt
$ ls -l -f
```

```
drwxr-xr-x 848 2005-10-19 11:36 src
-rw-r--r-- 0 2005-10-19 23:41 test.txt
drwxr-xr-x 632 2005-10-18 12:25 videos
```

你为什么要这样使用 `touch` 呢？假设你现在创建一个文件，稍后再向其中填充内容。或者你在玩新新的命令时，需要创建几个文件对其进行测试。这两者都是极佳的理由，当你开始学习更多关于 shell 时，你会发现更多原因。

### 创建新目录

`mkdir`

`touch` 命令创建空文件，但你如何创建一个新文件夹呢？通过 `mkdir` 命令就可以实现。

```
$ ls -l
```

```
drwxr-xr-x 848 2005-10-19 11:36 src
drwxr-xr-x 632 2005-10-18 12:25 videos
```

```
$ mkdir test
$ ls -l -f
```



```
drwxr-xr-x 848 2005-10-19 11:36 src
-drwxr-xr-x 48 2005-10-19 23:50 test
drwxr-xr-x 632 2005-10-18 12:25 videos
```

### 注意

在大多数系统上，`mkdir`创建的新目录赋予所有者读、写和执行权限，而给组和其他赋予执行权限。想要更改这些吗？请查看第 7 章的`chmod`。知道你的shell会处理尝试创建已存在目录的情况会让你感到不错。

```
$ mkdir test
mkdir: cannot create directory 'test': File exists
```

### 创建新目录及任何子目录

`mkdir -p`

如果你想在一个子目录内创建一个新的子目录，这似乎是一项繁琐的任务：创建第一个子目录，进入该目录，创建第二个子目录，进入它，最后创建第三个子目录。坦率地说，`mkdir`有一个棒的选项可以简化这个过程：`-p`（或`--parents`）。

```
$ ls -l
drwxr-xr-x 848 2005-10-19 11:36 src
drwxr-xr-x 632 2005-10-18 12:25 videos

$ cd pictures
$ ls -l
drwxr-xr-x 848 2005-10-19 11:36 src
drwxr-xr-x 632 2005-10-18 12:25 videos
drwxr-xr-x 2005-10-19 11:36 pictures

$ personal
$ mkdir -p personal/family
$ ls -l
drwxr-xr-x 848 2005-10-19 11:36 src
drwxr-xr-x 632 2005-10-18 12:25 videos
drwxr-xr-x 2005-10-19 11:36 pictures
drwxr-xr-x 2005-10-19 11:36 family

cd family
$ ls -l
drwxr-xr-x 848 2005-10-19 11:36 src
drwxr-xr-x 632 2005-10-18 12:25 videos
drwxr-xr-x 2005-10-19 11:36 pictures
drwxr-xr-x 2005-10-19 11:36 family
```

### 找出 mkdir 在做什么

`mkdir -v`

现在不是容易很多了吗？更简单的是使用`-v`选项（或`--verbose`），它会告诉你`mkdir`正在做的每一步，这样你就不需要实际去检查`mkdir`是否完成了工作。

```
$ mkdir -pv pictures/family
mkdir: created directory 'pictures'
mkdir: created directory 'pictures/family'
```

使用`-v`的优点之一是Linux用户不需要离开现场；这是查看执行效果的好方法。

### 复制文件

`cp`

复制文件是计算机用户（无论什么操作系统）经常做的事情之一。Linux中常用的命令之一是`cp`，它可以复制文件和目录。使用`cp`最简单的方法是输入命令，后面跟着你想复制的文件以及复制后的名称；将命令的结构想为`cp file-you-copying-from file-you-copying-to`。

```
$ pwd
/home/scott/libby
$ ls
libby.jpg
$ cp libby.jpg libby_bak.jpg
$ ls
libby_bak.jpg libby.jpg
```

这个示例很简单：文件被复制到了原文件所在的目录。你也可以将文件复制到另一个目录，甚至从你当前所在的目录复制文件到系统其他地方的目录。

```
$pwd
/home/scott
$ ls ~/libby
libby_bak.jpg libby.jpg
$ cp pix/libby_arrowrock.jpg libby/arrowrock.jpg
$ ls ~/libby
arrowrock.jpg libby_bak.jpg libby.jpg
```

在这个示例中使用了相同的文件名`libby.jpg`，这是的，因为文件被复制到了另一个目录。但在`cp`的第一个示例中，你必须使用新名称`libby_bak.jpg`而不是`libby.jpg`，因为你是将文件复制到同一个目录。

如果你想从另一个目录复制文件到你的工作目录（你当前所在的目录），只需使用`.`（记得你在本章前面学过它意味着“当前目录”，看到这个信息有多用了吗？）。当然，在使用`.`时你可以更改名称，它是原始文件名的快捷方式。

```
$pwd
/home/scott/libby
$ ls
libby_bak.jpg libby.jpg
$ cp pix/libby_arrowrock.jpg .
$ ls
arrowrock.jpg libby_bak.jpg libby.jpg
```

如果文件将存放在特定目录，你不需要为目标指定文件名，相反，你只需要提供目录名称。

```
$ ls
drwxr-xr-x 224 2005-10-20 12:34 libby
drwxr-xr-x 216 2005-09-29 23:17 music
drwxr-xr-x 1.6K 2005-10-16 12:34 pix
$ ls libby
arrowck.jpg libby.jpg
$ cp pix/libby_on_couch.jpg libby
$ ls libby
arrowck.jpg libby_on_couch.jpg
```

在在上一个示例中，你需要确保目录`libby`已经存在，`libby_on_couch.jpg`才能复制进去，否则你会在主目录下得到名为`libby`的文件。

### 使用通配符复制文件

```
cp *
```

现在是时候更懒一点了，即使用通配符一次性将多个文件复制到目录。如果你仔细命名文件，这可以是非常实用的东西，因为你可以精确地指定一组文件。

```
$pwd
/home/scott/libby
$ ls ~/pix
arrowck.jpg by_pool_03.jpg on_floor_03.jpg
by_pool_01.jpg on_floor_01.jpg on_floor_04.jpg
by_pool_02.jpg on_floor_02.jpg
$ ls
arrowck.jpg libby.jpg libby_on_couch.jpg
$ cp ~/pix/libby_on_pool_*.jpg
$ ls
arrowck.jpg by_pool_02.jpg on_couch.jpg
by_pool_01.jpg by_pool_03.jpg libby.jpg
```

你不局限于`*`通配符；相反，你可以使用匹配`[`和`]`之间任意字符的括号来更精确地识别你想复制的文件。如果你想用`cp`复制前三个`_floor`图片。

### 详细复制文件

```
cp -v
```

添加`-v`选项（或`--verbose`）会显示`cp`在完成其工作时的进度。

```
$ pwd
/home/scott/libby
$ ls ~/pix
arrowck.jpg by_pool_03.jpg on_floor_03.jpg
by_pool_01.jpg on_floor_01.jpg on_floor_04.jpg
by_pool_02.jpg on_floor_02.jpg
$ ls
arrowck.jpg libby_on_couch.jpg libby_on_couch.jpg
$ cp -v ~/pix/on_floor_01[1-3].jpg -> './.on_floor_01.jpg'
/home/scott/pix/on_floor_02.jpg -> './.on_floor_02.jpg'
/home/scott/pix/on_floor_03.jpg -> './.on_floor_03.jpg'
```

`arrowck.jpg libby_on_couch.jpg on_floor_02.jpg`

`libby.jpg on_floor_01.jpg on_floor_03.jpg`

`-v`选项很好地让你随时了解`cp`命令的进度。它做得非常出色，以至于你真的不需要运行最后那个`ls`命令了，因为`-v`选项向你确认了你想要的文件确实已经复制了。

### 停止复制重要文件

```
cp -i
```



上一个示例展示了关于 `cp` 的一个你需要知道的重要知识点。在“使用通配符复制文件”示例中，你将三张 `libby_on_floor` 图片复制到了 `libby` 目录中；在上一个示例中，你再次将这些相同的 `libby_on_floor` 复制到 `libby` 目录中。你复制了已经存在的文件，但 `cp` 并没有警告你，这就是 Linux 的工作方式：它并不知道你在做什么，所以除非你要求它这样做，否则它不会警告你正在覆盖文件。在用 `cp` 命令覆盖文件之前，你应该得到警告，请使用 `-i` 选项（或 `--interactive`）。如果你现在这次尝试使用 `-i` 选项复制相同的文件，你将得到一个不同的结果。

```
$pwd
/home/scott/libby
$ ls ~/pix
arrowck.jpg by_pool_03.jpg on_floor_03.jpg
by_pool_01.jpg on_floor_01.jpg on_floor_04.jpg
by_pool_02.jpg on_floor_02.jpg
$ ls
arrowck.jpg libby_on_couch.jpg on_floor_02.jpg
libby.jpg on_floor_01.jpg on_floor_03.jpg
$ cp -i ~/pix/on_floor_01[1-3].jpg
cp: overwrite './.on_floor_01.jpg'?
```

# 第一部分：入门

砰！`cp` 命令停了下来，询问你是否想要覆盖它正尝试覆盖的第一个文件 `libby_on_floor_01.jpg`。如果你想继续复制该文件，输入 `y`；否则，输入 `n`。如果你选择了 `n`，这并不意味着 `cp` 完全停止；你会被询问下一个文件，接下一个，依此类推。通过输入 `n` 来取消整个进程的唯一方法是按下 `Ctrl+c`。同样，没有办法提前对所有问题说是，如果你想将 1000 个文件复制到另外 1000 个同名文件，并且打算使用 `-i` 选项，请确保你有充足的时间坐在那里与 shell 交互，因为你会被询问 1000 次你是否真的想覆盖你的文件。

> **注意**
>
> 对于普通用户来说，`-i` 通常不是必要的。但对于 `root` 用户来说，它几乎是必须的，因为 `root` 用户可以轻松复制任何关键系统文件，导致灾难。出于如此，在 `root` 用户的 `.bashrc` 文件中创建一个别名是一个好主意，确保 `cp` 实际上是 `cp -i`。

```
alias cp='cp -i'
```

### 复制目录

#### `cp -R`

到目前为止你查看了复制文件，但有时你也想复制目录。不过，你不能直接输入 `cp 源目录 目标目录`，因为那样不会按你预期的方式工作；目录会复制，但它内部的文件不会。

```
$pwd
/home/scott
$ cp libby libby_bak
cp: omitting directory 'libby'
```

如果你想复制目录，需要包含 `-R` 选项（或 `--recursive`），你应该从 `ls` 命令中记得这个选项。添加 `-R` 意味着目录及其内容都会被复制。

```
$pwd
/home/scott
$ ls -l
drwxr-xr-x 328 2005-10-17 14:42 documents
drwxr-xr-x 240 2005-10-20 17:16 libby
$ cp -R libby_bak
$ ls -l
drwxr-xr-x 328 2005-10-17 14:42 documents
drwxr-xr-x 240 2005-10-20 17:16 libby
drwxr-xr-x 240 2005-10-20 17:17 libby_bak
```

### 作为目录复制文件

#### `cp -a`

你可能认为 `cp` 对备份文件很有用，这确实如此（尽管有更好的程序，我们会查看其中一个）。通过几行 `bash` 脚本，`cp` 可以是备份文件和目录的有效方法。在这种情况下最有用的选项是 `-a`（或 `--archive`），它等同于组合了多个选项：`-dp`（或 `--no-dereference recursive`）。另一种理解方式是 `-a` 确保 `cp` 不跟踪符号链接（这可能会导致复制膨胀），保留文件所有者和时间戳并递归处理子目录。

```
$pwd
/home/scott
$ ls
drwxr-xr-x 216 2005-10-21 11:31 libby
drwxr-xr-x 216 2005-09-29 23:17 music
$ ls -LR
libby:
total 312
-rw--r-- 73786 2005-10-20 12:12 arrowck.jpg
-rw--r-- 18034 2005-04-19 00:57 libby.jpg
-rw--r-- 198557 2005-04-19 00:57 on_couch.jpg
drwxr-xr-x 218 2005-10-21 11:31 on_floor
libby/on_floor:
total 764
-rw--r-- 218849 2005-10-20 16:11 on_floor_01.jpg
-rw--r-- 200024 2005-10-20 16:11 on_floor_02.jpg
-rw--r-- 358986 2005-10-20 16:11 on_floor_03.jpg
$ cp -a libby libby_bak
$ ls -l
drwxr-xr-x 216 2005-10-21 11:31 libby_bak/
drwxr-xr-x 216 2005-10-21 11:31 libby_bak/
drwxr-xr-x 216 2005-09-29 23:17 music
$ ls -LR
lib_bak:
total 312
-rw--r-- 73786 2005-10-20 12:12 arrowck.jpg
-rw--r-- 18034 2005-04-19 00:57 libby.jpg
-rw--r-- 198557 2005-04-19 00:57 on_couch.jpg
drwxr-xr-x 218 2005-10-21 11:31 on_floor
```

> **注意**
>
> 是的，你可能已经发现了，但让我确认一下：`Libby` 是我的狗，一只可爱的西西，最终以某种方式出现在我写的每个地方。想看她，请访问 `http://www.granneman.com/go/libby`。

### 移动并重命名文件

#### `mv`

复制文件。看起来足够简单，但移动文件呢？沿着移除命令中不必要元元的类似思路，我们有 `mv` 命令，`move` 的缩写。

你会很快发现，你为 `cp` 学的大多数选项与 `mv` 使用的选项非常相似。这应该不会感到惊讶；毕竟，`mv` 执行了 `cp -a`，然后移动它成功复制的文件。

简单来说，`mv` 将文件从你的一个位置移动到另一个位置。

```
$ pwd
/home/scott/libby
$ ls
libby_arrowck.jpg libby_bak.jpg libby.jpg libby_on_couch.jpg on_floor
$ ls ~/pix/dogs
libby_on_floor_01.jpg libby_on_floor_03.jpg
libby_on_floor_02.jpg libby_on_floor_04.jpg
$ mv ~/pix/dogs/libby_on_floor_04.jpg libby_on_floor_04.jpg
$ ls
libby_arrowck.jpg libby.jpg libby_on_floor_04.jpg
libby_bak.jpg libby_on_couch.jpg on_floor
$ ls ~/pix/dogs
libby_on_floor_01.jpg libby_on_floor_02.jpg libby_on_floor_03.jpg
```

就像你用 `cp` 时做的一样，如果你不想输入文件名，可以使用点来表示当前目录。

```
$pwd
/home/scott/libby
$ ls
arrowck.jpg libby_bak.jpg libby.jpg libby_on_couch.jpg on_floor
$ ls ~/pix/dogs
libby_on_floor_01.jpg libby_on_floor_03.jpg
libby_on_floor_02.jpg libby_on_floor_04.jpg
$ mv ~/pix/dogs/libby_on_floor_04.jpg .
$ ls
arrowck.jpg libby_bak.jpg libby.jpg libby_on_couch.jpg on_floor
libby_on_floor_04.jpg
$ ls ~/pix/dogs
libby_on_floor_01.jpg libby_on_floor_02.jpg libby_on_floor_03.jpg
```

如果你正在将一个文件移动到目录并想保留相同的文件名，你只需要指定目录。文件名保持不变。



```bash
$ pwd
/home/scott/libby
$ ls
arrowck.jpg libby_bak.jpg libby.jpg libby_on_couch.jpg on_floor_04.jpg
libby.jpg on_floor
$ ls on_floor
on_floor_01.jpg on_floor_03.jpg
on_floor_02.jpg on_floor_04.jpg
$ mv on_floor_04.jpg on_floor
$ ls
arrowck.jpg libby_bak.jpg libby.jpg libby_on_couch.jpg on_floor_04.jpg
libby.jpg on_floor
$ ls on_floor
on_floor_01.jpg on_floor_03.jpg
on_floor_02.jpg on_floor_04.jpg
```

为了在视觉上确认 `on_floor` 是一个目录，一个好主意是在移动文件的目录末尾使用 `/`，如下所示：`mv libby_on_floor_04.jpg on_floor/`。如果 `on_floor` 不是目录，你的 `mv` 将无法工作，防止你意外覆盖文件。

### 注意

`cp` 和 `mv` 命令使用许多相同的选项，这些选项在每个命令中的工作方式相同。例如，`-v` 用于详细复制和移动，而 `-i` 用于交互式复制和移动。

# 第一部分：入门

### 注意事项

你需要了解一个关于 `mv` 的非常重要但遗憾的是容易被忽略的细节。如果你正在移动一个指向目录的软链接，你需要对你输入的内容极度小心。假设你在主目录下有一个名为 `dogs` 的软链接，它指向 `/home/scott/pictures/dogs`，而你只想将该链接移动到 `/home/scott/libby` 子目录下。这个命令只移动软链接：

```bash
$ mv dogs ~/libby
```

然而，这个命令会移动软链接所指向的目录：

```bash
$ mv dogs/ ~/libby
```

区别在哪里？软链接末尾有一个简单的正斜杠。没有正斜杠，你移动的就是软链接本身，且仅移动链接本身；包含正斜杠，你移动的就是软链接设计用于指向的目录，而不是软链接本身。小心点！

### 删除文件

`rm` 命令（`remove` 的缩写）用于删除文件。它是真的、真的地把它们删除了。它们彻底消失了。Linux 命令行中没有垃圾箱或回收站。你正在走钢丝，伙计，如果你掉下去，就粉身碎骨了！

好了，这有点极端。Shell 确实缺少撤销（`undo`）命令，但删除文件并不意味着你就完全完蛋了。如果你在意识到错误的第二秒立即停止操作机器，操作系统还没有覆盖掉被删除的文件扇区，你就可以成功使用一些复杂的备恢复软件，是的，是可以恢复文件的。但毕竟，你会在整个过程中不断咒骂。从一开始就小心一点更好。

### 提示

许多人尝试过为 `rm` 提供某种安全保障，范围从将 `rm` 映射或替换为命令 `trash`（[www.comwt.com/open_source/projects/trashcan/](http://www.comwt.com/open_source/projects/trashcan/)），到在 shell 中添加一个垃圾桶（[http://pages.stern.nyu.edu/~marriaga/software/libtrash/](http://pages.stern.nyu.edu/~marriaga/software/libtrash/)），再到创建一个新命令 `trash, trash, trash` 来替换 `rm`（[www.unimelb.edu.au/~jltooker/shell.html#trash](http://www.unimelb.edu.au/~jltooker/shell.html#trash)）。

另一方面，如果你想确保没有人能恢复你删除的文件，即使是为某些阴暗的美国政府机构工作，也请使用 `shred` 命令代替 `rm`。`shred` 命令会覆盖文件 25 次，使其无法被重建。但在在使用 `shred` 之前，请阅读它的帮助页（`man` page），因为它的成功率高度取决于你正在使用的文件系统类型。

使用 `rm` 非常简单。有些人会说太简单了。

```bash
$ pwd
/home/scott/libby/by_pool/lieberman_pool
$ ls
pool_01.jpg pool_03.jpg
pool_01.jpg_bak pool_03.jpg_bak
$ rm pool_01.jpg_bak
$ ls
pool_01.jpg pool_03.jpg pool_03.jpg_bak
```

### 使用通配符一次删除多个文件

像 `*` 这样的通配符可以帮助一键删除多个文件。

```bash
$ pwd
/home/scott/libby/by_pool/lieberman_pool
$ ls
pool_01.jpg pool_03.jpg
pool_01.jpg_bak pool_03.jpg_bak
$ rm *bak
$ ls
pool_01.jpg pool_03.jpg
```

### 注意事项

在使用通配符删除文件时要非常、非常、非常小心，否则你删除的文件可能比预期的要得多！一个经典的例子是输入 `rm *txt` 而不是 `rm * txt`（那个多出的空格？）。结果不是删除所有的文本文件，星号意味着所有文件都被删除了，然后 `rm` 尝试删除一个名为 `txt` 的文件。哎！

### 详细模式删除文件

如果你想在 `rm` 执行时看到它的操作，请使用 `-v`（或 `--verbose`）选项。

```bash
$ pwd
/home/scott/libby/by_pool/lieberman_pool
$ ls
pool_01.jpg pool_03.jpg
pool_01.jpg_bak pool_03.jpg_bak
```

```bash
$ rm -v *bak
removed 'pool_01.jpg_bak'
removed 'pool_03.jpg_bak'
$ ls
pool_01.jpg pool_03.jpg
```

### 防止自己删除关键文件

`-i` 选项（或 `--interactive`）提供了一种安全网。它会在删除每个文件之前询问你。当你以 `root` 身份运行时运行时，这是一个非常实用的功能！

```bash
$ pwd
/home/scott/libby/by_pool/lieberman_pool
$ ls
pool_01.jpg pool_03.jpg
pool_01.jpg_bak pool_03.jpg_bak
$ rm -i *bak
rm: remove regular file 'pool_01.jpg_bak'? y
rm: remove regular file 'pool_03.jpg_bak'? y
$ ls
pool_01.jpg pool_03.jpg
```

当 `rm` 询问你该做什么时，输入 `y` 表示同意删除文件，输入 `n` 表示跳过该文件。

### 删除空目录

删除文件并不难，但目录呢？

```bash
$ pwd
/home/scott/libby/by_pool
$ ls
pool_01.jpg pool_03.jpg
pool_01.jpg_bak pool_03.jpg_bak
$ ls pool_bak
pool_01.jpg pool_03.jpg
pool_01.jpg_bak pool_03.jpg_bak
$ rm pool_bak
rm: cannot remove 'pool_bak': Is a directory
```

在观察了一会儿后，你可能会发现 `rmdir` 命令，它是专门为删除目录而设计的。试一下。

```bash
$ rmdir pool_bak
rmdir: 'pool_bak/': Directory not empty
```

该死！这也不行。`rmdir` 命令只能删除空目录。在这种情况下，`pool_bak` 文件夹包含项目，所以先删除内容再使用 `rmdir` 并不太难。但如果你想删除一个包含子目录的目录，你将陷入无尽的循环。关于这一点，请看下一节。

### 删除非空文件和目录

使用 `-R`（或 `--recursive`）和 `-f`（或 `--force`）选项。`-R` 会递归进入目录，而 `-f` 会强制忽略不存在的文件。

```bash
$ pwd
/home/scott/libby/by_pool
$ ls
pool_01.jpg pool_03.jpg
pool_01.jpg_bak pool_03.jpg_bak
$ rm -rf pool_bak
$ ls
```

# 第一部分：入门

```bash
$ ls
-cousin_roy.jpg cousin_beth.jpg
$ rm ./-cousin_roy.jpg
$ ls
cousin_beth.jpg
```

这恰恰说明了 Linux 用户的奇思妙想是非常深厚的。此外，尽量不要在文件名的开头使用连字符！

### 变成另一个用户



# 第一部分：入门

`su` 命令（全代表 switch user，即切换用户，而不是大众想象的 super user，即超级用户）可以允许一个用户临时扮演另一个用户，但它最常用于你想在 shell 中快速变成 root，运行一个命令，然后回到你正常的非 root 用户身份。可以把它想象成克拉克·肯特（Clark Kent）变身为他的超人职责，惩治一些不公，然后回到他非超能力的本我。

## 变成另一个用户

调用 `su` 并不困难。只需输入 `su`，然后输入你想要切换的用户身份即可。

```bash
$ ls
/home/scott/libby
$ whoami
scott
$ su gromit
Password:
$ whoami
gromit
$ ls
/home/scott/libby
```

那个示例中有一个新命令，它并不算是最广泛使用的：`whoami`。它从 shell 的角度告诉你是你是谁。在这里，你使用它来验证 `su` 是否按你预期的方式工作。

### 变成另一个用户，并携带他的环境变量

`su -l`

只有当你知道用户的密码时，`su` 命令才能起作用。没有密码，就没有转换。如果生效，它将切换到用户在 `/etc/passwd` 文件中指定的 shell：例如 `sh`、`tcsh`、`bash`。大多数 Linux 使用默认的 `bash`，所以你可能在那里不会看到任何区别。注意在上一个示例，当你切换用户时并没有更改目录。从本质上说，你变成了 gromit，但你仍然在使用 scott 的环境变量。如果你找到了超人的制服并像超人一样穿上它（呵呵，得吧？），你将不会拥有他的任何能力。

修复该问题的方法是使用 `-l` 选项（或 `--login`）。

```bash
$ ls
/home/scott/libby
$ whoami
scott
$ su -l gromit
Password:
$ whoami
gromit
$ ls
/home/scott/gromit
```

看起来与“变成另一个用户”的示例大部分相同，但背后的情况非常不同。你现在处于 gromit 的主目录，这一事实应该说明发生了某些变化。`-l` 选项告诉 `su` 使用登录 shell（login shell），尽管 gromit 实际上已经登录了这台机器。你现在名义上是 gromit，但你正在使用 gromit 的环境变量，并且你处于 gromit 的主目录中（这是 gromit 第一次登录这台机器时所在的地方）。这就像快速穿上超人的制服就让你拥有了一跳跃过高大建筑的能力！

### 变成 root

`su`

在本章的开头，已经提到大多数情况下 `su` 被用来变成 root。你可以使用 `su root`，或者更好一点，使用 `su -l root`，但有一种更快的方法。

```bash
$ whoami
scott
$ su
Password:
$ whoami
root
```

### 变成 root，并携带它的环境变量

`su -`

单独输入 `su` 等同于在名称和权力上输入 `su root`，但仅此而已。在背后，你的非 root 环境变量仍然有效，如下所示：

```bash
$ ls
/home/scott/libby
$ whoami
scott
$ su
Password:
```

```bash
$ whoami
root
$ ls
/home/scott/libby
```

当你使用 `su -` 时，你不仅变成了 root，还使用了 root 的环境变量。

```bash
$ ls
/home/scott/libby
$ whoami
scott
$ su -
Password:
$ whoami
root
$ ls
/root
```

现在好多了！在 `su` 后面添加 `-` 等同于 `su -l root`，但需要的输入更少。你在名称、权力和环境上都是 root，这意味着你是完全的 root。对于计算机来说，root 能做的任何事情，你都能做。尽情享受你的超能力吧，记住能力越大，责任越大，你知道它是如何结束的。

### 总结

如果这是法学院，你将在这一章中学习到轻罪、侵权行为和重罪。如果这是一门硬件维修课，学习过的将是 RAM、硬盘和主板。由于这是一本关于 Linux 的书，你已经检查了 Linux 用户有效使用命令行需要知道的常用命令：`ls`、`pwd`、`cd`、`touch`、`mkdir`、`cp`、`mv`、`rm` 和 `su`。`rmdir` 和 `whoami` 作为额外补充。掌握了这些关键命令后，你准备好继续学习如何学习命令了。为什么？你还没有结束。

## 第3章：学习命令

在第 2 章“基础”中，你开始学习一些基础系统命令。你涵盖了很多内容，但尽管如此，仍留下了很多。命令是一个极其丰富、强大的工具，其选项比第 2 章提供的多得多。所以，你能学习更多关于命令或其他让你感兴趣的内容吗？如果你不知道它们的名称，又该如何发现它们呢？这就是本章大显身场的地方。在这里你将发现如何学习你已经熟悉的命令、你不知道的命令，甚至是你完全不知道的命令！

# 第一部分：入门

### 通过功能查找命令

`man -k`

只需一点训练，你就会发现自己可以在帮助页面之间移动并找到你需要的……假设你知道该读哪一个。如果你知道关于命令的一些信息，但不知道实际的名称？尝试使用 `-k` 选项（或 `--apropos`）搜索描述你想要发现的命令类型的单词或短语。你将获得所有名称或摘要匹配你的搜索词的命令列表。

```bash
$ man list
No manual entry for list
$ man -k list
last: (2) - show last logged in as users
ls (1) - list directory contents
lsh (1) - list devices and their properties
lshw (1) - list hardware
lsof (8) - list open files
```

使用 `-k` 选项要小心，因为它可能会产生长列表，你可能会错过正在寻找的内容。如果你觉得不同的搜索词可能帮助你找到需要的命令，尽管去尝试。你会得到如下 man 结果：

```bash
$ man ls
LS(1)
NAME The name of the command
NOPSIS [OPTIONS] [FILE]
DESCRIPTION A longer overview of the command

OPTIONS The detailed explanations of the command

FILES used by

AUTHOR Who wrote the command, with contact information

BUGS Known bugs and how to report new ones

COPYRIGHT Information about copyright

SEE ALSO Related commands
```

在 man 页面中移动并不困难。逐行向下移动使用向下箭头键；逐行向上移动使用向上箭头键。向下翻页使用空格键或 `f`（for forward）；向上翻页使用 `b`（for backward）。当你到达 man 页面末尾时，man 会退出并回到 shell；然而，它在末尾不会退出，这种情况下你应该按 `q`。事实上，你可以随时退出退出程序。

在 man 页面中查找特定项目，有时你需要进行搜索。在 man 页面打开后输入 `/`，紧跟你的搜索词，然后按 Enter。如果存在，它将跳转到那里；跳转到下一个出现处，再次按 Enter（或 `n`），并继续按 Enter（或 `n`）向下跳转到每个位置；后退按 Shift+.

### 根据名称快速查找命令的作用

`man -f`

如果你知道一个命令的名字但不知道它是做什么的，有一种快速简单的方法可以查看，无需实际打开该命令的 man 页（帮助页）。使用 `-f` 选项（或 `--whatis`），就会显示命令的概览。

```bash
$ man -f ls
ls (1)           - list directory contents
```

> **提示**
> 是的，`-f` 选项（也称为 `--whatis`）与 `whatis` 命令完全一样，我们将在章稍后的部分详细介绍。

### 重建 man 的命令数据库

`man -u`

有时你会尝试使用 `man` 查找某个命令的信息，但 `man` 报告该命令没有页面。在放弃之前，尝试使用 `-u` 选项（或 `--update`），这将强制 `man` 重新构建它使用的命令数据库和 man 页。如果你认为某些地方不正常，这通常是一个很好的第一步。

```bash
$ man ls
No manual entry for ls

$ man -u ls
LS(1)           User Commands LS(1)

NAME

  ls - list directory contents

SYNOPSIS

ls [OPTION]... [FILE]...

[Listing condensed due to length]
```



### 读取命令的特定 man 页

`man [1-8]`

你可能在上一个列表中注意到，`man` 页的第一行引用了 `ls (1)`，而在早些你使用 `-k` 选项时，所有命令名称后面都跟着括号里的数字。大部分是 1，但其中一个 `lsof` 是 8。那么这些数字代表什么呢？

答案是 `man` 页被分为不同的章节，编号从 1 到 8，具体划分如下（如果你不认识这些示例请担心，因为很多非常晦奥且专业）：

- 1. 通用命令。例如 `cd`、`chmod`、`mkdir` 和 `passwd`。
- 2. 内核调用的低级系统调用。例如 `intro` 和 `chmod`。
- 3. C 库函数。例如 `beep`、`HTML::Parser` 和 `Mail::Internet`。
- 4. 特殊文件，例如在 `/dev` 中的的设备。例如 `console`、`lp` 和 `mouse`。
- 5. 文件格式和约定。例如 `apt.conf`、`dpkg.cfg`、`hosts` 和 `passwd`。
- 6. 游戏。例如 `atlantic_bouncingcow`、`kmahjongg` 和 `rubik`。
- 7. 杂项，包括宏包。例如 `ascii`、`base` 和 `utf-8`。
- 8. root 调用的系统管理命令。例如 `.` 和 `shutdown`。

我们在书中查找的几乎每个命令都属于第 1 部分，这并不意外，因为我们关注的是 Linux 系统的通用用法。但请注意命令可能属于多个章节：例如，`chmod` 同时属于第 1 和第 2 部分，`passwd` 可以在第 1 和 5 部分找到。默认情况下，如果你在 shell 中输入 `passwd`，`man` 默认显示数字较小的章节，因此你会看到 `passwd` 的第 1 节 `man` 页，如果你想学习 `passwd` 文件本身，这并没有什么帮助。要查看文件 `passwd` 的 `man` 页，请在命令后加上你想检查的数据章节数字。

```bash
$ man passwd

PASSWD (1)

NAME

passwd change user password

SYNOPSIS

passwd [-f] [-r] name

passwd [-q] [-R] group

passwd [-max] [-n min] [-w warn] [-i inact]

login [-l|u|-d|-S|-e] login

DESCRIPTION

passwd changes passwords for user and group accounts. A normal user...

[Listing condensed to length]

$ man passwd (5)

NAME

passwd - The password file

DESCRIPTION

passwd contains various pieces of information for each user account.

[Listing condensed to length]
```

## 第一部分：入门

### 打印 man 页

`-t`

虽然使用终端程序查看 `man` 页非常简单，但有时有必要打印 `man` 页以便于阅读和引用。然而，打印 `man` 页并不是一个一步到位的过程，完成这一特定章节的命令实际上使用了稍后会涵盖的原理。但如果你想打印 `man` 页，这就是操作方法。只需相信在阅读完后续章节后，你将更充分地理解这些命令的含义。

假设你有一个连接到系统的、标识为 `hp_laserjet` 的打印机。你想直接打印一份关于 `ls` 命令的 `man` 页，因此使用 `-t` 选项（或 `--troff`），然后将输出通过给 `lpr` 命令，用 `-P` 选项指定你的打印机。

```bash
$ man -t ls | lpr -P hp_laserjet
```

**注意**

你将在第 4 章“构建模块”中学习管道符号 (`|`) 以及第 6 章“管理打印任务”中学习 `lpr`。

过一会儿（取决于你的电脑和打印机的速度），`hp_laserjet` 应该开始输出 `ls` 的 `man` 页。然而，你可能不想实际打印这些页面。也许为 `ls` 命令的 `man` 页创建 PDF 就足够了。同样，现在执行这些操作命令看起来有些晦奥，但很快就会变得容易。

再次使用 `-t` 选项，但这次你将输出发送到一个以 `ls` 命令命名的 PostScript 文件。如果过程成功完成，你使用 `ps2pdf` 命令将 PostScript 文件转换为 PDF。

```bash
$ man -t ls > ls.ps
$ ps2pdf ls.ps ls.pdf
```

### 导航 Info 页面

如果你想减少按键次数，可以使用 `n`（代表 next）移动到同一级别的下一个节点。如果你正在阅读一个带有子模块的节点并按下 `n`，你将跳过这些子模块，移动到你当前阅读的节点的下一个部分。然而，如果你正在阅读一个子模块并按下 `n`，你将跳转到子网络。如果 `n` 将你带到当前层级的下一个节点，`p` 则会将你带到上一个节点（`p` 代表 previous，懂吧？），同样在同一级别。

如果你想向前移动到某个节点或子模块，请使用 `[` 或右方括号键。如果你正在阅读一个节点并按下 `[`，将跳转到该节点的第一个节点。否则，你将移动到该节点的下一个节点。以同样的方式向后移动，请使用 `{` 或左方括号键。

如果你想向上移动到当前阅读的节点的父节点，请使用 `u`（代表 up）键。但注意，这很容易跳过你正在阅读的 Info 命令的主页，该页面被称为“目录节点”（Directory node），它是通往所有 Info 节点的根节点（到达目录节点的另一种方法是随时输入 `d`，代表 directory）。

目录节点是一个特别大的示例，展示了你在 Info 中随处可见的一种页面类型：菜单页（Menu page），它列出了所有节点或节点组。如果你发现自己处于菜单页面，可以快速导航到你想要跳转的节点中列出的子节点之一。例如，当你在命令行输入 `info info` 时看到的页面：

```
[View full]:File.info, Node: Top, Next: Getting Started, Up: (dir)
```

Info: 简介

GNU 项目以“Info 格式”发布其大部分在线手册，你使用“Info 阅读器”来阅读它们。你现在可能正在使用 Info 阅读器阅读这些。

- 菜单 (Menu)
- 入门指南：如何使用 Info 阅读器入门。
- 导出 Info：面向专家的 Info 命令。
- 创建 Info 文件：如何制作你自己的 Info 文件。
- 索引：主题、命令和变量的索引。

要跳转到 Info，你可以输入 `m`，这将从 Exp 开始。此时，你可以完成输入 Info，或者按下 `Tab` 键，Info 会自动填充与你输入的字符匹配的菜单名称。如果 Info 报错，说明你输入了错误字符，或者有多个菜单选项与你输入的字符匹配。修正拼写错误，或输入更多字符，直到 Info 能够明确识别你感兴趣的是哪一个菜单选项。如果你意识到现在不想进入菜单，按下 `Ctrl+c` 取消命令，并回到你之前找到的节点。

或者，你也可以使用向上或向下箭头键将光标置于你想要的菜单选项上，然后按回车键。两种方法均有效。

如果你没有导航到 Info 页面并想要搜索，可以通过两种方式实现：通过搜索所有节点的标题来查找特定命令的 Info 页面，或者搜索与特定命令相关的节点实际文本。这种搜索使用节点索引（针对 Info），接着输入搜索词，然后按回车。如果你的词出现在某个节点的标题中，你将跳转到那里。如果你想重复搜索并进入下一个结果，请按逗号键。

### 搜索 Info 内容

如果你想搜索文本而不是标题，请输入 `s`（代表 search），接着输入你的搜索词或短语，然后按回车。要重复此操作，直接搜索 `s` 后紧接着按回车。这不像搜索词汇时按逗号键那么简单，但确实有效。

如果你在任何时候进入 Info 内部并需要帮助，只需按下 `/` 键，窗口下半部分将显示 Info 的所有选项。使用已学会的键在该部分上下移动。当你想退出帮助时，按下 `l`。

最后，可能最重要的点是，要完全退出 Info，只需按下 `q`（代表 quit），这将带你回到 shell 界面。哇！

### 定位命令执行文件、源文件和帮助页的路径

#### whereis

`whereis` 命令执行着极其实用的功能：它告诉你命令的可执行程序、源文件（如果存在）及其帮助页（`man` pages）的路径。例如，对于 KOOffice 套件中的文字处理器 Kword，你可能会得到以下结果（假设二进制文件、源码和帮助页都已安装）：

```
$View full width$ whereis
kword: /usr/src/koffice-1.4.1/kword /usr/bin/kword /usr/bin/X11/kword /usr/share/man/man1/kword.gz
```



`whereis` 命令报告了源文件的位置：`/usr/src/kword-1.4.1/kword` `/usr/bin/kword` `/usr/bin/X11`。Kword 在这台机器上找到了两个，这有点不寻常但也很奇怪。最后，你发现帮助页位于：`/usr/share/man/man1/kword.gz`。有了这些信息，你现在可以验证程序确实已安装在这台电脑上，并且知道如何运行它。

如果你只想搜索二进制文件，请使用 `-b` 选项。

```
$ whereis
kword: /usr/src/koffice-1.4.1/kword /usr/bin/kword /usr/bin/X11/kword /usr/share/man/man1/kword.gz
```

`whereis` 命令报告了源文件的位置：`/usr/src/kword-1.4.1/kword` `/usr/bin/kword` `/usr/bin/X11`。Kword 在这台机器上找到了两个，这有点不寻常但也很奇怪。最后，你发现帮助页位于：`/usr/share/man/man1/kword.gz`。有了这些信息，你现在可以验证程序确实已安装在这台电脑上，并且知道如何运行它。

如果你只想搜索二进制文件，请使用 `-b` 选项。

```
$ whereis
kword: /usr/src/koffice-1.4.1/kword /usr/bin/kword /usr/bin/X11/kword /usr/share/man/man1/kword.gz
```

如果你只想搜索帮助页，请使用 `-m` 选项。

```
$ whereis
kword: /usr/src/koffice-1.4.1/kword /usr/bin/kword /usr/bin/X11/kword /usr/share/man/man1/kword.gz
```

如果你只想搜索源文件，请使用 `-s` 选项。

```
$ whereis
kword: /usr/src/koffice-1.4.1/kword /usr/bin/kword /usr/bin/X11/kword /usr/share/man/man1/kword.gz
```

这一次，`last` 没有出现，是因为你只想要精确词汇列表的结果，而不是列出。事实上，`list` 命令的结果列表从不使用 `-e` 选项的 80 个减少到了使用 `-e` 的 55 个，这使得你更容易精确地针对你的命令搜索，并准确地找到你需要的命令。

### 找出哪个版本的命令将运行

`which`

回想一下 `which` 命令，以及当你对 KWord 使用 `-b` 选项（仅显示二进制文件）时发生了什么。

```
$ which kword
kword: /usr/bin/kword /usr/bin/X11/kword
```

KWord 的可执行文件位于两个地方。但哪一个会先运行？你可以通过运行 `which` 命令来判断。

```
$ which kword
/usr/bin/kword
```

`which` 命令可以告诉你如果你只输入命令名称，将运行的是哪个版本的命令。换句话说，如果你输入 `kword` 然后按回车，你的 shell 将执行位于 `/usr/bin/X11` 内部的那个；你必须使用 `cd` 命令切换目录，然后输入 `./kword`，或者使用命令的绝对路径并输入 `/usr/bin/X11/kword`。

`which` 命令也是检查命令是否存在于你系统的快速方法。如果命令存在于你的系统并在你的 `PATH` 中，它会告诉你在哪里可以找到它；如果命令不存在，你会回到命令行且一无所获。

```
$ arglebargle
$
```

如果你想找到命令的所有位置（就像你使用 `which -b` 一样），请尝试 `-a`（代表 all）选项。

```
$ which -a kword
/usr/bin/kword
/usr/bin/X11/kword
```

### 结论

本章的标题是“学习命令”，我们涵盖了这些内容。现在，你已经看到有很多方法可以查看命令的选项。最重要的工具是 `man` 和 `info`，它们拥有海量的数据和对你 Linux 计算机上找到的几乎所有命令的描述。请记住，虽然 `whatis`、`apropos` 和 `which` 都有自己的用处，特别是当你的目标是避免在 `man` 和 `info` 有时令人崩溃的冗长描述中挣扎时（这些描述是可以理解的，但往往是不可能的），你只需要卷起袖子开始运行页面即可。把它想象成西兰花：你可能不喜欢它，但它对你有好处。

确实，本章中的许多命令在某种程度上是重叠的。例如，`-k` 等于 `apropos`，`-f` 就像 `whatis`，而 `-b` 在功能上等同于 `which -a`。在特定情况下使用哪一个取决于你。然而，了解这些各种相似之处仍然是一个好主意，这样你就能阅读他人提供的脚本或指令，并准确地理解正在发生什么。Linux 的核心在于多样化和选择，即使在在 shell 中运行命令这些看似微不足道的事情上也是如此。

## 第 4 章：构建块

当你年轻时，你先学习，稍后又学习如何使用 `+`、`-` 和 `=` 等符号将它们结合起来并进行操作。到目前为止，你已经学习了命令，但每个命令都是一次运行的。然而，命令实际上可以使用更复杂、更有趣的方式来构建，例如使用 `|`、`>` 和 `<` 等各种符号。本章将介绍这些构建块，让你能够利用你已经学到的命令以及将在后续章节中更详细研究的命令来完成有用的事情。

### 顺序运行多个命令

`;`

如果你有几个命令需要运行，但某些命令将花费很长时间，而你又不想守着你的电脑怎么办？例如，如果你在一个压缩归档文件中大量的 John Coltrane MP3 文件，并想要解压它们、将它们放入一个新的子目录，然后删除压缩文件？通常情况下，你必须一个一个地运行它们，如下所示：

**注意**
为了节省空间，我从长列表中删除了所有者和组。

```
$ ls -l /home/music/music
-rw-r--r-- 1437931 2005-11-07 17:19 JohnColtrane.zip
$ unzip /home/music/music/JohnColtrane.zip
$ mkdir -p /home/music/music/coltrane
$ mv /home/music/music/JohnColtrane*.mp3 /home/music/music/coltrane/
$ rm /home/music/music/coltrane.zip
```

`JohnColtrane.zip` 是一个 4GB 的文件，即使在快速机器上，解压那个巨兽也需要一些时间，你可能有比坐着等更有事情要做。命令堆叠来救你了！

命令堆叠将你想运行的所有命令放在 shell 的同一行中，每个命令之间用分号 (`;`) 隔开。每个命令按顺序执行，并且每个命令在下一个命令运行之前都会成功或失败终止。这很容易做到，你可以轻松节省一些时间。使用命令堆叠，之前的系列命令看起来如下：

```
$ ls -l /home/scott/music
-rw-r--r-- 1437931 2005-11-07 17:19 JohnColtrane.zip
$ unzip /home/scott/music/JohnColtrane.zip ; mkdir -p /home/scott/music/coltrane/ mv /home/scott/music/JohnColtrane*.mp3 /home/scott/music/coltrane/ rm /home/scott/music/coltrane.zip
```

当然，你也可以使用这种方法在命令运行时引入短的延迟。如果你想对显示器上的所有内容截图，只需运行以下命令（这假设你安装了 ImageMagick，几乎所有的 Linux 发行版都安装了）：

```
$ sleep 3 ; import window.tif
```



`sleep` 命令等待三秒，然后使用 `import` 截图。延迟给了你有时间最小化终端应用程序，并将你希望出现的任何窗口带到前台。`;` 很容易在逻辑上分离命令，从而最大限度地利用它们。

**警告**
在使用命令堆叠时要非常小心，特别是在删除或移动文件时！确保你输入的内容是你想要的，因为命令会一个接一个地运行，你可能会导致意想不到的结果。

# 第一部分：入门

如果你使用了 `|` 而不是 `;` 且 `ps2pdf` 执行失败了，PostScript 文件仍然会落空空，导致你不得不从头开始。

现在你确信 `&&` 通常是更好的选择了？？如果没有删除文件的风险，使用 `;` 可能是没问题的；但如果你的命令中包含涉及 `rm` 或其他无法恢复的操作，你最好使用 `&&`。

### 仅在在上一个命令失败时运行命令

`&&` 只有在在上一个命令成功完成时，才会按顺序执行每个命令。`||` 则相反：如果第一个命令失败（从技术上讲，它返回一个非 0 的退出状态），那么它就会执行第二个命令。把它想象成“要么……或者”运行：执行第一个命令，要么执行第二个。

`||` 通常用于在进程停止时提醒管理员。例如，为了确保某个命令正在运行，管理员可能会使用 `ping` 命令不断对其查询（你将在第 14 章“连接性”中了解到 `ping`），如果 `ping` 失败，就会向管理员发送一封电子邮件通知他。

```
ping -c 1 -w 15 -n 72.14.203.104 || echo "Server down" | mail -s 'Server down' admin@google.com
```

**注意**

想知道 `|| |` 是什么吗？请查看本章的“将一个命令的输出作为另一个命令的输入”部分以了解它以及如何使用它。

经过思考，你会开始发现许多 `||` 可以帮助你的地方。它是一个强大的工具，确实非常有用。

### 将一个命令的输出插到到另一个命令中

命令替换获取命令的输出，并将其插入另一个命令中，就像你直接输入了该输出一样。将要产生被插入输出的初始命令括在 `$( ( )` 之中。一个示例会让这变得清晰得多。

假设你刚参加完家庭晚餐回家，将数码相机连接到你的 Linux 机器，提取出新照片，现在你想把它们放在一个命名为今天日期的文件夹中。

```
$ pwd
/home/scott/photos/family

$ ls -lF

2005-11-01/

2005-11-09/

2005-11-15/

$ date "+%Y-%m-%d"

2005-11-24

$ mkdir $(date "+%Y-%m-%d")

$ ls -lF

2005-11-01/

2005-11-09/

2005-11-15/

2005-11-24/
```

在这个示例中，`date "+%Y-%m-%d"` 首先运行，然后命令的输出 `2005-11-24` 被 `mkdir` 用作新目录的名称。这是非常强大的功能，当你查看别人编写的 Shell 脚本（你可以在 Web 上随处找到它们）时，你会发现命令替换随处可见。

**注意**

在过去，你应该用反引号（键盘左上角的 `` ` `` 字符）将初始命令括起来。然而，现在建议你使用本节中使用的字符：`$( ( )`。

### 理解输入/输出流

为了利用本章中的信息，你需要理解 Linux Shell 有三个输入/输出流：标准输入、标准输出和标准错误。每个流都有一个文件描述符（或数字标识符）、一个常用缩写和一个默认值。

让我们使用常用命令 `ls` 来观察这三个流。当你从键盘上输入 `ls` 时，使用的是 `stdin`。在输入 `ls` 并按回车后，文件和文件夹的列表以 `stdout` 显示。如果你尝试对一个不存在的文件夹运行 `ls`，错误信息显示在终端上，这是 `stderr` 的功。。表4.1 可以帮助记住这三个流。

| 表 4.1 三种输入/输出流 | 常用缩写 | 典型默认值 |
| :--- | :--- | :--- |
| 文件描述符 (标识符) | | |
| 0 | 标准输入 | 键盘 |
| 1 | 标准输出 | 终端 |
| 2 | 标准错误 | 终端 |

在本章中，我们将学习如何重定向输入和输出。与其让输出显示在终端上，不如让程序从文件中获取它。

# 将一个命令的输出作为另一个命令的输入

有一个格言：Unix 是由松散连接的小组件组成的。没有什么比管道（pipes）的概念更能体现这一原则了。管道是键盘上的 `|` 符号，放在两个命令之间时，它获取第一个命令的输出并作为第二个命令的输入。换句话说，`|` 重定向 `stdout` 将其发送到下一个命令的 `stdin`。

这里有一个简单的示例有助于理解这个概念。你已经了解 `ls`，你将在第 5 章“查看文件”中了解到 `less` 命令。现在知道 `less` 允许分页查看文本文件。如果你对一个不存在的文件夹运行 `ls`，错误信息显示在终端上，这是 `stderr` 的功。

```
1958_Peckin'_Time/
1960_Roll_Cell/
1960_Soul_Station/
1961_Workout/
1963_No_Room_For_Squares/
```

如果你决定不再喜欢或需要 `noclobber`（覆盖保护），你可以再次关闭它：

```
$ set +o noclobber
```

要永久开启 `noclobber`，你需要向你的 `.bashrc` 文件中添加 `set -o noclobber`。

### 将命令的输出追加到文件

```
>>
```

正如你之前学到的，`>` 字符将输出从标准输出（stdout）重定向到文件。例如，你可以轻松地将 `date` 命令的输出重到一个文件中：

```
$ date

Mon Nov 21 21:33:58 CST 2005

$ date > hank_mobley.txt

$ cat hank_mobley.txt

Mon Nov 21 21:33:58 CST 2005
```

记住，`>` 在文件不存在时会创建一个新文件，并覆盖已存在的文件。如果你使用 `>>` 而不是 `>`，你的输出将追加到文件的末尾（如果文件不存在，则会创建它）。

```
$ cat hank_mobley.txt

Mon Nov 21 21:33:58 CST 2005

$ ls -lf Hank_mobley/* >> hank_mobley.txt

$ cat hank_mobley.txt

Mon Nov 21 21:33:58 CST 2005

1958_Peckin_Time/

1960_Roll_Cell/

1960_Soul_Station/

1961_Workout/

1963_No_Room_For_Squares/
```

### 注意事项

小心使用 `>>`。如果你不小心打成了 `>`，你就不会追加，而是覆盖！

### 将文件作为命令的输入

通常情况下，键盘为命令提供输入，这被称为标准输入（stdin）。就像你可以将 stdout 重定向到文件一样，你也可以重定向 stdin，使其源一个文件而不是键盘。为什么这样做很有用？某些命令无法直接打开文件，在这种情况下，`<`（小于号）正是你需要的。

例如，通常 `echo` 命令会重复你在 stdin 上键入的内容，如下所示：

```
$ echo "This will be repeated"

This will be repeated.
```

然而，你可以使用 `<` 来重定向输入，`echo` 命令将使用文件的内容而不是 stdin。在这种情况下，让我们使用上一节创建的 `hank_mobley.txt` 文件。

```
$ echo < hank_mobley.txt

Mon Nov 21 21:33:58 CST 2005

1958_Peckin_Time/

1960_Roll_Cell/

1960_Soul_Station/

1961_Workout/

1963_No_Room_For_Squares/
```

你不会一直使用 `<`，但在许多情况下它将恰好是你需要的，请记住这一点。

### 结论

本书从一些简单的命令开始，但现在你已经学习了构建模块，它们允许你以新颖有趣的方式组合这些命令。展望未来情况将变得更加复杂，也会更加强大。本章涵盖的内容是获得力量的关键因素。现在，前进吧！

## 第二部分：文件操作

- 第 5 章：查看文件
- 第 6 章：打印和管理打印作业
- 第 7 章：所有权与权限
- 第 8 章：存档与压缩

## 第 5 章：查看文件

Linux 系统的优点之一是，几乎所有重要的系统配置、日志和信息文件都是 ASCII 文本格式。由于 ASCII 是一种广受支持的古老（在计算机术语中）标准，有大量的软件命令可以查看这些文本文件的内容。本章介绍了你在读取 ASCII 文本文件时会不断使用的四个命令。

### 在 stdout 上查看文件

```
cat
```



## DOS 和 Linux 中的文本查看命令

DOS 用户有`type`命令，可以在屏幕上显示文本文件的内容。Linux 用户可以使用`cat`，它的功能相同。想在 shell 中查看文件吗？尝试一下`cat`。

```bash
$ cat Hopkins,--The_Windhover.txt
```

I caught this morning morning's minion, kingdom

of daylight's dauphin, dappled-drawn Falcon, in his riding

of the rolling level beneath him steady air, and striding

high there, he reung upon the rein of a wimping wing

in his ecstasy! then off, off on swerving.

As a skater's feel sweeps smooth on a bow-bend; the hurt and gliding

Rebound in the wild wind; my heart in hiding

Stirred for a bird,-- the achieve of, the mastery of the thing!

```
Brute beauty and valour and act, Oh, pride, plume, here
Buckle! AND the fire that breaks from thee, a billion

Times told lovely, more dangerous, o my chevalier!
No wonder of it: sheer plod makes plough down
sillion

Shine, and blue-bleak emmers, ah my dear,
Fall, gall themselves, and gash gold-vermilion.

Brute beauty and valour and act, Oh, pride, plume, here
Buckle! AND the fire that breaks from thee, a billion

Times told lovely, more dangerous, o my chevalier!
No wonder of it: sheer plod makes plough down
sillion
```

*(注：原文中存在大量由于 OCR 错误导致的重复文本，此处已根据要求进行清理和处理。)*

## 第二部分：文件操作

### 替代 cat 的工具：dog

如果你想要一个更好的`cat`，请看看`dog`（更多信息请参阅 `http://opensource.webblogs.com/2005/02/17/why-dogs-are-better-than-cats`）。你可以使用`dog`代替本地文件，在标准输出上查看网页的 HTML 源代码，或者查看指定网页上的图像或链接列表。`dog`可以将所有字符转换为小写或反之；将行结束符转换为`Mac OS`、`DOS`或`Unix`格式；你甚至可以指定输出的字符范围（例如第 525 行）。更不用说，`dog`的`man`页是史以来最优秀的文档之一。这个`dog`知道了很多新花样！

这里还有另一个为了响应`cat`而的程序：`tac`。它是`cat`的反过来写。这正是`tac`的作用：它反向合并文件。这并不是一个你总是会用到的功能，但当你确实需要这种功能时，知道它可以轻松实现是很棒的。

### 每次显示屏文本文件：less

`less` `file`

`cat`命令很有用，但如果你试图读取一个长文件，它就完全没用了，因为文本会像永无止境且不可读的流一样流过。如果你感兴趣在命令行中查看长文件（这里所谓的“长”是指超过一两页的内容），你不需要`cat`；你需要的是`less`。

`less`命令是一个分页程序的示例，它每次显示文件的一页。其他的程序还有`pg`和`most`；事实上，`less`是在 1985 年作为`more`的改进版而发布的，再次证明了*less is more*（少即是多）！

用`less`打开一个像弥尔顿的《失乐园》那样庞巨大的文件再简单不过了：

```bash
$ less Paradise_Lost.txt
```

`less`命令会占据你的整个屏幕，因此你必须使用键盘在`less`内部进行导航，并且必须退出`less`返回命令行。要在`less`内部导航，请使用表 5.1 中的按键：

**表 5.1. less 快捷命令**

| 按键命令 | 动作 |
| :--- | :--- |
| `PageDn`, `e` 或空格键 | 向前翻一页 |
| `PageUp` 或 `b` | 向后翻页 |
| `Return`, `e`, `j` 或向下箭头 | 向前移动一行 |
| `y`, `k` 或向上箭头 | 向后移动一行 |
| `G` 或 `p` | 跳到文件末尾 |
| `IG` | 回到文件开头 |
| `Esc-,` 或向右箭头 | 向右滚动 |
| `Esc(-)` 或向左箭头 | 向左滚动 |
| `Q` | 退出 |

如你所见，你有许多命令选项。你可能最常用的两个是用于一次移动一页和退出程序的命令。

在`less`状态下查看文件信息时，按下`=`，它会在屏幕最底部显示数据，如下所示：

```bash
Paradise_Lost.txt lines 7521-7560/10762 byte 166743/237306 70% (press RETURN)
```

如你所见，它会友好地提示按回车键清除数据并返回使用`less`。

就像你可以告诉`cat`为文件显示行号一样，你也可以让`less`显示行号。当然，这些数字只在你使用`less`时出现。当你按下`q`之后，数字就消失了。要查看每行开头都有行号的文件，请使用`-N`（或`--LINE-NUMBERS`）选项启动`less`，且必须全部大写：

```bash
$ less -N Paradise_Lost.txt
```

### 在分页器中搜索

如果你使用`less`查看一个大文件或内容特别密集的文件，可能很难找到你特别感兴趣的文本。例如，如果你想知道弥尔顿在《失乐园》是否使用了“苹果”一词来描述亚当和夏娃吃的水果？在`less`状态下，按下`/`然后输入你想要搜索的模式，你可以使用你喜欢的正则表达式。如果模式匹配，按下回车，`less`就会跳转到搜索结果的第一个实例（如果存在）。如果文件中没有该模式，`less`会提示你：

```bash
Pattern not found (press RETURN)
```

重复搜索也很简单，并且可以在文件中向前或向后搜索。表 5.2 涵盖了搜索`less`所需的主要命令。

**表 5.2. less 搜索命令**

| 按键命令 | 动作 |
| :--- | :--- |
| `/pattern` | 使用正则搜索模式 |
| `n` | 重复搜索 |

> **Note**: 不，弥尔顿从未明确将那种果实称为苹果；它只是一个“果实”。是的，我研究过多年十七世纪英国文学的博士学位。不，我没有完成它，这解释了为什么我在写这本书，而不是完全致力于约翰·弥尔顿和复兴时期文学。

### 编辑用分页器查看的文件

确实，`less`本身不是编辑器，只是一个查看器，但你可以通过按键将正在用`less`查看的文件传递给`vim`或`nano`等文本编辑器进行编辑。尝试`v`。用`less`查看文件，然后按下`v`。在一两秒钟内，`less`会消失，一个全屏文本编辑器会取而代之。进行编辑，退出以返回命令行。

## 第二部分：处理文件

And bathed every veyne in swich licour,
Of which vertu engend is the flour;
When Zephyrus eek with his sweete breeth
Inspired hath in every holt and heeth

如果你想查看查叟的《坎terbury故事集》的前 100MB，你会使用……不，那会占掉整本书书的剩余部分！但如果你真的想这样做，可以尝试这个：

```bash
$ head -c 100m Canterbury_Tales.txt
```



这里的`m`代表 1048576 字节，或者说 1024 x 1024。

### 查看文件的最后 10 行

`tail`

`head` 命令允许你查看文件的前 10 行，按照 Unix 那种典型的幽默风格，`tail` 命令则允许你查看文件的最后 10 行。从头（head）到尾（tail），你得到的是什么？

> `$ tail Paradise_Lost.txt`
> to the subjected plain - then disappeared
> They, looking back, all the eastern side beside
> Of Paradise, so late their happy meat;
> Waved by that flaming brand; the gate
> With dreadful faces thronged and fiery arms.
> Some natural tears they dropped, but wiped them:
> The world all before them, where to choose
> Their place of rest, and Providence their guide.
> They, hand in hand, with wandering steps and slow,
> Through Eden took their solitary way.

为什么要用`tail`？最常见是为了查看日志文件的末尾，以查看应用程序或系统正在发生什么。当然，在那种情况下你有一个想要使用的重要选项，正如你将在接下来的“查看不断更新的文件或文件的最后几行”章节中学习到的那样。

### 查看多个文件的最后 10 行

`tail file1 file2`

你可以使用`head`一次查看多个文件的前 10 行；惊讶的是，你也可以用`tail`做同样的事情。

```
$ tail Paradise_Lost.txt Miller's_Tale.txt

=> Paradise_Lost.txt <==

## 第二部分：处理文件

To the subjected plain - then disappeared
They, looking back, all the eastern side beside
Of Paradise, so late their happy seat,
Waved over by that flaming brand; the gate
With dreadful fears and fiery arms.
Some at them they stopped, but wiped them soon;
The world was all before them, where to choose
Their place of rest, and Providence guide.
They, in hand, with wandering steps and slow,
Through dark took the solitary way.
--> Miller's_Tail.txt <==

With others he went so sworn adown
That he holde wood in al the thou;
For he went midnight beheld with other.
They seyde, "The man is wood, my leeve brother";
And every wig gan laughter at this stryf.
Thus swyed was this carterys wyf,
For al his kepning and his jalousye;
And Absolution hath kist hir nether ye;
And Nicholas is scalded in the towte.
This tale is done, and God save al rowte!
```

同样像`head`一样，`tail`在条目之间包含一个标题/分隔符，这很有帮助。

### 查看文件或文件的最后几行

#### `tail -n`

延续`head`和`tail`的相似之处，你可以利用`-n`（或`--lines`）选项指定你想查看的文件行数，而不是接受默认的 10 行。想看多个文件？只需将其添加到你的命令中。

```
$ tail -n 4 Paradise_Lost.txt Miller's_Tale.txt

--> The world was all before them, where to choose

Their place of rest, and Providence guide.

They, in hand, with wandering steps and slow,

Through dark took the solitary way.

--> Miller's_Tail.txt <==

For al his kepning and his jalousye;

And Absolution hath kist hir nether ye;

And Nicholas is scalded in the towte.

This tale is done, and God save al rowte!
```

你有多个想要查看的日志文件吗？那么这个命令就很有用。但它并不完美。想要完美的命令，请阅读下一节。

### 查看不断更新的文件或文件的最后几行

#### `tail -f`

`tail -f --pid=PID` 在 `PID` 死亡后终止。

日志文件的棒之处在于，它们会随着系统上发生的事情而不断变化。`tail` 命令向你显示文件的快照，然后把你放回命令行。想再次查看日志文件吗？那就再次运行`tail`……反复运行。真讨厌！

使用`-f`（或`--follow`）选项，`tail`不关闭。相反，它会在你显示文件的最后 10 行（如果你混合了`-n`则显示不同的数字）后，随着文件的内容变化，让你能够观察日志文件发生的所有变化。如果你正试图弄清楚系统或程序到底发生了什么，这非常有用。

例如，Web 服务器的日志可能像这样：

注意

为了节省空间，我们忽略了访问的 IP 地址、日期和时间。

```
$ tail -f /var/log/httpd/d20srd_org_log_20051201

"GET /skrd/skills/1.1"

"GET /skrd/skills/motive.1"

"GET /skrd/skills/concentration.1"

"GET /skrd/skills/escape.1"
```

### 总结

在本章中你查看了四个命令：`cat`、`less`、`head` 和`tail`。它们以不同的方式显示。`cat` 命令一次显示整个文件，而`less`允许你逐页查看文件。`head` 和`tail` 命令是一枚硬币的两面，针对的是同一个文件。

## 第 6 章：打印和管理打印作业

多年来，Linux 有多种打印系统，包括老的打印机守护进程（LPD）和 LPR Next Generation（LPRng），它们在现代发行版中仍以遗留形式存在。在过去的几年里，大多数发行版已选择通用 Unix 打印系统（CUPS）作为首选。CUPS 支持良好、易于使用、现代，是 LPD 和 LPRng 的完美替代。本章关注 CUPS，因为它是大多数 Linux 用户使用的打印系统。本章不涵盖如何设置和配置打印机。大多数发行版现在提供了简单的 GUI 工具来完成。

Linux Journal 的“Linux 打印系统概述”（见 `http://www.linuxjournal.com/article/6729`）为 Linux 用户提供的选项提供了极佳的视角，特别关注了收藏。更多关于 CUPS 的信息，请参见 Linux Journal 的“CUPS 打印系统”（`http://www.linuxjournal.com/article/8618`），是对这项关键技术的很好的介绍。获取 CUPS 信息的最佳去处，不言自喻，是 CUPS 软件用户手册，你可以在 `http://www.cups.org/doc-1/sum.html` 找到。它很长有时过时，但充满了价值建议和帮助，是一份重要的资源。

### 列出所有可用打印机

```
lpstat -p
```

在开始处理打印机之前，你需要知道什么是“你的打印机”。要查找系统中配置的打印机，请使用`lpstat` 命令（line printer status 的缩写）以及`-p` 选项。

```
$ lpstat -p

printer bro is idle. enabled since Jan 01 00:00

printer bro_wk is idle. enabled since Jan 01 00:00

printer wu is idle. enabled since Jan 01 00:00
```



正如你看到的，这个系统有三个打印机 `bro`、`bro_wk` 和 `wu`，它们目前都没有在打印任何。

### 确定你的默认打印机

# 第二部分：处理文件

通过运行 `lpstat -p`，你已经知道了所有的打印机，但哪一个是默认的？正如你很快就会看到的，你可以将打印作业发送到特定的打印机，也可以快速将其发送到默认打印机。要找出哪个打印机是默认的，请使用带有 `-d`（代表 default）选项的 `lpstat` 命令。

```
$ lpstat -d
system default destination: bro
```

当然，如果电脑只连接了一台打印机，你可能不需要运行此命令。但对于在不同地点移动并向不同打印机打印的笔记本用户来说，这个命令是不可少的。

### 查看你的打印机是如何连接的

```
lpstat -s
```

笔记本用户会发现下一个命令特别有用，因为它告诉他们如何访问可用的打印机。当你首次设置打印机时，必须指定连接方式。你有几种选择：

- 本地（并行口、串口或 USB）
- 远程 LPD 队列
- SMB 共享打印机（Windows）
- 网络打印机 (TCP)
- 远程 CUPS 服务器 (IPP/HTTP)
- 带有 IPP 的网络打印机 (IPP/HTTP)

要查找你的电脑配置了哪些打印机以及你如何连接它们，请使用带有 `-s` 选项的 `lpstat`。

```
$ lpstat -s
system default destination: bro
device for bro: socket://192.168.0.160:9100
device for bro_wk: socket://192.168.1.110:9100
device for wu: socket://128.252.93.10:9100
```

在这种情况下，每台打印机都是网络打印机，因此它们使用 `socket:`，随后是打印机的 IP 地址和端口（`9100` 是大多数网络打印机的标准端口，尽管你也可能看到使用端口 `3500`）。这非常简单，但可能会迅速变得复杂。

尽管 CUPS 在许多方面都很用户友好，但在处理用于指示打印机相对于你的 Linux 位置的统一资源标识符 (URI) 时，它是臭名昭著的难懂。表 6.1 列出了每种连接方法以及你可能会看到的 URI 类型，这应该帮助你理解在执行 `lpstat -s` 时看到的打印机和 URI 列表。

### 注意

假设后续示例中的打印机是 `bro`，位于网络 `192.168.0.160`。当然，这在所有情况下并不适用。如果打印机是通过并行线连接的，那么其 IP 地址就无关了。

### 6.1. 打印机连接与 CUPS 连接方法

| 示例 URI（位于 `192.168.0.160` 的打印机 `bro`） |
| :--- |
| `parallel:/dev/lp0` |
| `serial:/dev/ttyS1/baud=115200` |
| `usb:/dev/usb0` |
| `lp1:/192.168.0.160/LPT1` |
| `smb://username:password@192.168.0.160/bro` |
| `socket://192.168.0.160:9100` |
| `ipp://192.168.0.160:631/printers/bro` |
| `http://192.168.0.160/printers/bro` |

- 并行
- 串行
- USB
- 远程 LPD 队列
- SMB 共享打印机（Windows）
- 网络打印机 (TCP)
- 远程 CUPS 服务器 (IPP/HTTP)
- 带有 IPP 的网络打印机 (IPP/HTTP)

得益于过去几年网络打印的兴起，通过 `socket`、`ipp` 或 `http` 连接打印机变得更加简单。即使你仍然遇到需要较旧、更复杂方法的遗留打印机，熟悉它们也是好的。

### 提示

一个额外的好处是，`lpstat -s` 本质上复制了 `lpstat -p` 的功能，因为它列出了系统已知的所有打印机以及默认打印机。如果你想快速获取所有信息，这是一个好用的命令。

### 一次性获取关于你打印机的所有信息

### `lpstat -t`

现在来看这个强大的命令。`lpstat -p`、`lpstat -d` 或 `lpstat -s` 的优点在于，你只会获得你所需的精确信息。然而，如果你想一次获取所有信息，请使用带有 `-t` 选项的 `lpstat`，它会将 `lpstat` 关于你打印机的所有信息转储到你的 shell 中。

```
$ lpstat -t
scheduler is running
system default destination: bro
device for bro: socket://192.168.0.160:9100
device for bro_wk: socket://192.168.1.10:9100
device for wu: socket://128.252.93.10:9100
bro accepting requests since Jan 01 00:00
bro_wk accepting requests since Jan 01 00:00
wu accepting requests since Jan 01 00:00
printer bro is idle, enabled since Jan 01 00:00
printer bro_wk is idle, enabled since Jan 01 00:00
printer wu is idle, enabled since Jan 01 00:00
```

你获得了一切：你的默认打印机、系统所有打印机列表、这些打印机的连接方法和位置，以及所有打印机的状态。你电脑上的配置越多，这个列表就越长。对于某些人来说，这可能会让人压力很大，因此你可能发现使用其他选项的 `lpstat` 更好。

### 将文件打印到默认打印机

### `lpr`

现在你已经知道系统中有哪些打印机了，是时候实际使用它们来打印东西了。打印到默认打印机（通过 `lpstat -d` 确定）很容易的。

```
$ lpr Lovecraft-Call_of_Cthulhu.txt
```

就是这样：只需输入 `lpr` 加上文件名。非常简单。你可能认为可以使用 CUPS 在命令行上打印 ASCII 文本，但发现你也可以打印 PDF 或 PostScript 文件，可能会让你感到惊讶。但不要尝试打印 Word、OpenOffice 或任何其他非文本或非 PostScript 的文档，否则你的打印机将吐出一页页乱码！

### 将文件打印到任何打印机

如上一节所示，打印到默认打印机非常简单。如果你有多个打印机，并且想打印到某个不是默认的打印机，只需使用 `-P` 选项，后面跟着打印机名称。

```
$ lpr -P bro_wk Lovecraft-Call_of_Cthulhu.txt
```

如果你不知道打印机的名称，请像之前在“列出所有打印机”节中讨论的那样，使用 `lpstat -p`。你会注意到文件名使用了下划线而不是空格，这使得处理命令行变得容易得多。如果文件名包含空格，你必须使用以下方法之一来引用它：

```
$ lpr -P bro_wk "Lovecraft - Call of Cthulhu"
```

或者

```
$ lpr -P bro_wk Lovecraft\ Call\ Cthulhu
```

如果文件名包含空格，最简单的方法也许是使用 Tab 键补全，这样你就不需要手动输入名称。例如，输入 `lpr -P bro_wk Love` 然后按 Tab 键，让 `bash` 完成文件名。更多关于 Tab 补全的信息，请访问 `linuxbook.org/html/shell.html`。

### 打印文件的多个副本

### `lpr -#`

如果你想打印一个文件的多个份，请使用 `#`（井号）选项，后面跟份数：

```
$ lpr -# 2 -P bro Lovecraft-Call_of_Cthulhu.txt
```

数字范围从 1 到 100。想要 100 份？重复命令。或者写个脚本。

### 查看打印作业

### `lpq`

如果你有多个作业排队打印，你可能想查看该列表。也许你想取消某些作业（如何操作见后续章节），你想知道为什么作业打印得这么慢，或者你想知道队列中有多少作业。`lpq` 命令（即“打印队列”）列出了默认打印机上正在打印的所有作业。

```
$ lpq
bro is ready and printing
Rank Owner(s) Total Size
active scott 489 Lovecraft-Call_of_Cthulhu 108544 bytes
```

如果要列出所有打印机的状态而不只是默认的，只需在 `lpq` 后加上 `-a`（代表 all）：

```
$ lpq -a
Rank Owner(s) Total Size
active scott 489 Lovecraft-Call_of_Cthulhu 108544 bytes
```



`list scott 490 ERB-A_Princess_of_Mars 52488 bytes`

```

请记住两点。首先，`lpq -a` 列表被截断了，所以文件名实际上是 `Lovecraft-Call_of_Cthulhu.txt` 和 `ERB-A_Princess_of_Mars.txt`，你没有看到完整名称是因为 `lpq` 显示的字符有限。

其次，非常重要，`lpq` 显示并不是打印机知道的所有作业，而是你的机器知道的。从打印机的角度来看，打印队列可能像这样：

- `Lovecraft-Call_of_Cthulhu.txt`
- `Doyle-The_Lost_World.txt`
- `ERB-A_Princess_of_Mars.txt`

要查询真实的队列，你需要使用该设备自带的管理工具，这超出了本书的范围。

### 按打印机列出打印作业

`lpstat`

`lpq` 命令显示排队打印的文件，但它没有告诉这些文件被发送到了哪个打印机。要了解这一点，你需要使用之前在“列出所有打印机”节中介绍过的 `lpstat` 命令。然而，这次只需不带任何选项直接使用 `lpstat`：

```
$ lpstat
```

# 18

## 第二部分：文件操作

结果是一个作业列表，每行的开头是处理该作业的打印机名称。你是否在无意中将作业发送到了你当前未连接的打印机？使用 `lpstat` 查找，然后删除该作业（你将在下一节中学习如何删除它）。

### 取消发送到默认打印机的当前打印作业

#### `lpm`

你想取消当前正在发送到默认打印机的打印作业吗？只需使用 `lpm` 即可（类似于 "lp remove"）。

```bash
$lpm
```

请务必快速执行此命令。现在的许多打印机速度非常快，而且内存非常大，作业可能已经离开了你的机器并在打印机上运行。在这种情况下，请找到你打印机上的“取消（Cancel）”按钮并快速按下！

### 取消发送到任意打印机的打印作业

#### `lpm` `job ID`

在上一节中，你学习了如何取消发送到默认打印机的当前打印作业。但如果作业仍在队列中，几分钟后才会开始呢？或者如果作业正发往一个非默认打印机呢？在这种情况下，你仍然可以使用 `lpm`，但你需要通过引用作业 ID 号来告诉命令要取消哪个作业。

查看[列出打印作业]中的示例。第三列标记为“Job（作业）”，里面有一个数字。现在回[按打印机列出打印作业]。在每个作业 ID 名称之后是一个连字符，然后是你在[列出打印作业]中看到的数字。那个就是作业 ID 号。将该数字指定给 `lpm`，该作业将被取消。

```bash
$ lpstat

bro-489 rsgranne 108544 Tue 10 Dec 2005

bro_wk-490 rsgranne 524288 Tue 10 Dec 2005

$ lpm 490

$ lpstat

bro-489 rsgranne 108544 Tue 10 Dec 2005
```

使用这个特定的命令，你真的可以避免纸张、碳粉盒和墨水的无谓浪费。下次当你意识到自己刚刚向打印机发送了一份 500 页的大图文档，并使用 `lpm` 和作业 ID 停止了它时，请给我发封邮件感谢我吧。

### 取消所有打印作业

```bash
lprm -
```

如果你有多个想要取消的打印作业怎么办？你可以通过指定所有的作业 ID 号来删除它们，如下：

```bash
$ lprm 489 490 491 492 493
```

但那样太多了。如果你想删除每台打印机上队列的所有打印作业，在 `lprm` 后加一个连字符即可：

```bash
$ lprm
```

它既快速又无痛，而且符合 Linux 最优秀的“懒人传统”。这没什么好羞的！

### 总结

打印是人们在计算机上执行的一项活动，因此学习如何高效打印非常重要。打印的一部分是知道如何查询打印机以及最初如何将这些作业发送到打印机。当然，并不是所有的作业都需要打印，所以知道如何取消不需要的作业同样重要。本章涵盖了你在 Linux 内部与打印机交互所需的主要任务，最后我给你一点建议：支持 Linux 的自动双面打印机价格已经大幅下降，它们将帮你节省一大笔纸张钱。下次你想购买打印机时，去看看它们。你会庆幸此举的。

## 第 7 章：所有权与权限

Linux 从一开始就被设计为多用户系统（与 Windows 不同，Windows 被设计为单用户操作系统，这直到今天仍是其安全问题的根源）。这意味着不同的用户将在系统中创建文件、删除目录和读取各种项目。为了防止大家互相踩脚和损坏底层操作系统，一套权限系统被创建了。掌握权限的艺术将有助于你使用 Linux 机器，无论它是单人的工作站还是数百人访问的服务器。是时候开始了！

### 修改文件的所属组

#### `chgrp`

默认情况下，在几乎所有的 Linux 系统上，当你创建一个新文件（或目录）时，你是该文件的所有者和组。例如，假设我们要编写一个可以在你的系统中运行的脚本。

**注意**：为了节省空间，我用省略号替换了 `ls` 通常会看到的信息。

```bash
$ new_script.sh

$ ls -l

-rw-r--r-- 1 scott ... script.sh
```

**注意**：在该机器上用户名和组名恰好都是 "scott"，但并非每台机器都如此。创建文件时，用户的 UID（用户 ID 号）成为文件的所有者，而用户的 GID（组 ID）成为文件的所属组。

如果你是你机器上 admins 组的成员，并希望你的组其他成员也能运行你的脚本呢？在这种情况下，你需要使用 `chgrp` 命令将组从 scott 改为 admins。

```bash
$ chgrp admins new_script.sh

$ ls -l

-rw-r--r-- 1 scott admins ... script.sh
```

**注意**：是的，脚本无法运行是因为没有执行权限。该过程将在本章后面通过 `chmod` 进行讲解。

你应该了解关于 `chgrp` 的几点。运行 `chgrp` 时，可以使用组名或组的数字 ID。如何找到与组关联的数字？最简单的方法是对 `/etc/group` 使用 `cat`（这是记录机器上组信息的文件），然后查看结果。

```bash
$ cat /etc/group

bind:x:118:

scott:x:1001:

admins:x:1002:scott,alice,bob
```

### 递归修改目录的所属组

#### `chgrp -R`

如果你想更改目录及其所有内容的组，请使用递归标志 `-R`。

```bash
$ chgrp -R group_name directory_name
```

## 第二部分：操作文件

这次，系统没有对 `libby.jpg` 进行任何报告，因为它已经在家庭组中了。所以，如果你想要完整的报告（即使是对于不会更改的文件），请使用 `-v`；如果需要更简洁的列表，请使用 `-c`。

### 修改文件和目录的所有者

`chown`

更改文件的所属组是重要的，但你更有可能更改所有者。要更改组，使用 `chgrp`；要更改所有者，使用 `chown`。

```
$ ls -l

-rw-r-- 1 scott libby_arrowrock.jpg

-rw-r-- 1 scott family ... libby.jpg

-rw-r-- 1 scott scott ... libby_on_couch.jpg

$ chown denise libby.jpg

$ ls -l

-rw-r-- 1 scott libby_arrowrock.jpg

-rw-r-- 1 denise family ... libby.jpg

-rw-r-- 1 scott scott ... libby_on_couch.jpg
```

之前关于 `chgrp` “更改文件和目录的所属组”的一些要点也适用于 `chown`。`chown` 命令使用用户名或数字 ID。可以通过运行 `cat /etc/passwd` 查看用户的数字 ID，它会给你如下内容：

```
bind:x:110:118:/var/cache/bind:/bin/false

scott:x:1001:101:scott,,,:/home/scott:/bin/bash

top:x:120:120::/var/lib/ntop:/bin/false
```



你看到的第一个数字是该用户的数字 ID（第二个数字是与用户关联的主组的数字 ID）。

此外，如果你是当前文件的所有者（当然，也包括 `root` 用户），你可以更改文件的所有者。这不应该让你感到惊讶，但记住这一点是有好的。

### 注意事项

如果你使用 `chown -R scott *`，你不会更改目录中的任何隐藏文件（dot files）。然而，不应使用 `chown -R scott .*`。它会更改当前目录下的所有隐藏文件，但 `.` 也会匹配 `..`，因此父目录中的所有文件也会被更改，这可能不是你想要的。

## 修改文件和目录的所有者和组

`chown owner:group`

你已经看到可以使用 `chgrp` 更改组，可以使用 `chown` 更改所有者，但使用 `chown` 可以“一石二鸟”。在 `chown` 之后，指定用户然后是组，用冒号隔开，最后是文件或目录（这就是为什么你应该避免在用户名或组名中使用冒号的原因）。

```
$ ls -l
-rw-r--r-- 1 scott ... libby.jpg
$ chown denise:family libby.jpg
$ ls -l
-rw-r--r-- 1 denise family ... libby.jpg
```

你可以通过在冒号前留空用户来使用 `chown` 仅更改组。

```
$ ls -l
-rw-f--r-- 1 scott ... libby.jpg
$ chown :family libby.jpg
$ ls -l
-rw-f--r-- 1 scott family ... libby.jpg
```

### 提示

如果用户名或组名中包含冒号怎么办？只需在冒号前输入一个反斜杠，这会“转义”该字符并告诉系统它只是一个冒号，而不是用户名和组名之间的分隔符：

```
$ chown denise\:libby.jpg
```

这种方法可行，但从根本上最好不要在用户名和组名中使用冒号。因为 `chown` 可以完成 `chgrp` 能做的所有事情，所以几乎很少使用 `chgrp`，除非你觉得有用。当你分离用户和组时，实际上可以使用 `.` 或 `:`，但建议坚持使用 `:`，因为 `.` 已经废弃。

## 理解权限的基础知识

在继续学习 `chmod` 命令（它允许你更改与文件或目录关联的权限）之前，让我们回顾 Linux 是如何理解这些权限的。

### 注意事项

Linux 系统开始使用一种更细粒度、更强大的系统，称为访问控制列表（ACLs）。目前 ACLs 尚未被广泛使用，因此这里没有涵盖它们。有关 ACLs 的更多信息，请参见 `www.linux-mag.com/2004/11/guru_01.html` 以及 Linux Magazine 中的“An ACL GUI for Linux”（`http://opensource.weblogs.com/2005/12/an-acl-gui-for-linux/`）。

Linux 理解为三类用户在操作文件或目录：实际所有者（也称为用户）、一个组以及系统上的其他人。这些组中的每一组由不同的字母表示，如表 7.1 所示。

### 表 7.1. 用户和缩写

| 用户 | 缩写 |
|---|---|
| 用户 (所有者) | `u` |
| 组 | `g` |
| 其他人 | `o` |

### 表 7.2. 权限层级和含义

| 文件属性 | 缩写 | 对文件的含义 | 对目录的含义 |
|---|---|---|---|
| 可读 | `r` | 可以查看内容。 | 可以用 `ls` 列出。 |
| 可写 | `w` | 可以编辑内容。 | 可以删除、重命名或添加文件。 |
| 可执行 | `x` | 可以作为程序运行。 | 可以进入（访问）读取文件和子目录，或运行文件。 |
| `suid` | `s` | 任何用户都可以以所有者的权限执行文件。 | 不适用。 |
| `sgid` | `s` | 任何用户都可以以组权限执行文件。 | 目录中所有新创建的文件都属于该目录的组。 |
| 位 | `t` | 告诉操作系统该文件将被频繁执行，因此将其保留在交换空间中以便快速访问（仅针对旧版 Unix 系统；Linux 忽略）。 | 用户无法删除或重命名文件，除非他是该文件或所在目录的所有者。 |

### 注意事项

`root` 用户始终对任何文件或目录执行任何操作，因此前面的表不适用于 `root`。这些文件属性在接后的章节中会有更详细的介绍。现在你已经理解了基础知识，让我们来看看如何使用 `chmod` 命令更改文件和目录的权限。

## 使用字母表示更改文件和目录的权限

字母或数字表示各有优劣，但对用户来说，字母系统有时更容易。基本方法使用一个简单的公式：你想要更改的用户组 (`u`, `g`, `o`)；后面跟着加号 (`+`) 表示授予权限、减号 (`-`) 表示移除权限或等号 (`=`) 表示设置精确权限；最后是字母 (`r`, `w`, `x`, `s`, `t`)，表示你想要更改的权限。例如，假设你想允许家庭组能够更改某个文件。

```
$ ls -l
-rw-r--r-- 1 scott ... libby.jpg
$ chmod g+w libby.jpg
$ ls -l
-rw-f-w-- 1 ... libby.jpg
```

这足够了。但如果你想让家庭组和其他所有用户对文件都有写入权限呢？如果你使用 `chown -R scott *`，你不会更改目录中的任何隐藏文件。然而，不应使用 `chown -R scott .*`。它会更改当前目录下的所有隐藏文件，但 `.` 也会匹配 `..`，因此父目录中的所有文件也会被更改，这可能不是你想要的。

## 第二部分：文件文件操作

### 表 7.4. 使用 `ls -l` 表示的数字权限

| 数字 | `ls -l` 表示法 |
| :--- | :--- |
| 0 | `---` |
| 1 | `--x` |
| 2 | `-w-` |
| 3 | `-wx` |
| 4 | `r--` |
| 5 | `r-x` |
| 6 | `rw-` |
| 7 | `rwx` |

尽管可以设置各种权限，但有几种权限往往反复出现。表 7.5 显示了常用权限及其含义。

## 表 7.5. 使用 `ls -l` 表示的常用权限

| `chmod` / `ls -l` 表示法 | 含义 |
| :--- | :--- |
| `chmod 400` | `-r--------` | 所有者可以读取；其他人无法进行任何操作。 |
| `chmod 644` | `-rw-r--r--` | 所有人都可以读取；只有所有者可以编辑。 |
| `chmod 660` | `-rw-rw--` | 所有者和组可以读取并编辑；世界无法进行任何操作。 |
| `chmod 664` | `-rw-rw-r--` | 所有人都可以读取；所有者和组可以编辑。 |
| `chmod 700` | `-rwx------` | 所有者可以读取、写入和执行；其他人无法进行任何操作。 |
| `chmod 744` | `-rwxr--r--` | 所有人都可以读取；只有所有者可以编辑和执行。 |
| `chmod 755` | `-rwxr-xr-x` | 所有人都可以读取和执行；只有所有者可以编辑。 |
| `chmod 777` | `-rwxrwxrwx` | 所有人都可以读取、编辑和执行（通常不是个好主意）。 |

注意

是的，你可以对文件或目录设置 `chmod 000`，但现在唯一可以对其进行任何操作或再次使用 `chmod` 更改权限的用户是 `root` 了。

八进制权限确实会引起困惑。它们比理解权限需要更多的认知，但它们允许你一次性完成多项更改。让我们回顾一下“使用字母表示法更改文件和目录权限”中的示例，但改用数字。

假设你想允许家庭组的成员能够更改一张图片。

```bash
$ ls -l
-rw-f--r-- 1 scott family ... libby.jpg
$ chmod 664 libby.jpg
$ ls -l
-rw-f-w-- 1 scott family ... libby.jpg
```

如果你想给家庭组和所有其他用户提供该文件的写入权限怎么办？

```bash
$ ls -l
-rw-f-w--r-- 1 scott family ... libby.jpg
$ chmod 666 libby.jpg
$ ls -l
-rw-f-w-f-w-- 1 scott family ... libby.jpg
```

你意识到你犯了一个错误，需要移除家庭组和世界用户修改该图片的能力，并确保所有人都能看到图片。

```bash
$ ls -l
-rw-f-w--r-- 1 scott family ... libby.jpg
$ chmod 640 libby.jpg
$ ls -l
-rw-f--r-- 1 scott family ... libby.jpg
```



### 递归更改权限

这个示例展示了这种方法的关键优势。使用字母表示法需要分两步——先 `chmod go-w` 然后是 `chmod -r`（或 `chmod g=r` 和 `chmod o=`）——而使用数字表示法只需要一个命令。出于这个原因，你经常看到高级 Linux 用户使用表示法，因为它更快且似乎更精确。

#### chmod -R

你现在可能已经注意到许多 Linux 命令允许你将它们递归应用于文件和目录，`chmod` 也不例外。`-R`（或 `--recursive`）选项允许你在几秒钟更改数百个文件的权限，只需确保这是你想要做的。

```bash
$ pwd

/home/scott

$ ls -l

-rw-r--r-- 1 scott scott ... libby.jpg

drwxr-xr-x 2 scott scott ... pictures/

-rw-r--r-- 1 scott scott ... vacation.jpg

drwxr-xr-x 2 scott scott ... documents/

-rw-r--r-- 1 scott scott ... report.txt
```

如果你运行 `chmod -R 644 pictures`，它将递归地更改目录及其所有文件的权限。

```bash
$ chmod -R 644 pictures

$ ls -l

drw-r--r-- 2 scott scott ... pictures/

-rw-r--r-- 1 scott scott ... vacation.jpg
```

注意，这会导致目录失去可执行权限，因此你将无法进入该目录。要修复此，你需要为目录添加执行权限：

```bash
$ chmod -R 755 pictures

$ ls -l

drwxr-xr-x 2 scott scott ... pictures/

-rw-r--r-- 1 scott scott ... vacation.jpg
```

如果你只想递归地更改文件而不影响目录，可以使用 `find` 命令：

```bash
$ find pictures -type f -exec chmod 644 {} +

$ ls -l

drwxr-xr-x 2 scott scott ... pictures/

-rw-f--r-- 1 scott scott ... vacation.jpg
```

在第 10 章“find 命令”中了解更多信息。

### 设置并清除 suid

#### chmod u[+-]s

在“理解权限基础”部分中，你查看了多种可能的权限。你关注的是 `r`、`w` 和 `x`，因为它们是最常见的，但其他权限在某些时候派得上用场。

与 `suid` 密切相关的 `sgid` 可以同时应用于文件和目录。对于文件，`sgid` 就像 `suid`，区别在于用户可以使用组权限而不是所有者权限来执行文件。例如，在你的系统中，`crontab` 命令可能被设置为 `sgid`，这样用户就可以请求 `cron` 为他们运行程序，但使用的是受限的 `crontab` 组而不是强大的 `root` 用户。

```bash
$ ls -l /usr/bin/crontab

-rwsr-sr-x 1 root crontab ... /usr/bin/crontab
```

作为普通用户，你不太可能更改程序为 `suid`。大多数这与 `root` 拥有的程序有关，但在偶尔需要使用时，了解它仍然是好事。

## 第二部分：文件操作

假设你有三个用户：`Alice`、`Bob` 和 `Carol`，他们都是 `admins` 组的成员。`Alice` 的用户名是 `alice`，她的主组也是 `alice`，这在 Linux 系统中是非常常见的现象。`Bob` 和 `Carol` 遵循相同的模式，他们的用户名和主组分别为 `bob` 和 `carol`。如果 `Alice` 在 `admins` 组共享的目录中创建一个文件，该文件的所有者和所属组将是 `alice`，这意味着 `admins` 组的其他成员无法对其进行写入。当然，`Alice` 在创建新文件后可以运行 `chown`（`chown admins document`），但这会变得极其繁琐。

然而，如果将共享目录设置为 `sgid`，那么在该目录下创建的任何新文件所有者仍然是创建它的用户，但在这种情况下，组是 `admins`。结果是，`Bob` 和 `Carol` 也可以读取和编辑该共享目录中的任何文件，而且减少了繁琐程度。

惊讶的是，你可以使用字母或数字设置 `sgid`。使用字母时，`sgid` 就像 `suid` 一样，只是使用了 `s`。让我们看看应用于目录的 `sgid`，但请记住，相同的过程也适用于文件。

```
$ ls -lf

drwxr-xr-x 11 admins ... /bin/

$ chmod g+s bin

$ ls -lf

drwxr-xr-x 11 admins ... /bin/
```

### 注意

你可能会同时看到 `s` 和 `S` 来表示设置了 `sgid`。如果你在设置 `sgid` 之前组已经有了执行权限（`x`），则你会看到 `s`；如果你在设置 `sgid` 之前组没有执行权限，则你会看到 `S`。最终结果是相同的，但大小写可以了原始的权限状态。

移除 `sgid` 几乎与添加它完全相反。

```
$ ls -lf

drwxr-xr-x 11 admins ... /bin/

$ chmod g-s bin

$ ls -lf

drwxr-xr-x 11 admins ... /bin/
```

如果你还没有读过之前的章节“设置和清除 suid”，请回去读一下，因为它解释了出现在所有者权限数字之前的那个神秘的第四位。在 `suid` 的情况下，该数字是 `4`；对于 `sgid`，数字是 `2`。

```
$ ls -lf

drwxr-xr-x 11 admins ... /bin/

$ chmod 2755 bin

$ ls -lf

drwxr-xr-x 11 admins ... /bin/
```

你通过移除 `suid` 的相同移除 `sgid`：在开头使用一个 `0`，这会让 `sgid` 消失。

```
$ ls -lf

drwxr-sr-x 11 scott admins ... bin/

$ chmod 0755 bin

$ ls -lf

drwxr-xr-x 11 scott admins ... bin/
```

### 注意

你知道在 `sgid` 目录中创建新文件会发生什么，但请注意其他文件系统进程也会受到 `sgid` 的影响。如果你用 `cp` 将文件复制到 `sgid` 目录，它将获得该目录的组。然而，如果你用 `mv` 将文件移动到 `sgid` 目录，它将保留当前的组所有权，而不会获得目录组的所有权。最后，如果你使用 `mkdir` 在 `sgid` 目录内部创建一个新目录，它不仅会继承拥有 `sgid` 目录的组，本身也会变成 `sgid`。

### 设置并清除粘滞位（Sticky Bit）

```
chmod [+]-t
```

除了这是一个朗朗上口的短语外，粘滞位是什么？在 Unix 的旧时代，如果一个可执行文件设置了粘滞位，操作系统就知道该文件将不断运行，因此会将其保留在交换空间中，以便快速高效地访问。Linux 是一个更现代的系统，因此当在文件上设置粘滞位时它会忽略它。

这意味着粘滞位用于目录。在文件夹中设置粘滞位后，除非用户是文件的所有者或粘滞位目录的所有者，否则无法删除或重命名该文件夹中的文件。如果没有设置粘滞位且文件夹对其他人可写，这意味着那些用户可以删除和重命名其中的任何文件。粘滞位防止了这种情况发生。你最常看到它的地方是 `/tmp` 目录，它设计上对所有人可写，但 `/tmp` 内部的单个文件和文件夹受粘滞位的保护，其他用户无法操作。

```
$ ls -t /

drwxrwt 12 root root ... tmp

[结果截断]
```

### 注意

你可能会同时看到 `a` 和 `T` 来表示设置了粘滞位。如果你在设置粘滞位之前世界已经有了执行权限（`x`），则你会看到 `t`；如果你在设置粘滞位之前世界没有执行权限，则你会看到 `T`。结果是相同的，但大小写可以了原始的权限状态。

与本章中许多其他使用 `chmod` 的示例一样，可以使用字母或数字设置粘滞位。

```
$ ls -lF

drwxrxr-x 2 scott family ... libby_pix/

$chmod +t libby_pix

$ ls -lF

drwxrxr-t 2 scott family ... libby_pix/
```



# 高级文档排版优化内容

## 潜在困惑

有两点可能会有点困惑：首先，在这里，之前使用字母方法时，可以使用字母或数字设置粘滞位。

## 第二部分：文件操作

本章中所有的归档和压缩格式——`zip`、`gzip`、`bzip2` 和 `tar`——都是非常流行的。`zip` 可能是世界上使用最广泛的格式。由于这个原因，它在 `Windows` 上几乎无处不在，但 `zip` 和 `unzip` 在所有主要（以及次要）操作系统中都得到了良好支持，这意味着使用 `zip` 压缩的文件在 `Linux` 和 `Mac OS` 上也可以运行。如果你正在向用户发送归档文件，并且知道他们使用的系统，那么 `zip` 是一个安全的选择。

`gzip` 被设计为旧版 `Unix` 程序 `compress` 的开源替代品。它存在于世界上几乎每一个基于 `Unix` 的系统中，包括 `Linux` 和 `Mac OS X`，但在 `Windows` 上作为附件时并不常见。如果你需要与基于 `Unix` 的机器的用户往来收发文件，`gzip` 是一个安全的选择。

`bzip2` 是该领域的新秀。`bzip2` 的设计旨在取代 `gzip`，它能创建更小的文件，但是以牺牲速度为代价的。尽管如此，现在的计算机运行非常快，大多数用户可能感觉不到使用 `gzip` 或 `bzip2` 压缩一组文件的时间差异有多大。

> **注意**
>
> 《Linux 杂志》发表过一篇比较几种压缩格式的优秀文章，你可以在 `http://www.linux-mag.com/content/view/1678/43` 找到。

`zip`、`gzip` 和 `bzip2` 侧重于压缩（尽管 `zip` 也负责归档）。`tar` 命令只做一件事：执行它做了很久的文件归档。它几乎只出现在基于 `Unix` 的机器上。如果你下载源代码，绝对会遇到 `tar` 文件（称为 `tar` 包），但几乎每个 `Linux` 用户都可以预期在职业生涯中的某个时候遇到一个 `tar` 包。

### 使用 `zip` 归档和压缩文件

#### `zip`

`zip` 同时对文件进行归档和压缩，使其非常适合将多个文件作为附件、备份项目或节省磁盘空间。它非常简单。假设你想通过电子邮件向某人发送一个 `TIFF` 文件。`TIFF` 图像是未压缩的，因此通常很大。将其压缩应该帮助让邮件附件变小一点。

> **注意**
> 在使用 `ls -l` 时，我只显示了每个示例所需的信息。

```bash
$ ls -lh

-rw-r-- scott 1006K young_edgar_scott.tif

$ zip grandpa.zip young_edgar_scott.tif

adding: young_edgar_scott.tif (deflated 19%)

$ ls -lh

-rw-r-- scott 1006K young_edgar_scott.tif

-rw-r-- scott 819K grandpa.zip grandpa
```

在这种情况下，你为生成的 `zip` 文件缩减了约 200KB，或者说 19%，正如 `zip` 高乐地告知的那样。不错。你可以对几张图片进行同样的操作。

```bash
$ ls -l

-rw-r--r-- scott scott 251980 edgar_intl_shoe.tif
-rw-r--r-- scott scott 1130922 edgar_baby.tif
-rw-r--r-- scott scott 1029224 young_edgar_scott.tif

zip grandpa.zip edgar_intl_shoe.tif baby.tif young_edgar_scott.tif

adding: edgar_intl_shoe.tif (deflated 4%)

adding: edgar_baby.tif (deflated 12%)

adding: young_edgar_scott.tif (deflated 19%)

$ ls -l

-rw-r--r-- scott scott 251980 edgar_intl_shoe.tif
-rw-r--r-- scott scott 1130922 edgar_baby.tif
-rw-r--r-- scott scott 2074296 grandpa.zip
-rw-r--r-- scott scott 1029224 young_edgar.zip
```

随你所愿将单个文件压缩并没有什么大不了的。对于三个文件，接收者将解压 `grandpa.zip` 并最终得到三个独立的文件。如果密码是 500，用户最终将得到散落在各处的文件。最好压缩包含那 50 个文件的目录，这样用户解压它们时，就能得到一个整洁的目录。

```bash
$ ls -if

drwxr-xr-x scott scott edgar_scott/

zip grandpa.zip edgar_scott

adding: edgar_scott/ (stored 0%)

adding: edgar_scott/edgar_baby.tif (deflated 12%)

adding: edgar_scott/young_edgar_scott.tif (deflated 19%)

adding: edgar_scott/edgar_intl_shoe.tif (deflated 4%)

$ ls -if

drwxr-xr-r-- scott scott 160 edgar_scott/
-rw-r--r-- scott scott 2074502 grandpa.zip
```

无论你是压缩一个文件、多个文件还是一个目录，模式都是相同的：先是 `zip` 命令，接着是你要创建的 Zip 文件名，最后是你要添加到 Zip 文件中的项目。

### 使用 `zip` 获得可能的压缩效果

你可以调整 `zip` 在工作时使用的压缩级别。`zip` 命令使用从 0 到 9 的量级，其中 0 表示“完全不压缩”（这很像 `tar`，正如你稍后会看到的），1 表示“快速完成工作，但压缩不多”，而 9 表示“拼命压缩这些文件，我不介意多等一会儿来完成任务”。默认值是 6，但现代计算机的速度足够快，可能一直使用 9 也没问题。

假设你正在研究赫尔曼·梅维尔的《白鲸记》，所以你想收集一些关键文本来帮助理解这本书：《白鲸记》本身、密尔顿的《天堂乐》以及圣经中的《约伯记》。让我们比较不同压缩率的结果。

```bash
$ ls -l

-rw-r--r-- scott scott 102519 job.txt
-rw-r--r-- scott scott 1236574 moby-lost.txt
-rw-f--r-- scott scott 508925 paradise_lost.txt

$ zip moby.zip *.txt

adding: job.txt (stored 0%)

adding: moby-lost.txt (stored 0%)

adding: paradise_lost.txt (stored 0%)

$ ls -l

-rw-f--r-- scott scott 102519 job.txt
-rw-f--r-- scott scott 1236574 moby-lost.txt
-rw-f--r-- scott scott 508925 paradise_lost.txt
```

#### 解压文件

##### `unzip`

解压 Zip 归包并不困难。要创建一个压缩归包，请使用 `zip` 命令；要解压该归包，请使用 `unzip` 命令。

```bash
$ unzip moby.zip

Archive: moby.zip

inflating: job.txt

inflating: moby-dick.txt

inflating: paradise_lost.txt
```

`unzip` 命令在执行工作时会告诉你它正在做什么。要获取更多信息，可以添加 `-v` 选项（代表 verbose，即详细输出）。

```bash
unzip -v moby.zip

Archive: moby.zip

Length Method Size Ratio CRC-32 Name
102519 Defl:X 65% fab86c9 job.txt
123674 Defl:X 487553 61% 34a8cc3a moby-dick.txt
508925 Defl:X 224004 56% 6a8ebd0f paradise_lost.txt
148018 747304 60%
3 files
```

这里包含很多有用数据，包括用于压缩文件的方法、原始文件与压缩文件大小的比例，以及用于错误纠正的循环冗余校验（CRC）。

##### 列出将被解压的文件

###### `-l`

有时你可能会发现自己看着一个 Zip 文件，但不记得里面有什么。或者你可能想确保你需要的某个文件包含在 Zip 文件中。在不解压的情况下列出 `zip` 文件的内容：

```bash
$ unzip -l moby.zip

Archive: moby.zip

Length Date Time Name
0 01-26-06 18:40 bible/
207254 01-26-06 18:40 bible/genesis.txt
102519 01-26-06 18:19 bible/job.txt
```



`123674 01-26-06 18:19 moby-dick.txt`

`508925 01-26-06 18:19 paradise_lost.txt`

`2055272 5 files`

从这些结果中，你可以看到 `moby.zip` 包含两个文件 `moby-dick.txt` 和 `paradise_lost.txt`，以及一个目录（`bible`），该目录本身包含两个文件：`genesis.txt` 和 `job.txt`。现在你确切知道在解压 `moby.zip` 时会发生什么。使用 `-l` 命令可以防止在无意中解压一个会喷出 100 个文件的文件，而不是在解压一个包含 100 个文件的目录。前者的结果会让你杂乱无章，而后者处理起来要容易得多。

# 测试将被解压的文件

`-t`

有时压缩归包会损坏。发现这种情况的最糟糕时机是你已经解压了归包并删除了它之后，结果发现部分甚至全部内容已损坏且无法打开。最好的办法是在实际解压之前，使用 `-t` 选项（代表 `test`）对归包进行测试。

```
$ unzip -t moby.zip

Archive: moby.zip

testing: bible/
testing: bible/genesis.txt OK
testing: bible/job.txt OK
testing: moby-dick.txt OK
testing: paradise_lost.txt OK

No errors detected in compressed data of moby.zip.
```

你真的应该在每次处理压缩文件时都使用 `-t`。这是明智的做法，尽管这可能会花费一些额外时间，但最终是值得的。

# 使用 gzip 归档和压缩文件

`gzip`

在某些方面，使用 `gzip` 比 `zip` 稍微简单一点。使用 `zip`，你需要指定新创建文件的名称，否则 `zip` 将无法工作；但使用 `gzip`，你只需要输入命令和想要压缩的文件名。

```
$ ls -l
-rw-r--r-- scott 508925 paradise_lost.txt

$ gzip paradise_lost.txt

$ ls -l
-rw-r--r-- scott 224425 paradise_lost.txt.gz
```

你应该意识到 `zip` 和 `gzip` 之间有一个巨大的区别：当你 `zip` 一个文件时，`zip` 会保留原始文件，你同时拥有原始文件和新的压缩文件；但当你 `gzip` 一个文件时，你只剩下新的压缩文件。原始文件消失了。

# 第二部分：操作文件

如果你想让 `gzip` 保留原始文件，你需要使用 `-c`（或 `--stdout`）选项，它会将 `gzip` 的结果输出到 shell，但你需要将该输出重定向到另一个文件。如果你使用了 `-c` 却忘记重定向输出，你就会得到这样的无意义内容：

```
$ gzip -c paradise_lost.txt
```

```
w'

I

, (3 i+MS3t1*eYO[g

D]d]Cg

R,rretrB3+3/|ODQs

-BAAqn,Y8*#]RU

*b'utm(-xYz3-o'~cn8K

```

不太好。输出到文件。

```
$ ls -l
-rw-r--r-- scott 508925 paradise_lost.txt

$ gzip -c paradise_lost.txt > paradise_lost.gz

$ ls -l
-rw-r--r-- scott 497K paradise_lost.txt
-rw-r--r-- scott 220K paradise_lost.txt
```

好多了。现在你同时拥有原始文件和压缩版本。

### 提示

如果你不小心在没有指定输出文件的情况下 `-c` 选项，只需按 Ctrl+C 直到 `gzip` 停止。

# 递归归档和压缩文件

如果你想对目录中的多个文件使用 `gzip`，只需使用通配符。你可能会压缩你认为的所有东西，看看这个示例：

```
$ ls -F
bible/ moby-dick.txt paradise_lost.txt

$ ls -l
-rw-r--r-- scott 1236574 moby-dick.txt
-rw-r--r-- scott 508925 paradise_lost.txt

bible:
-rw-r--r-- scott 207254 genesis.txt
```

注意通配符对 `bible` 目录内部的文件没有起任何作用，因为 `gzip` 默认不会进入子目录。要实现这一点，需要使用 `-r`（递归）选项。

```
$ ls -F
bible/ moby-dick.txt paradise_lost.txt

$ ls -l
-rw-r--r-- scott 1236574 moby-dick.txt
-rw-r--r-- scott 508925 paradise_lost.txt

bible:
-rw-r--r-- scott 207254 genesis.txt

$ gzip -r *

$ ls -l
-rw-r--r-- scott 1236574 moby-dick.txt.gz
-rw-r--r-- scott 508925 paradise_lost.txt.gz

bible:
-rw- 207254 genesis.txt.gz
```

这次子目录中的每个文件都被压缩了。然而，注意每个文件都是单独压缩的。要像使用 `zip` 命令那样将文件合并为一个大文件，你需要 `tar`，正如你在“使用 gzip 归档和压缩文件”中所看到的。

### 使用 gzip 获取最佳压缩

`-0–9`

和 `zip` 一样，你可以调整 `gzip` 使用的压缩级别。`gzip` 命令使用从 0 到 9 的量级，0 表示“完全不压缩”（正如你稍后会看到的），1 表示执行工作但压缩率不高，9 表示“压缩这些文件，我不介意等久一点”。默认是 6，但现代计算机的速度足够快，一直使用 9 也没问题。

```
$ ls -l
-rw-r--r-- scott 1236574 moby-dick.txt

$ gzip -c -1 moby-dick.txt > moby-dick.txt.gz

$ ls -l
-rw-r--r-- scott 1236574 moby-dick.txt

-rw-r--r-- scott scott 571005 moby-dick.txt.gz

$ gzip -c -9 moby-dick.txt > moby-dick.txt.gz

$ ls -l
-rw-r--r-- scott scott 487585 moby-dick.txt
```

由于 `gzip` 的工作方式，记得使用 `-c` 选项并将输出定向到实际的 `.gz` 文件，正如在“使用 gzip 归档”中所讨论的。

### 注意

如果你想得聪明点，可以在你的 `.bashrc` 文件中定义一个如下所示的别名：

```
alias gzip='gzip -9 '
```

这样你就会一直使用 `-9`，而无需考虑它。

# 解压缩用 gzip 压缩的文件

`gunzip`

使用 `gunzip` 命令从 `gzip` 归包中提取文件很容易的。

```
$ ls -l
-rw-r--r-- scott 224425 paradise_lost.txt.gz

$ gunzip paradise_lost.txt.gz > paradise_lost.txt

$ ls -l
-rw-r--r-- scott 508925 paradise_lost.txt
```

使用 `-c` 可能是一个好主意，特别是如果你打算保留 `.gz` 文件或将其传递给别人时。当然，你可以使用 `gzip` 创建自己的归档文件，但为什么要多费这番功夫呢？

### Note

如果你不喜欢 `gunzip` 命令，也可以使用 `gzip -d`（或 `--decompress` 或 `--uncompress`）。

## 用于 gunzip 解压的测试文件

`-t`

在使用 `gzip` 压缩文件（或多个文件）之前，你可能想验证它们能够正确解压而没有任何文件损坏。要做到这一点，请使用 `-t`（或 `--test`）选项。

```
$ gzip -t paradise_lost.txt.gz

$
```

没错：如果归包没有问题，`gzip` 不向你返回任何信息。如果有问题，你会知道；但如果没有问题，`gzip` 会保持沉默。这可能让人有点无所措，但这就是 Unix 系统的运行方式。它们通常只在出现你需要知道的问题时才会发出声音，而不是在一切运行正常的情况下如此。

## 使用 bzip2 归档和压缩文件

`bzip2`

如果你熟悉 `gzip`，那么使用 `bzip2` 会非常简单，因为 `bzip2` 的创建者故意让新命令的选项和行为与其前身尽可能相似。

```
$ ls -l
-rw-r--r-- scott scott 1236574 moby-dick.txt
```



```
$ bzip2 moby-dick.txt

$ ls -l

-rw-r--r-- scott scott 367248 moby-dick.txt.bz2
```

就像 `gzip` 一样，`bzip2` 只留下一个 `.bz` 文件。原始的 `moby-dick.txt` 消失了。要保留原始文件，请使用 `-c`（或 `--stdout`）并将输出重定向到以 `.bz2` 结尾的文件。

```
$ ls -l

-rw-r--r-- scott scott 1236574 moby-dick.txt
```

## 第二部分：处理文件

```
$ bzip2 -c moby-dick.txt moby-dick.txt.bz2

$ ls -l

-rw-r--r-- scott scott 1236574 moby-dick.txt

-rw-r--r-- scott scott 367248 moby-dick.txt.bz2
```

如果你回看“使用 `gzip` 归档和压缩文件”，你会发现 `gzip` 和 `bzip2` 极其相似，这是设计如此的。

## 使用 `bzip2` 获取尽可能的压缩率

与 `zip` 和 `gzip` 一样，你可以调整 `bzip2` 在工作时使用的压缩级别。`bzip2` 命令使用从 0 到 9 的比例，其中 0 表示“完全不压缩”（这类似于 `tar`，你将看到的），1 表示“快速完成工作，但压缩程度不高”，而 9 则表示“拼命压缩文件，我不介意多等一会来完成任务”。默认值是 6，但现代计算机足够快，一直使用 9 也是没问题的。

```
$ ls -l

-rw-r--r-- scott 1236574 moby-dick.txt

$ bzip2 -c moby-dick.txt > moby-dick.txt.bz2

$ ls -l

-rw-r--r-- scott 1236574 424084 moby-dick.txt.bz2

$ bzip2 -c 9 moby-dick.txt > moby-dick.txt.bz2

$ ls -l

-rw-r--r-- scott 1236574 367248 moby-dick.txt.bz2
```

从 424KB 变成使用 9 的 367KB——这差别很大！还要注意 `gzip` 和 `bzip2` 之间的文件大小差异。在 `-9` 下，`gzip` 将 `moby-dick.txt` 压缩到 488KB，而 `bzip2` 将其进一步压缩到 367KB。`bzip2` 命令明显比 `gzip` 命令慢，但在快速机器上，这意味着 `bzip2` 比 `gzip` 多花两到三秒，坦率说这没什么值得担心。

### Note

如果你愿意，可以在你的 `.bashrc` 文件中定义一个如下所示的别名：

```
alias bzip2='bzip2 -9'
```

这样你就会一直使用 `-9` 而不需要考虑它了。

## 解压缩用 `bzip2` 压缩的文件

#### `bunzip2`

正如 `bzip2` 被刻意设计为尽可能模拟 `gzip` 一样，`bunzip2` 的工作方式与 `gunzip` 非常相似。

```
$ ls -l

-rw-r--r-- scott scott 367248 moby-dick.txt.bz2

$ bunzip2 moby-dick.txt.bz2

$ ls -l

-rw-r--r-- scott scott 1236574 moby-dick.txt
```

你会发现 `bunzip2` 与 `gzip` 相似之处；两个命令都会删除原始文件，只留下解压缩后的结果。如果你想确保同时拥有压缩和未解压缩的文件，你需要使用 `-c`（或 `--stdout`）并将文件重定向到你想要的文件。

```
$ ls -l

-rw-r--r-- scott scott 367248 moby-dick.txt.bz2

$ bunzip2 -c moby-dick.txt.bz2 > moby-dick.txt

$ ls -l

-rw-r--r-- scott scott 1236574 moby-dick.txt

-rw-f--r-- scott scott 367248 moby-dick.bz2
```

命令之间相互复制选项和行为是一件好事，因为这让它们更容易学习。事实上，`bzip2` 和 `bunzip2` 的创建者非常有远见。

### Note

如果你不喜欢 `bunzip2`，也可以使用 `bzip2 -d`（或 `--decompress` 或 `--uncompress`）。

## 用于 `bunzip2` 解压的测试文件

在使用 `bunzip2` 处理文件（或文件）之前，你可能想验证它们能够在无任何文件损坏的情况下正确解压。要做到这一点，请使用 `-t`（或 `--test`）选项。

```
$ bunzip2 -t paradise_lost.txt.bz2
```

## 第二部分：处理文件

就像 `gunzip` 一样，如果归包没有问题，`bunzip2` 不会向你报告任何信息。如果有问题，你会知道；但如果没有问题，`bunzip2` 会保持沉默。

### 使用 `tar` 归档文件

记住，`tar` 不进行压缩；它只是归档（生成的归包被称为 tarball）。相反，`tar` 使用其他程序（如 `gzip` 或 `bzip2`）来压缩它创建的归包。即使你不压缩，仍然使用相同的基本选项：`-c`（或 `--create`）告诉 `tar` 你正在创建一个 tarball，以及 `-f`（或 `--file`）指定 tarball 的文件名。

```
$ ls -l

scott 102519 job.txt

scott 1236574 moby-dick.txt

scott 508925 paradise_lost.txt

$ tar -cf moby-dick.tar *

$ ls -l

scott 102519 job.txt

scott 1236574 moby-dick.txt

scott 1853440 moby-dick.tar

scott 508925 paradise_lost.txt
```

注意三点：首先，将 `job.txt`、`moby-dick.txt` 和 `paradise_lost.txt` 的大小相加，得到 1848018 字节。将其与 `moby.tar` 的大小比较。记住 `tar` 是归档工具而不是压缩工具，所以结果与单个文件的总和相同，只有为了跟踪 tarball 内容的开销。其次，`tar` 与 `gzip` 和 `bzip2` 不同，它会保留原始文件。考虑到 `tar` 作为备份工具的行为，这并不意外。`tar` 的真正在于它设计用于压缩整个目录结构，因此你可以一次归档大量的文件和目录。

```
$ ls -lf

drwxr-xr-x scott 168 moby-dick/

$ ls -lf moby-dick/*

scott 102519 moby-dick/job.txt

scott 1236574 moby-dick/moby-dick.txt

scott 508925 moby-dick/paradise_lost.txt

moby-dick/bible:

scott 207254 genesis.txt

scott 102519 job.txt/

$ tar -cf moby.tar

$ ls -lf

drwxr-xr-x scott 168 moby-dick/

21700880 moby.tar
```

`tar` 命令已经存在很久了，原因显而易见：它太实用了！当你开始考虑压缩工具时，它会变得更好，正如你在下一节看到的。

### 使用 `tar` 和 `gzip` 归档并压缩文件

如果你回看“使用 `gzip` 归档和压缩文件”和“`bzip2` 归档和压缩文件”并思考讨论的内容，可能会发现一个问题。如果你想压缩一个包含 100 个位于各个子目录文件的目录怎么办？如果你使用 `gzip` 或 `bzip2` 并配合 `-r`（递归）选项，你将得到 100 个单独压缩的文件，每个文件都整齐地存储在自己的子目录中。这无疑不是你想要的。你如何向电子邮件附带 100 个 `.gz` 或 `.bzip2` 文件？这不可能！

这就是 `tar` 派上用场的地方。首先，使用 `tar` 归档目录及其内容（位于各个子目录中的 100 个文件），然后使用 `gzip` 或 `bzip2` 压缩生成的 `tar` 文件。由于 `gzip` 是与 `tar` 配合常用的压缩程序，我们将关注它。

你可以这样操作：

```
$ ls -l moby-dick/

scott scott 102519 moby-dick/job.txt

scott scott 1236574 moby-dick/moby-dick.txt

scott scott 508925 moby-dick/paradise_lost.txt

moby-dick/bible:
```



## 第一部分：使用 tar 和 gzip

`scott` `207254` `genesis.txt`

`scott` `102519` `job.txt`

```
$ tar -cf moby.tar moby-dick/ | gzip -c > moby.tar.gz

$ ls -l
scott scott 168 moby-dick/
scott 20 moby.tar.gz
```

这种方法可行，但打字太麻烦了！有一种更简单的方法应该是你的默认选择。它涉及 `tar` 的两个选项：`-z`（或 `--gzip`），它在 `tar` 内部调用 `gzip`，无需你手动操作；`-v`（或 `--verbose`），这并不是必需的，但总是有用，因为它能让你知道 `tar` 在运行运行时正在做什么。

```
$ ls -l moby-dick/
scott 102519 moby-dick/job.txt
scott 1236574 moby-dick/moby-dick.txt
scott 508925 moby-dick/paradise_lost.txt
moby-dick/bible:
scott 207254 genesis.txt
scott 102519 job.txt

$ tar -zcf moby.tar.gz moby-dick/
moby-dick/
moby-dick/job.txt
moby-dick/bible/
moby-dick/bible/genesis.txt
moby-dick/bible/job.txt
moby-dick/moby-dick.txt
moby-dick/paradise_lost.txt
```

## 第二部分：文件操作

`scott` `scott` `846049` `moby.tar.gz`

对于使用了 `tar` 命令后又使用 `gzip` 命令处理的文件，通常扩展名是 `.tar.gz`；不过，如果你喜欢，也可以使用 `.tgz` 和 `.tar.zip`。

### 注意

完全可以使用 `bzip2` 代替 `gzip` 配合 `tar` 使用。你的命令看起来如下（注意 `-j` 选项，这里是 `bzip2` 起作用的地方）：

```
$ tar -jcvf moby.tar.bz2 moby-dick/
```

在这种情况下，扩展名应该是 `.tar.bz2`，尽管你也可以使用 `.tar.bzip2`、`.tbz2` 或 `.tbz`。是的，如果使用 `gzip` 或 `bzip2` 让你感到非常困惑，它们都可能导致生成以 `.tbz` 结尾的文件。这有力地支持了使用该特定扩展之外的任何名称，以最大限度地减少混乱。

## 测试将要解压和解压缩的文件

```
$ tar -zvtf moby.tar.gz
```

在拆解 `tar` 包（无论其是否也使用了 `gzip` 压缩）之前，对其进行测试是一个非常好的主意。首先，如果 `tar` 包损坏了，可以避免在文件看起来无法工作时让你抓狂掉头发。其次，如果你知道创建 `tar` 包的人体贴地打包了一个包含 100 个文件的目录，或者在无意中打包了 100 个独立文件，那么你就要面对桌面被扫地的局面了。

要测试你的 `tar` 包（假设它也用 `gzip` 压缩过），请使用 `-t`（或 `--list`）选项。

```
$ tar -zvtf moby.tar.gz
scott/scott 0 moby-dick/
scott/scott 102519 moby-dick/job.txt
scott/scott 0 moby-dick/bible/
scott/scott 207354 moby-dick/bible/genesis.txt
scott/scott 102519 moby-dick/job.txt
scott/scott 1236574 moby-dick/moby-dick.txt
scott/scott 508925 moby-dick/paradise_lost.txt
```

这会告诉你每个文件的权限、所有者、文件大小和日期。此外，由于每一行都以 `moby-dick/` 开头，你可以看到你将得到一个包含 `tar` 包所有文件和目录的目录，这让人松了一口气。

确保 `-f` 是在你指定 `.tar.gz` 文件名之前的最后一个选项。如果你不这样做，`tar` 会报错：

```
$ tar -zvft moby.tar.gz
tar: You must specify one of the '-Acdutx' options
try 'tar --help' or 'tar --usage' for more information.
```

现在，既然你已经确保你的 `.tar.gz` 文件没有损坏，是时候真正打开它了，正如你将在下一节中看到的那样。

### 注意

如果你正在测试一个使用 `bzip2` 压缩的 `tar` 包，只需使用此命令即可：

```
$ tar -jvtf moby.tar.bz2
```

## 解压并解压缩文件

```
$ tar -zxvf moby.tar.gz
```

要创建一个 `.tar.gz` 文件，你使用了一组选项：`-zcvf`。要解压并解压缩生成的文件，你只需要进行一个替换：用 `-x`（或 `--extract`）替换 `-c`（或 `--create`）。

```
$ ls -l
granneanne rsgranne 84649 moby.tar.gz

$ tar -zvf moby.tar.gz
moby-dick/
moby-dick/job.txt
moby-dick/bible/
moby-dick/bible/genesis.txt
moby-dick/bible/job.txt
moby-dick/moby-dick.txt
moby-dick/paradise_lost.txt

$ ls -l
rsgranne rsgranne 168 moby-dick
rsgranne rsgranne 84649 moby.tar.gz
```

确保你在打开文件之前总是对其进行测试，正如上一节“测试将要解压和解压缩的文件”中所提到的。这意味着你应该运行的命令顺序看起来如下：

```
$ tar -zvft moby.tar.gz
$ tar -zxvf moby.tar.gz
```

### 注意

如果你正在打开一个使用 `bzip2` 压缩的 `tar` 包，只需使用此命令即可：

```
$ tar -jxvf moby.tar.bz2
```

### 结论

在那个拨号器缓慢、硬盘很小的年代，归档和压缩是必须的。在今天，这更多是一种便利，但你仍然会发现自己一直在使用它们。例如，如果你下载了源代码进行编译，你很可能会面对一个诸如 `sourcecode.tar.gz` 这样的文件。在未来，你可能会看到越来越多以 `.tar.bz2` 结尾的文件。如果你与 Windows 用户交换文件，你会遇到许多以 `.zip` 结尾的文件。学习使用你的归档和压缩工具，因为你使用它们的频率比你想象的要高得多。

# 第三部分：寻找内容

```
/txt/rider_haggard/Queen_of_the_Dawn.txt
/txt/rider_haggard/Allan_and_the_Ice-Gods.txt
/txt/rider_haggard/Heu-Heu_or_The_Monster.txt
/txt/rider_Haggard
/txt/Rider_Haggard/King_Solomons_Mines.txt
/txt/Rider_Haggard/Quaternaim.txt
```

事实证明，艾伦·哈加德（Allan Haggard）可用的小说比他最初看起来要多。记住，当你想要最大化定位结果时要使用 `-i` 参数，否则你可能会错过你想要查找的重要文件和文件夹。

### 注意

关于 H. 莱德·哈加德（H. Rider Haggard），请参见 `http://en.wikipedia.org/wiki/Rider_Haggard`。他是一位很有趣（尽管有些过时）作家。

## 管理搜索文件名数据库时收到的结果

`-n`

如果你经常使用 `locate`，最终你会遇到这样的情况：

```
$ locate pdf
/etc/cups/pdftops.conf
/etc/xpdf
/etc/xpdf/xpdfrc-latin2
```

在这台电脑上，我们得到了 2,373 条结果。太多了！最好用下面这种结构：

```
$ locate pdf | less
```

将你的 `locate` 搜索输出通过管道传给分页器 `less`（这在“第 5 章：一次查看一个屏幕的文本文件”中已经介绍过），这样你就可以每次处理一个屏幕，来查看这 2,373 条结果。

如果你想查看前 x 个结果（其中 x 是你选择的整数），请使用 `-n` 参数，后面紧跟你想看到的结果数量。

```
$ locate -n 3 pdf
/etc/cups/pdftops.conf
/etc/xpdf
/etc/xpdf/xpdfrc-latin2
```



# 4

这要容易得多，而且可能就是你需要的全部。不要让 `locate` 向你倾泻如洪水般的结果；相反，要控制 `locate` 命令的输出并利用它为自己服务。

## 更新 locate 使用的数据库

`updateddb`

在本章介绍 `locate` 的第一部分“搜索文件名数据库”中提到，该命令之所以如此快速，是因为它实际上是在搜索一个包含你机器文件和目录名称的数据库。当安装 `locate` 时，它会自动设为扫描你的硬盘并在白天更新该数据库。这样做是为了方便，但如果你需要找到你刚刚放在电脑上的文件，这可就不太妙了。

例如，如果你安装了 Rootkit Hunter（一个用于寻找 rootkit——即坏人用来控制你 Linux 的后门程序的程序），然后你想查看该程序安装的文件？`locate` 命令将无法为你提供帮助，因为它并不知道这些文件，并且在数据库被 `updateddb` 更新之前，它不会知道这些文件。由于该命令会索引你电脑上的每个文件和文件夹，因此你需要运行它（或者在 Linux/Ubuntu 等不鼓励使用 root 用户的发行版上使用 `sudo`）。

```
# apt-get install rkhunter

# exit

$ locate rkhunter

$ su

$ updateddb

# exit

$ locate rkhunter

/usr/local/rkhunter

/usr/local/rkhunter/bin

/usr/local/rkhunter/etc
```

在前面的命令中，你首先安装了 `rkhunter`（Rootkit Hunter 的包名），然后退出 root。搜索 `rkhunter`，但找不到它。你再次变为 root，运行 `updateddb` 扫描硬盘并让 `locate` 知道任何变化，然后退出 root。最后，再次用 `locate` 查找 `rkhunter`，这次你成功了。

你需要注意的一点是：`updateddb` 的运行速度与硬盘上的内容以及电脑的速度成正比。快速处理器、快速硬盘和少量文件？那么 `updateddb` 会运行得很快。如果你有一个慢速的 CPU、5400RPM 的硬盘和百万个文件？请预计 `updateddb` 将花费相当长。如果你想知道运行需要多久，可以在 `updateddb` 前加上 `time` 命令，如下所示：

```
# time updateddb
```

当 `updateddb` 完成时，`time` 会告诉你整理好 `locate` 数据库花了多久。这些信息记在心里很有用，以防你以后需要使用 `updateddb` 且时间紧迫。

### 注意

`updateddb` 命令与运行 `slocate -u` 完全相同，而且 `updateddb` 实际上是 `slocate` 的一个链接，你可以很容易地看到这一点。

```
$ ls -l /usr/bin/updateddb -> slocate
```

## 在文本文件中内部搜索模式

`grep`

`locate` 命令搜索文件和目录的名称，但它不能搜索这些文件的内部。要做到这一点，你需要使用 `grep`。基本上，你给 `grep` 提供一个你想要搜索的模式，将其指向你想要搜索的文件或一组文件（甚至是整个硬盘），然后 `grep` 会输出匹配你模式的行列表。

```
$ grep pain three_no_more_forever.txt

all and in pain
```

在这种情况下，你使用 `grep` 来查看 `pain` 这个词是否出现在一个包含 Peter Mhlen 创作的名为《永不再三个》（Three More Forever）诗歌的文件中。果其然，`pain` 这个词在文件中，所以 `grep` 打印出包含你搜索词的行。但如果你想同时查看 Peter 的几首诗呢？通配符来救场了！

```
$ grep pain *

fiery inferno in space.txt:which the

three_no_more_forever.txt:all and in

the speed of morning.txt:of a

hour a day.txt:nice job

ghost pain.txt:Subject: ghost pain
```

注意 `grep` 找到的是整个字符串，包括 `painting`。还要注意 `grep` 如何显示包含该术语的文件名以及包含该术语的行。到目前为止，用 `grep` 搜索文件内部是相当简单的，正如你将在后续章节中发现的那样。

## 在文本文件中内部搜索模式的基础

在上一节中，你学习了 `grep` 是通过在一组文件中搜索模式来工作的。你第一次使用 `grep` 非常基础，但现在你需要变得更复杂一点了，为了做到这一点，你需要理解 Linux 工具箱中最强大的工具之一：正则表达式，或 `regex`。为了充分利用 `grep` 的作用，你真的需要了解正则表达式；然而，正则表达式本身就是一本书，所以我们在这里只涵盖基础知识。

### 提示

想了解更多关于正则表达式的知识吗？[正则表达式入门 (Learn GNU Regular Expressions)](https://en.wikipedia.org/wiki/Regular_expression) 是一本很好的书。如果你想了解更多，可以查看 [正则表达式百科](https://en.wikipedia.org/wiki/Regular_expression)。

### 9.1 grep 的不同版本

| 模式 | 命令 | 说明 |
|---|---|---|
| 基础正则表达式 | `grep` | `grep` (Basic) |
| 扩展正则表达式 | `grep -E` | `egrep` |
| 固定字符串 | `grep -F` | `fgrep` |
| Perl 兼容的正则表达式 | `grep -P` | `pgrep` |

*(注：原文中重复出现的表格和段落已根据指令去重。)*

### 9.1 grep 的不同版本

*(注：此处保留原结构标题，但内容已在上文去重展示。)*

## 管理搜索文件名数据库时收到的结果

`-n`

如果你经常使用 `locate`，最终你会遇到这样的情况：

```
$ locate pdf

/etc/cups/pdftops.conf

/etc/xpdf

/etc/xpdf/xpdfrc-latin2
```

*(注：以下内容为原文中位于不同位置但逻辑上相关的片段整理)*

# 第三部分：寻找内容

```
/txt/rider_haggard/Queen_of_the_Dawn.txt
/txt/rider_haggard/Allan_and_the_Ice-Gods.txt
/txt/rider_haggard/Heu-Heu_or_The_Monster.txt
/txt/rider_Haggard
/txt/Rider_Haggard/King_Solomons_Mines.txt
/txt/Rider_Haggard/Quaternaim.txt
```

事实证明，艾伦·哈加德（Allan Haggard）可用的小说比他最初看起来要多。记住，当你想要最大化定位结果时要使用 `-i` 参数，否则你可能会错过你想要查找的重要文件和文件夹。

### 注意

关于 H. 莱德·哈加德（H. Rider Haggard），请参见 `http://en.wikipedia.org/wiki/Rider_Haggard`。他是一位很有趣（尽管有些过时）作家。

## 管理搜索文件名数据库时收到的结果

`-n`

如果你经常使用 `locate`，最终你会遇到这样的情况：

```
$ locate pdf

/etc/cups/pdftops.conf

/etc/xpdf

/etc/xpdf/xpdfrc-latin2
```



# 4. 控制输出与更新数据库

在这台电脑上，我们得到了 2,373 条结果。太多了！最好用下面这种结构：

```
$ locate pdf | less
```

将你的 `locate` 搜索输出通过管道传给分页器 `less`（这在“第 5 章：一次查看一个屏幕的文本文件”中已经介绍过），这样你就可以每次处理一个屏幕，来查看这 2,373 条结果。

如果你想查看前 `x` 个结果（其中 `x` 是你选择的整数），请使用 `-n` 参数，后面紧跟你想看到的结果数量。

```
$ locate -n 3 pdf

/etc/cups/pdftops.conf

/etc/xpdf

/etc/xpdf/xpdfrc-latin2
```

这要容易得多，而且可能就是你需要的全部。不要让 `locate` 向你倾泻如洪水般的结果；相反，要控制 `locate` 命令的输出并利用它为自己服务。

## 更新 `locate` 使用的数据库：`updateddb`

在本章介绍 `locate` 的第一部分“搜索文件名数据库”中提到，该命令之所以如此快速，是因为它实际上是在搜索一个包含你机器文件和目录名称的数据库。当安装 `locate` 时，它会自动设为扫描你的硬盘并在白天更新该数据库。这样做是为了方便，但如果你需要找到你刚刚放在电脑上的文件，这可就不太妙了。

例如，如果你安装了 `Rootkit Hunter`（一个用于寻找 `rootkit`——即坏人用来控制你 `Linux` 的后门程序），然后你想查看该程序安装的文件？`locate` 命令将无法为你提供帮助，因为它并不知道这些文件，并且在数据库被 `updateddb` 更新之前，它不会知道这些文件。由于该命令会索引你电脑上的每个文件和文件夹，因此你需要运行它（或者在 `Linux`/`Ubuntu` 等不鼓励使用 `root` 用户的发行版上使用 `sudo`）。

```
# apt-get install rkhunter

# exit

$ locate rkhunter

$ su

$ updateddb

# exit

$ locate rkhunter

/usr/local/rkhunter

/usr/local/rkhunter/bin

/usr/local/rkhunter/etc
```

在前面的命令中，你首先安装了 `rkhunter`（`Rootkit Hunter` 的包名），然后退出 `root`。搜索 `rkhunter`，但找不到它。你再次变为 `root`，运行 `updateddb` 扫描硬盘并让 `locate` 知道任何变化，然后退出 `root`。最后，再次用 `locate` 查找 `rkhunter`，这次你成功了。

你需要注意的一点是：`updateddb` 的运行速度与硬盘上的内容以及电脑的速度成正比。获取快速处理器、快速硬盘和少量文件？那么 `updateddb` 会运行得很快。如果你有一个慢速的 `CPU`、5400`RPM` 的硬盘和百万个文件？请预计 `updateddb` 将花费相当长。如果你想知道运行需要多久，可以在 `updateddb` 前加上 `time` 命令，如下所示：

```
# time updateddb
```

当 `updateddb` 完成时，`time` 会告诉你整理好 `locate` 数据库花了多久。这些信息记在心里很有用，以防你以后需要使用 `updateddb` 且时间紧迫。

### 注意

`updateddb` 命令与运行 `slocate -u` 完全相同，而且 `updateddb` 实际上是 `slocate` 的一个链接，你可以很容易地看到这一点。

```
$ ls -l /usr/bin/updateddb -> slocate
```

## 在文本文件中内部搜索模式：`grep`

`locate` 命令搜索文件和目录的名称，但它不能搜索这些文件的内部。要做到这一点，你需要使用 `grep`。基本上，你给 `grep` 提供一个你想要搜索的模式，将其指向你想要搜索的文件或一组文件（甚至是整个硬盘），然后 `grep` 会输出匹配你模式的行列表。

```
$ grep pain three_no_more_forever.txt

all and in pain
```

在这种情况下，你使用 `grep` 来查看 `pain` 这个词是否出现在一个包含 `Peter Mhlen` 创作的名为《永不再三个》（`Three More Forever`）诗歌的文件中。果其然，`pain` 这个词在文件中，所以 `grep` 打印出包含你搜索词的行。但如果你想同时查看 `Peter` 的几首诗呢？通配符来救场了！

```
$ grep pain *

fiery_inferno_in_space.txt:which the

three_no_more_forever.txt:all and in

the_speed_of_morning.txt:of a

hour_a_day.txt:nice job

ghost_pain.txt:Subject: ghost pain
```

注意 `grep` 找到的是整个字符串，包括 `painting`。还要注意 `grep` 如何显示包含该术语的文件名以及包含该术语的行。到目前为止，用 `grep` 搜索文件内部是相当简单的，正如你将在后续章节中发现的那样。

## 在文本文件中内部搜索模式的基础

在上一节中，你学习了 `grep` 是通过在一组文件中搜索模式来工作的。你第一次使用 `grep` 极其基础，但现在你需要变得更复杂一点了，为了做到这一点，你需要了解 `Linux` 工具箱中最强大的工具之一：正则表达式，或 `regex`。为了充分利用 `grep` 的作用，你真的需要了解正则表达式；然而，正则表达式本身就是一本书，所以我们在这里只涵盖基础知识。

### 提示

想了解更多关于正则表达式的知识吗？[正则表达式入门 (Learn GNU Regular Expressions)](https://en.wikipedia.org/wiki/Regular_expression) 是一本很好的书。如果你想了解更多，可以查看 [正则表达式百科](https://en.wikipedia.org/wiki/Regular_expression)。

### 9.1 `grep` 的不同版本

| 模式 | 命令 | 说明 |
|---|---|---|
| 基础正则表达式 | `grep` | `grep` (Basic) |
| 扩展正则表达式 | `grep -E` | `egrep` |
| 固定字符串 | `grep -F` | `fgrep` |
| Perl 兼容的正则表达式 | `grep -P` | `pgrep` |

后面紧跟一个进程 ID（`PID`）数字，它代表你运行过的更早的命令，例如 `!264`。

在这里，`bash` 看到了 `!`，在它后面寻找 `PID`，然后抱怨说找不到名为 `" *"`（一个双引号、一个空格和一个星号）的早期命令，这确实是一个非常奇怪的命令。

事实证明，引号表示你在搜索词中使用了变量，而这实际上并不是你想要的。所以双引号不起作用。让我们尝试使用单引号。

```
$ grep 'hey'

txt/pvzm@ hours_a_day.txt:hey you let's run!
```

结果好得多！单引号告诉 `grep` 你的搜索词中不包含任何 `shell` 变量，只是你想要匹配的一串字符。你瞧吧，出现了一条结果，正是你想要的那个。

教训是什么？知道什么时候该用单引号，什么时候用双引号，以及什么时候都不用。如果你正在搜索精确匹配，请使用单引号；但如果你想将 `shell` 变量整合到搜索词中，请使用双引号。如果你正在搜索一个包含数字和字母的单个单词，完全省略所有引号也是安全的。如果你想稳妥起见，尽管使用单引号吧，即使是在单个单词周围也没害。

## 在文件中递归搜索文本

```bash
-R
```

通配符 `*` 允许你搜索同一目录下的多个文件，但若要同时搜索多个子目录，你需要 `-R`（或 `--recursive`）选项。让我们在一堆老派（但仍然精彩！）的故事中寻找 `hideous` 这个词，它是 19 世纪和 20 世纪初恐怖小说作者的喜爱。

```
$ grep -R hideous *

machen/great_god_pan.txt:know, not in
your most fantastic, hideous dreams you can have
machen/great_god_pan.txt:hideously
contorted in the entire course of my practice, and I
machen/everpan.txt:death was
horrible. The blackened face, the hideous form upon
lovecraft/Beyond the Wall of Sleep.txt:blant over
unknown wrong, which
lovecraft/Beyond the Wall of Sleep:the hideous face, and awakened the nurse.
```



`lovecraft/Call of Cthulhu.txt:a chain. I think they, professor, too, intended to`

`lovecraft/Call of Cthulhu.txt:voodoo meeting; and so singular and hideous were the rites`

`lovecraft/Call of Cthulhu.txt:stated, a very crude base-relief of stone, comprising a hideous...`

# 第三部分：寻找内容

提示

当然，如果你得到太多结果，你应该将结果通过管道交给 `less`，就像你之前在“管理搜索文件名数据库时收到的结果”中所做的那样：

```
$ grep -R hideous | less
```

另一种策略是将命令的输出发送到文本文件，然后用你喜欢的任何文本编辑器打开该文件：

```
$ grep -R hideous > hideous_in_horror.txt
```

这是一种搜索并存储结果的好方法，以防日后之需。

# 在文件中搜索忽略大小写大小的文本

`-i`

默认情况下，使用 `grep` 执行的搜索是区分大小写大小的。在上一节中，你在 `H.P.` 洛夫克拉夫特的故事中搜索了单词 `hideous`（该作者喜爱的词）。但 `Hideous` 呢？

```
$ grep h_p_lovecraft/*

h_p_lovecraft/the_whisper_in_darkness.txt: them.
Hideous though the idea was, I knew...
```

你对 `hideous` 的搜索找到了 463 条结果（哇！），而 `Hideous` 返回了一个。有办法能把它们合并起来吗？使用 `-i`（或 `--ignore-case`）选项，你可以同时搜索两者，还会搜索 `HideDeUs`、`HIDEOUS` 以及所有可能的组合。

```
$ grep h_p_lovecraft/*

h_p_lovecraft/Call of Cthhu.txt:voodoo meeting;
so singular and hideous were the rites
h_p_lovecraft/Call of Cthhu.txt:stated, a very
crude bas-relief of stone, comprising a hideous
h_p_lovecraft/the_whisper_in_darkness.txt: them.
Hideous though the idea was, I knew...
```

请记住，你可能会增加获得的结果数量，甚至可能增加一个数量级。如果这是一个问题，请查看上一节末尾的提示，以获得关于处理它的建议。

# 第三部分：寻找内容

# 在文件中仅搜索整个单词

`-w`

回想一下早的章节“在文本文件中搜索模式的基础”，你在那里第一次学习了 `grep`。你搜索了单词 `pain`，`grep` 顺从地返回了一个列表，显示 `pain` 被使用的地方。

```
$ grep pain *

fiery in space.txt:watch the paint peel,
three_no_more_forever.txt:all alone and in pain
the speed of morning.txt:of a Chinese painting.
8 day.txt:nice paint job too
ghost pain.txt:Subject: ghost pain
```

默认情况下，`grep` 搜索字符串 `pain` 的所有出现处，显示包含 `pain` 的行，但也包括 `painting` 和 `faint`。如果 `painless`、`Spain` 或 `painstaking` 出现在被搜索的某个文件中，行也会很好地显示它们。但如果你只想要包含精确单词的行，请使用 `-w` 选项。如果你想保险，即使是针对单个单词也可以加上引号。

```
$ grep -w pain *

three_no_more_forever.txt:all alone and in
ghost pain.txt:Subject: ghost pain
```

当你收到太多搜索结果时，这个选项真的可以帮助缩小搜索范围。

# 显示文件中单词出现的行号

`-n`

`grep` 命令显示包含你正在搜索的术语的行，但它并没有告诉你在文件中的具体位置。要找到行号，请利用 `-n`（或 `--line-number`）选项。

```
$ grep -n pain *

fiery in space.txt:56:watch the paint peel,
three_no_more_forever.txt:19:all alone and in
the speed of morning.txt:66:of a Chinese painting.
8 day.txt:78:nice paint job too
ghost pain.txt:32:Subject: pain
```

现在你知道每个 `pain` 实例行号，在任何文本编辑器中直接跳转到那些行就很简单了。

# 为其他命令的输出搜索特定单词

```
$ ls -l | grep 1960
```

`grep` 命令在单独使用时很强大，但当你将其作为其他程序输出的过滤器时，它就变得非常灵活了。例如，假设你有所有 `Coltrane` 的专辑组织在单独文件夹中（`Coltrane` 是开头）。部分列表可能像这样（使用了 `ls -l`，所以有一个结果）：

```
$ ls -l

1956_Coltrane_For_Lovers
1957_Blue_Train
1957_Coltrane_Lush_Life
1957_The_Monk_With_Coltrane
```

现在，如果你只想看 1960 年发布的专辑列表呢？将 `ls` 的输出交给 `grep`，你几秒钟就能得到答案。

```
$ ls -l | grep 1960

1960_Coltrane_Plays_The_Blues
1960_Coltrane's_Sound
1960_Giant_Steps
1960_My_Favorite_Things
```

在开始思考之后，你会发现这种方法有数百种 `grep` 的用法。这里另一个强大的用法：`ps` 命令列出运行中的进程，而 `-f` 选项让 `ps` 提供完整的列表，带有关于每个进程的大量信息，`-U` 选项后面跟着用户名限制输出为该用户。通常 `ps -U scott` 会导致一个很长的列表，如果你在寻找特定进程的信息。通过 `grep`，你可以轻松限制输出。

注意

为了节省空间，通常通过 `ps` 看到的某些信息被删除了。

```
$ ps -U scott | grep firefox

scott 17623 /bin/sh/opt/firefox/firefox
scott 17634 firefox-bin
```

`ps` 命令列出了 `scott` 用户的所有命令（事实上），但将该输出交给 `grep`，它只列出了包含单词 `firefox` 的行。遗憾的是，输出的最后一行是错误的：你只想看到真实的 `Firefox`，而不是使用 `grep` 搜索 `firefox`。要在 `grep` 结果中隐藏对 `firefox` 的搜索，尝试这个：

```
$ ps -U scott | grep -v firefox

scott 17623 /bin/sh/opt/firefox/firefox
scott 17634 /opt/firefox-bin
```

# 第三部分：寻找内容

现在你的 `grep` 搜索词使用了正则表达式范围，从 `f` 到 `f`，在 `ps` 运行的那些行中找到了 `firefox`：然而，它没有匹配 `grep` 的行，因为那行实际上是 `[firefox]`，这应该是匹配的。这里的 `grep` 命令无法匹配原始的 `ps -ef | grep [firefox]`，因为它包含了 `|`，而 `[firefox]` 的搜索解析为搜索精确单词 `firefox`。这有点让人困惑，但如果你自己尝试并思考，它就通了。总之，它是有效的。试试吧！

# 查看文件中单词的上下文

`-A`, `-B`, `-C`

在处理数据时，上下文就是。正如你所学的，`grep` 输出包含搜索词的实际行，但你也可以告诉 `grep` 包含前后的行。在最后一节“为其他命令的输出搜索特定单词”中，你使用 `grep` 处理 `John Coltrane` 专辑列表。其中之一是 `A Love Supreme`。在它之前出了哪三个？要获得答案，使用 `-B`（或 `--context=#`）。

```
$ ls -l | grep -B 3 A_Love_Supreme

1963_Impressions
1963_John_Coltrane&Johnny_Hartman
```



`1963_Live_At_Birdland`

`1964_A_Love_Supreme`

```
如果你想找到 `A Love Supreme` 之后的是什么，请使用 `-A`（或 `--after-context=#`）选项。

$ ls -l | grep -A 3 'A_Love_Supreme'

1964_A_Love_Supreme

1964_Coltrane's_Sound

1964_Crescent

1965_Ascension
```

要获取 `A Love Supreme` 的完整历史背景，尝试 `-C`（或 `--context=#`）选项，它将前后行结合在一起。

```
$ ls -l | grep -C 2 'A_Love_Supreme'

1963_John_Coltrane&_Johnny_Hartman

1963_Live_At_Birdland

1964_A_Love_Supreme

1964_Coltrane's_Sound

1964_Crescent
```

## 第三部分：查找内容

```bash
$ ls -1 | grep -c Live

1963_John_Coltrane&_Johnny_Hartman

1963_Live_At_Birdland

1964_A_Love_Supreme

----

1965_Last_Trane

1965_Live_in_Seattle

1965_Major_Works_of_John_Coltrane

----

1965_Transition

1966_Live_at_the_Village_Vanguard_Again!

1966_Live_in_Japan

1967_Expression

1967_Olatunji_Concert_Last_Live_Recording

1967_Stellar_Regions
```

`---` 用于分隔每个匹配组。前两组结果显然是标题中包含 `Live`，而紧随其后和几乎最后的组则稍微复杂一些。几行包含单词 `Live` 的专辑挨在一起，因此结果聚集在了一起。这看起来可能有点奇怪，但如果你观察每一行，你会发现匹配行前后的专辑也在列表中。

如果加入 `-n` 选项，结果会更加详细，它会列出行号（因为你使用了 `-1`，这是 `ls` 列表的行号）。

```bash
$ ls -1 | grep -n c Live

37-1963_John_Coltrane&_Johnny_Hartman

38-1963_Live_At_Birdland

39-1964_A_Love_Supreme

----

48-1965_Last_Trane

49-1965_Live_in_Seattle

50-1965_Major_Works_of_John_Coltrane

----

52-1965_Transition

53-1966_Live_at_the_Village_Vanguard_Again!

54-1966_Live_in_Japan

55-1967_Expression

56-1967_Olatunji_Concert_Last_Live_Recording

57-1967_Stellar_Regions
```

现在 `-C` 为你提供了关于每行的更多信息，如行号前的字符 `-` 所示。`:` 表示该行匹配成功，`-` 表示它是匹配项之前或之后的行。第 54 行 `1966_Live_in_Japan` 承担了双重职责。它位于 `1966_Live_at_the_Village_Vanguard_Again!` 之后，这意味着它本应该有一个 `-`，但它本身也是一个匹配项，因此需要一个 `:`。由于匹配项更重要，所以它胜出，最终使用的是 `:`。

## 显示文件中不包含某些单词的行

在爵士乐界，约翰·科特兰（John Coltrane）在去世近40年后仍占据着统治地位；同样，齐飞乐队（Led Zeppelin）也被认为是历史上最伟大的摇滚乐队之一。在活跃期间，齐飞乐队发行了九张专辑；然而，其中许多专辑的标题中包含了乐队名称（第四张没有标题，但大多数评论家将其识别为《齐飞乐队 IV》，所以也是如此）。如果你想查看包含齐飞乐队专辑的 MP3 文件夹列表，但排除那些实际上确实包含“Led Zeppelin”单词的文件夹怎么办？使用 `-v` 或 `--invert-match` 选项，你可以只显示不包含这些内容的结果：

```bash
$ ls -l

1969_Led_Zeppelin

1969_Led_Zeppelin_II

1970_Led_Zeppelin_III

1971_Led_Zeppelin_IV

1973_Houses_Of_The_Holy

1975_Physical_Graffiti

1976_Presence

1979_In_Through_The_Out_Door

1982_Coda

$ ls -l | grep -v Led_Zeppelin

1973_Houses_Of_The_Holy

1975_Physical_Graffiti

1976_Presence

1979_In_Through_The_Out_Door

1982_Coda
```

通过 `-v`，你可以开始筛选结果，只显示你需要的精确项目。你不会一直使用 `-v`，但当你需要时，它就会派上场。

## 列出包含搜索单词的文件

`grep` 命令列出包含你所搜索术语的行，但有时你可能不知道文件的名称；相反，你想知道包含这些行的文件名称。在之前的“忽略大小写在文件中搜索文本”中，你查找了 H.P. 洛克拉夫（H.P. Lovecraft）故事中包含隐藏单词的行。现在，你可以使用 `-l`（或 `--files-with-matches`）选项来生成这些文件的列表（记住，`-l` 是用于不区分大小写的搜索）。

```bash
$ grep -il hideous h_p_lovecraft/*

h_p_lovecraft/Call of Cthulhu.txt

h_p_lovecraft/From Beyond.txt

h_p_lovecraft/The Case of Charles Dexter Ward.txt
```

这种结果在与其他命令结合使用时特别有用。例如，如果你想打印包含隐藏单词的洛克拉夫故事列表，可以将 `grep` 与 `lpr` 命令结合如下：

```bash
$ grep -il hideous h_p_lovecraft/* | lpr
```

`find` 的另一个重要方面是，结果的格式取决于你搜索的路径。之前，我们使用的是相对路径，因此结果是以相对路径的形式给出的。如果我们改用以 `/` 开头的绝对路径会发生什么呢？

```
$ find -name "Shags**"

/music/Outs/Shags

/music/Outs/Shags/Gimme_Dat_Ting_(Live).mp3

/music/Outs/Shags/My_Pal_Foot_Foot.ogg

/music/Outs/Shags/f_Love.mp3

/music/Outs/Shags/Things_I_Wonder
```

如果你使用相对路径搜索，你的结果将使用相对路径；如果你使用绝对路径搜索，你的结果将使用绝对路径。我们将在本章后面的部分部分介绍这一原则的其他用法。现在，只需记住这个重要的观点。

> **注意**
>
> 要了解更多关于 The Shags 的信息，请访问 `www.allmusic.com/cg/am.dll?p=am&sql=11:qyk9kett7q7q`，或者在 `www.allmusic.com` 上搜索 “Shags”。在你下一次派对上播放“My Pal Foot Foot”之前，你算没生活过！

# 按所有权查找文件

```
find -user
```

除了按名称搜索文件，你还可以按所有者搜索文件。你想找到音乐驱动器上由 `scott` 拥有的文件吗？使用 `find` 配合 `-user`，后跟用户名（或用户 ID，你可以在 `/etc/passwd` 中找到它）：

```
$ find -user scott
```

哇！结果太多了！寻找不属于 `scott` 拥有的文件会简单得多。要这样做，在你想要反转的选项前面加一个 `!`：

> **注意**
>
> 为了节省空间，你通常通过 `ls -1` 能够看到的某些数据已被删除。

```
$ find ! -user scott

./Outsider/Wing/01-_Dancing_Queen.mp3

$ ls -1 ./.Outsider/Wing/01-_Dancing_Queen.mp3
```



$ gus music ./Outsider/Wing/01-_Dancing_Queen.mp3

啊……Wing 的一首歌属于 `gus` 而不是 `scott`。为了解决这个问题，我们需要使用 `chown`（在第 7 章“所有权与权限”中介绍）。请记住，你始终可以使用 `!` 作为非（NOT）运算符（例如，“查找用户不是 `scott` 的文件”）。

注意

啊，Wing。她首次在《南方公园》的一集节目中被引入大世界，她的网站可以在 www.wingtones.com 找到。强烈推荐 Wing 版本的《Dancing Queen》，以及她演绎的《I Want to Hold Your Hand》同样如此。

# 按组所有权查找文件

```
file -group
```

如果一个命令提供了一个允许你与用户操作的选项，你就知道该命令可能存在一个关于组的选项。`find` 命令也不例外：如果你想查找由特定组拥有的文件，只需使用 `-group`，后跟组名或组 ID。在音乐驱动器上，`scott` 应该是所有者，`music` 应该是组。让我们看看 `music` 组是否有任何文件：

```
$ find ! -group music

./Disco/Strides_of_Funkenstein__-_Disco_to_Go.mp3
./Disco/Sister_Sledge_-_He's_The_Greatest_Dancer.mp3
./Disco/Wild_Cherry__-_Play_That_Funky_Music.mp3
./Electronica/New_Order/Bizarre_Love_Triangle.mp3
```

在大量文件中，只有四个不属于 `music` 组。我们需要运行 `chgrp`（见第 7 章）来确保驱动器上的所有文件都完全一致。

注意，我们再次使用了 `!` 来表示“查找不属于 `music` 组拥有的文件”。

# 按文件大小查找文件

```
file -size
```

有时你想根据文件的大小查找文件。`find` 命令在这里也可以提供帮助。要指定大小，使用 `-size` 选项，后跟一个代表你所选大小方案的字母。如果你不提供字母，将使用默认值；但你应该理解，你可能找不到你想要的内容。如果你不在数字后附加字母，默认单位是字节（通过除以 512 并向上进位到下一个整数）。这计算量太大了。更简单的方法是在数字后面使用一个代表用更常用术语表示大小的后缀，如表 10.1 所示。

| 表 10.1. 按大小查找文件 | 含义 |
|---|---|
| 无后缀 | 512 字节块（默认值） |
| c | 字符 (1 字节) |
| k | 千字节 (KB) |
| M | 兆字节 (MB) |
| G | 吉字节 (GB) |

假设我们想找到你理想专辑《London Calling》中每一首大小为 10MB 的歌曲。（是的，这些是以极高比特率编码的。）这项任务很容易就能找到：

```
$ cd Punk/Clash/1979_London_Calling
$ find . -size +10M

./07_The_Right.ogg
./08_In_The_Supermarket.ogg
./09_down.ogg
./12_Death_Glory.ogg
```

太奇怪了。在大量文件中只有四个不属于 `music` 组的（注：此处原文逻辑略有误，意指只有四个符合条件的）。我们需要运行 `chgrp` 来让驱动器上的所有文件都完全相同。

注意，我们再次使用了 `!` 来表示“查找不属于 `music` 组拥有的文件”。

（注：此处原文文本似乎存在部分重复或逻辑跳转，翻译已根据语境进行微调以保持通顺）

## 当任一表达式为真时显示结果 (OR)

`find -o`

早在“按文件大小查找文件”章节中，我们看到可以使用 `find` 列出 *London Calling* 中所有恰好为 10MB 的 Clash 歌曲，也可以使用 `find` 列出大于 10MB 的歌曲，但我们无法通过 `-size` 同时完成这两个操作。在上一节中，我们看到 `-a` 选项组合逻辑与 AND；然而，我们也可以利用 `-o`（或 `-or`）来组合逻辑或 OR。

因此，为了找到 *London Calling* 中 10MB 或更大的歌目，我们使用以下命令：

```
$ cd London_Calling
$ find . -size +10M -o -size 10M

03__Jimmy_Jazz.ogg
07__The_Right_Profile.ogg
08__Last_In_The_Supermarket.ogg
09__Clampdown.ogg
12__Death_Or_Glory.ogg
15__Lover's_Rock.ogg
18__Revolution_Rock.ogg
(25th_Anniversary)__18__Revolution_Rock.mp3
(25th_Anniversary)__37__-Heart_And_Mind.mp3
(25th_Anniversary)__39__-London_Calling_(Demo).mp3
```

哎……我们还得到了 *London Calling* 25 周年纪念版的结果，这是我们不想要的。我们需要做两件事：排除 25 周年版的结果，并确保我们的 OR 语句正常工作。

为了排除 25 周年版的歌曲，我们在命令末尾添加了 `! -name "*25*"`。为了确保 OR 正常，我们需要用括号将其括起来，以组合这些语句。然而，你需要用反斜杠对括号进行转义，以免 shell 解释它们，同时你还需要在语句前后加上空格。这种组合让我们得到了如下命令：

```
$ cd London_Calling
$ find \(-size +10M -o -size 10M\) ! -name "*25*"

03__Jimmy_Jazz.ogg
07__The_Right_Profile.ogg
08__Last_In_The_Supermarket.ogg
09__Clampdown.ogg
12__Death_Or_Glory.ogg
15__Lover's_Rock.ogg
18__Revolution_Rock.ogg
```

完美。有七首歌的大小为 10MB 或更大。

### 注意

## 第三部分：查找内容

可以在 [Allmusic](www.allmusic.com/cg/ang.dll?p=amp&sqn=10:aeu1z82ajvyn) 或 [Pitchfork](www.pitchforkmedia.com/record-reviews/c/clash/london-calling-calling.html) 阅读更多关于 *London Calling* 的信息。

我们还可以使用 `-o` 来找出硬盘上有多少首歌。我们可以从这个命令开始，我们在 `/media/music` 根目录下运行它，并使用 `-a`（请耐心，我们会讲 `-o` 的）：

```
$ find /media/music -name "*mp3*" -a -type f | wc -l

23407
```

两万三千？这不对。啊，现在显而易见了。我们之前只搜索了 mp3 文件，而大量的歌曲采用了更优的 Ogg Vorbis 格式编码，这是 mp3 的免专利、开源替代方案。让我们查找 mp3 和 ogg 文件，并用 `wc` 统计结果：

```
$ find /media/music \( -name "*mp3*" -o -name "*.ogg" \) -a -type f | wc -l

41631
```

这听起来好多了，但那里还有 FLAC 文件。让我们再加入一个 `-o`：

```
$ find /media/music \( -name "*mp3*" -o -name "*.ogg" -o -name "*.flac" \) -a -type f | wc -l

42187
```

现在看起来才像样了：42,000 首歌，而且还在增加！

## 当表达式不为真时显示结果 (NOT)

```
find ! expr
```

在本章之前的节章节（“按所有者查找文件”和“当任一表达式为真时显示结果 (OR)”）中，我们已经使用 `!` 来否定表达式，但让我们来看另一个，看看这个运算符。在上一节中，我们使用 `find` 确定了音乐硬盘上有多少 mp3、ogg 和 flac 文件。

```
$ find /media/music -name "" | wc -l

52111
```

嗯……52,000 个文件，但只有 42,000 个是 mp3、ogg 或 flac。其他的是什么？让我们构建一个 `find` 命令，排除以 .mp3、.ogg 或 .flac 结尾的文件，同时排除目录。将这些封装在括号中，然后在命令前加上 `!`，表示我们想要排除这些项目，并寻找不符合这些规格的内容：

```
$ find /media/music ! \( -name "*mp3*" -o -name "*.ogg" -o -name "*.flac" -o -type d \) -type f

./Folk/John_Baez/John_Baez___Image.m3u
```



`./500_Greatest_Singles.txt`

`./Blues/Muddy_Waters/Best_Of.mp3`

`./Blues/Robert_Johnson/Hellhound_On.mp3`

`./Blues/Robert_Johnson/Hellhound_On_The_Road.mp3`

`./Blues/Robert_Johnson/Death.mp3`

`./500_Greatest_Singles.txt`

## 第三部分：查找内容

### 对每个文件执行命令

`find` `-exec`

当我们想要对 `find` 找到的每个文件执行操作时，使用 `-exec` 选项。`{}` 是当前文件名的占位符，命令以分号后跟反斜杠 `\;` 结束。

```bash
$ find . -name "*.mp3" -exec ls -l \;
```

让我们使用这个命令重命名我们所有的 mp3 文件，将下划线替换为空格。我们将使用 `sed` 命令进行替换：

```bash
$ find . -name "*.mp3" -exec sed 's/_ /g' {} \;
```

该命令按预期运行。

你可以在脚本中使用这些结果，或者在有帮助的情况下将它们发送到打印机。

### 结论

如你所见，使用 `find` 命令可以做很多事情。`find` 还有很多可以实现，所以你真的应该学习一下 `find`，或者阅读互联网上几篇优秀的教程，它们涵盖了该命令更晦奥但实用的方面。你可以使用各种极其选项通过 `find` 来搜索并列出文件和文件夹。然而，当你使用 `-exec` 选项在发现的文件上运行命令，或者将输出管道给其他命令时，它就变得价值连城了。这是你 Linux 系统上可用的最强大的命令之一，所以开始使用它吧！

# 第四部分：环境

- 第 11 章：你的 Shell
- 第 12 章：监控系统资源
- 第 13 章：安装软件

## 第 11 章：你的 Shell

到本书为止，你一直在 `bash` shell 中运行命令，但你并没有关注过 shell 本身。在本章中，你将查看两个影响你使用 shell 的命令：`history`，它会列出你在命令行上输入的所有内容；以及 `alias`，它允许你为命令创建快捷方式。两者都非常有用，并且在使用命令行时可以为你节省大量时间。对于计算机用户来说，懒惰是一件好事，而这两个命令绝对能帮助你在使用 Linux 系统时尽可能地“懒”。

### 查看你的命令行历史

`history`

每当你在 shell 中输入一个命令时，该命令都会保存在家目录下的一个名为 `.bash_history` 的文件中（文件名前的点 `.` 表示它是隐藏文件，除非你使用 `ls -a`）。默认情况下，该文件保存了命令行中输入的最后 500 行内容。如果你想查看该命令列表，只需输入 `history` 命令即可。

```bash
$ history
496 ls
497 cd rsync-ssh
498 ls
499 cat linux
500 exit
```

由于你正在查看 500 条结果，它们流过得非常快，以至于在到达结尾之前你看不清任何内容。想等待一个屏幕一个地翻页结果吗？转而使用你的老朋友 `less` 吧：

```bash
$ history | less
```

现在你可以更轻松地跳转查看结果了。

**注意**

现在你理解了为什么在命令行输入密码和其他敏感信息时需要小心：任何能查看你 `.bash_history` 文件的人都能看到那些密码。请务必小心，并思考直接在命令行中输入的内容！

### 再次运行上一次命令

`!!`

如果你想再次运行上一次命令，请输入两个感叹号。它会查找历史文件并运行列表中的最后一个命令。

```bash
$ pwd
/home/scott

$ !!
pwd
/home/scott
```

注意，你首先看到的是即将运行的实际命令，然后是该命令的结果。这是一种让计算机替你完成枯燥工作的极具价值的方法。

## 使用数字运行之前的命令

`!##数字`

当你运行 `history` 时，它会自动在每个之前的命令前面加上一个数字。如果你想运行某个之前的命令，并且知道 `history` 为其分配的数字，只需立即输入一个感叹号，紧跟该命令的历史数字，它就会再次运行。

```bash
$ pwd
/home/scott

$ whoami
scott

$ !499
pwd
/home/scott
```

如果你不确定数字，请再次运行 `history` 来查找。请注意，示例中的 `pwd` 命令第一次运行时是数字 499，但在我使用 `!499` 运行它后，它变成了 498，因为它被我的新命令推后了列表。

### 使用字符串运行之前的命令

`!字符串`

通过引用命令来运行命令的能力很棒，但如果你不知道该命令在 `history` 中的数字，这可能很麻烦（不过将 `history` 的输出管道给 `grep` 会有帮助）。通常更好的引用之前的命令的方法是在感叹号后加上命令的前几个字母，这样它会在 `.bash_history` 中找到它。

```bash
$ cat /home/scott
Buy milk
Dog food
Renew Linux subscription

$ cd /home/scott/pictures

$ cat
cat /home/scott
Buy milk
Dog food
Renew Linux subscription
```

如果 `cat` 命令在你的历史记录中出现了三次（例如 35 `cat /home/scott`、412 `cat /etc/sources.list` 和 496 `cat /home/scott`），而你输入 `!cat`，它运行的是 496。如果你想运行 412，你需要输入 `!412` 或者在感叹号后提供足够的信息以便它知道你引用的是命令 412。

```bash
$ !cat /etc
cat /etc/sources.list
deb http://us.archive.ubuntu.com/ubuntu breezy restricted
deb-src http://us.archive.ubuntu.com/ubuntu breezy restricted
```

由于人类更容易记住单词而不是数字，你可能会倾向于使用这种方法。

### 显示所有别名

`alias`

如果你想查看定义的所有别名，只需输入 `alias`。它将列出你当前所有的别名及其代表的命令。如果你想查找特定的别名，可以将 `alias` 的输出管道给 `grep`。

如果你想查看某个特定别名的功能，可以输入 `alias` 后加上该别名。这会显示该别名代表的命令。

如果你想删除一个别名，可以使用 `unalias` 命令加上该别名。这将从当前会话中删除该别名。

如果你想创建一个新的别名，可以使用 `alias` 命令。语法为 `alias 名字='命令'`。这将在当前会话中创建一个新的别名。

```bash
$ alias ll='ls -F'
```

### 删除别名 (Alias)

`unalias`

好事终有散场时，有时一个别名的寿命会超过它的用处。要删除一个别名，请使用 `unalias` 命令。

```bash
$ ls -d *
by_pool/ libby_pix/ on_floor/

$ alias lsd='ls -d *'

$ lsd
by_pool/ libby_pix/ on_floor/

$ unalias lsd

$ $
```

注意，此命令只对临时 shell 别名永久生效（这些别名之前在“创建新的临时别名”中讨论过）。上一个示例中的 `lsd` 别名将彻底消失。如果你对 `.bash_aliases` 中找到的别名使用 `unalias` 命令，它是没问题的，但仅限于你登录期间有效。当你注销并重新登录，或者重新加载 `.bash_aliases` 时，别名就会回来。

要从 `.bash_aliases` 中删除别名，你需要编辑该文件并手动删除包含该别名的行。如果你以后可能还会再次使用该别名，只需在文件行前加一个井号（这将其注释掉），如下：

```bash
# alias lsd='ls -d *'
```



保存`.bash_aliases`，使用`.bash_aliases`命令重新加载它，别名将不再生效。但如果你以后再次需要它，打开`.bash_aliases`，删除井号，保存并重新加载文件，它就可以再次使用了。

### 总结

作为Linux用户，你的目标之一是减少完成目标时需要输入的字符数量。Unix的原始开发者们深信这样一种理念：你应该输入`ls`而不是`makedirectory`。

你在本章中学习的命令在这一过程中都包含了别名（`alias`）的功能。厌倦了输入长而复杂的命令吗？通过`history`引用它，或者为它创建一个别名。无论哪种方式，你都能节省击键次数，你的键盘（更重要的是你的手和手腕）会为此感谢你的。

## 第 12 章 监控系统资源

一个良好的计算机用户应该兼任系统管理员，随时检查机器的健康状况，以确保一切运行顺利。为了帮助实现这一目标，Linux有几条命令可以监控资源。在本章中，你将查看其中的几个命令。它们中的许多都有多种用途，但Unix用小工具完美解决单一任务的传统在系统监控的一个特定方面尤为出色。它们的任务从跟踪计算机上运行的进程（`ps`和`top`）到结束错误进程（`kill`）、列出所有打开的文件（`lsof`），以及报告RAM使用情况（`free`）和磁盘空间（`df`和`du`）。学好这些工具，你会在各种情况下用到它们。

### 查看所有当前运行的进程

`ps aux`

偶尔你运行的某个程序会卡死并停止，需要你将其关闭。或者你可能想知道某个用户正在运行哪些程序。或者你只是想知道你机器上当前运行的进程。在这些任何一种以及许多其他情况下，你都会使用`ps`命令来列出计算机上的进程。

遗憾的是，`ps`有很多版本，它们具有不同类型的选项。取决于这些选项前是否带有连字符，它们的含义甚至可能不同，因此`u`和`-u`的含义是完全不同的。到目前为止，本书在描述`ps`的带连字符选项时一直非常严格，其实不必，这会让事情变得更简单、更统一。

要查看用户在系统上运行的所有进程，请在`ps`后面加上这些选项：`a`（表示所有用户）、`u`（面向用户，或显示谁在使用aux）以及`x`（没有控制终端的进程，即“显示每个进程”的另一种说法）。请准备好一大长列表将划过你的屏幕：这台电脑上有132行。

```bash
User      $ ps aux %CPU %MEM VSZ RSS TTY START STAT TIME COMMAND

scott 24224 4.1 4.2 115040 44036 7 R 11:02 12:03 /home/scott/.coxoffice/bin/wine-preloader

scott 5594 0.0 0.1 3432 1820 pts/6 S+ 12:14 0:00 scott@humbug,machine.com

scott 14957 0.3 7.5 171144 78628 7 S1 13:01 0:35 /usr/lib/openoffice2/program/soffice.bin -writer

scott 12369 0.0 0 0 7 Z 15:43 0:00 [wine-preloader]<defunct>

scott 14680 0.0 0.1 3860 1044 pts/5+ R 15:55 0:00 ps aux
```

`ps`命令为你提供了大量信息，包括哪个用户拥有该进程、标识进程的唯一ID数字（`PID`）、进程使用的CPU百分比（`%CPU`）和内存百分比（`%MEM`）、进程的当前状态（`STAT`）以及进程本身的名字。

`STAT`列可能有不同的字母，以下是最重要的：

| STAT字母 | 含义 |
| :--- | :--- |
| R | Running (运行中) |
| S | Sleeping (睡眠中) |
| T | Stopped (停止) |
| Z | Zombie (僵尸进程) |

`Z`是不好的，因为它意味着进程已经挂起。如果你对`.bash_aliases`中找到的别名使用`unalias`命令，它是没问题的，但仅限于你登录期间有效。当你注销并重新登录，或者重新加载`.bash_aliases`时，别名就会回来。

要从`.bash_aliases`中删除别名，你需要编辑该文件并手动删除包含该别名的行。如果你以后可能还会再次使用该别名，只需在文件行前加一个井号（这将其注释掉），如下：

```bash
# alias lsd='ls -d *'
```

保存`.bash_aliases`，使用`.bash_aliases`命令重新加载它，别名将不再生效。但如果你以后再次需要它，打开`.bash_aliases`，删除井号，保存并重新加载文件，它就可以再次使用了。

### 查看进程树 (Process Tree)

`ps axjf`

在Linux世界中，进程通常以父子关系组织。

```bash
$ ps axjf

UID  PPID PID TTY S TIME COMMAND

root    1 1 ? S 0:00 /systemd

root    1 2 ? S 0:00 /systemd-journal-write

scott 1 24224 ? R 12:03 /home/scott/.coxoffice/bin/wine-preloader

scott 1 5594 pts/6 S+ 0:00 scott@humbug,machine.com

scott 1 14957 pts/7 S1 0:35 /usr/lib/openoffice2/program/soffice.bin -writer

scott 1 12369 ? Z 0:00 [wine-preloader]<defunct>

scott 1 14680 pts/5+ R 0:00 ps aux
```

`ps`命令为你提供了大量信息，包括哪个用户拥有该进程、标识进程的唯一ID数字（`PID`）、进程使用的CPU百分比（`%CPU`）和内存百分比（`%MEM`）、进程的当前状态（`STAT`）以及进程本身的名字。

`STAT`列可能有不同的字母，以下是最重要的：

| STAT字母 | 含义 |
| :--- | :--- |
| R | Running (运行中) |
| S | Sleeping (睡眠中) |
| T | Stopped (停止) |
| Z | Zombie (僵尸进程) |

`Z`是不好的，因为它意味着进程已经挂起。如果你对`.bash_aliases`中找到的别名使用`unalias`命令，它是没问题的，但仅限于你登录期间有效。当你注销并重新登录，或者重新加载`.bash_aliases`时，别名就会回来。

要从`.bash_aliases`中删除别名，你需要编辑该文件并手动删除包含该别名的行。如果你以后可能还会再次使用该别名，只需在文件行前加一个井号（这将其注释掉），如下：

```bash
# alias lsd='ls -d *'
```



保存 `.bash_aliases`，使用 `source .bash_aliases` 命令重新加载它，别名将不再生效。但如果你以后再次需要它，打开 `.bash_aliases`，删除井号，保存并重新加载文件，它就可以再次使用了。

### 结论

作为 Linux 用户，你的目标之一是减少完成目标时需要输入的字符数量。Unix 的原始开发者们深信这样一种理念：你应该输入 `ls` 而不是 `makedirectory`。

你在本章中学习的命令在这一过程中都包含了别名（alias）的功能。厌倦了输入长而复杂的命令吗？通过 `history` 引用它，或者为它创建一个别名。无论哪种方式，你都能节省击键次数，你的键盘（更重要的是你的手和手腕）会为此感谢你的。

## 第 12 章 监控系统资源

一个良好的计算机用户应该兼任系统管理员，随时检查机器的健康状况，以确保一切运行顺利。为了帮助实现这一目标，Linux 有几条命令可以监控资源。在本章中，你将查看其中的几个命令。它们中的许多都有多种用途，但 Unix 用小工具完美解决单一任务的传统在系统监控的一个特定方面尤为出色。它们的任务从跟踪计算机上运行的进程（`ps` 和 `top`）到结束错误进程（`kill`）、列出所有打开的文件（`lsof`）、以及报告 RAM 使用情况（`free`）和磁盘空间（`df` 和 `du`）。学好这些工具，你会在各种情况下用到它们。

### 查看所有当前运行的进程

**ps aux**

偶尔你运行的某个程序会卡死并停止，需要你将其关闭。或者你可能想知道某个用户正在运行哪些程序。或者你只是想知道你机器上当前运行的进程。在这些任何一种以及许多其他情况下，你都会使用 `ps` 命令来列出计算机上的进程。

遗憾的是，`ps` 有很多版本，它们具有不同类型的选项。取决于这些选项前是否带有连字符，它们的含义甚至可能不同，因此 `u` 和 `-u` 的含义是完全不同的。到目前为止，本书在描述 `ps` 的带连字符选项时一直非常严格，其实不必，这会让事情变得更简单、更统一。

要查看用户在系统上运行的所有进程，请在 `ps` 后面加上这些选项：`a`（表示所有用户）、`u`（面向用户，或显示谁在使用 aux）以及 `x`（没有控制终端的进程，即“显示每个进程”的另一种说法）。请准备好一大长列表将划过你的屏幕：这台电脑上有 132 行。

```bash
User      $ ps aux %CPU %MEM VSZ RSS TTY START STAT TIME COMMAND

scott 24224 4.1 4.2 115040 44036 7 R 11:02 12:03 /home/scott/.coxoffice/bin/wine-preloader

scott 5594 0.0 0.1 3432 1820 pts/6 S+ 12:14 0:00 scott@humbug,machine.com

scott 14957 0.3 7.5 171144 78628 7 S1 13:01 0:35 /usr/lib/openoffice2/program/soffice.bin -writer

scott 12369 0.0 0 0 7 Z 15:43 0:00 [wine-preloader]<defunct>

scott 14680 0.0 0.1 3860 1044 pts/5+ R 15:55 0:00 ps aux
```

`ps` 命令为你提供了大量信息，包括哪个用户拥有该进程、标识进程的唯一 ID 数字（PID）、进程使用的 CPU 百分比（`%CPU`）和内存百分比（`%MEM`）、进程的当前状态（`STAT`）以及进程本身的名字。

`STAT` 列可能有不同的字母，以下是最重要的：

| `STAT` 字母 | 含义 |
| :--- | :--- |
| `R` | Running (运行中) |
| `S` | Sleeping (睡眠中) |
| `T` | Stopped (停止) |
| `Z` | Zombie (僵尸进程) |

`Z` 是不好的，因为它意味着进程已经挂起。如果你对 `.bash_aliases` 中找到的别名使用 `unalias` 命令，它是没问题的，但仅限于你登录期间有效。当你注销并重新登录，或者重新加载 `.bash_aliases` 时，别名就会回来。

要从 `.bash_aliases` 中删除别名，你需要编辑该文件并手动删除包含该别名的行。如果你以后可能还会再次使用该别名，只需在文件行前加一个井号（这将其注释掉），如下：

```bash
# alias lsd='ls -d *'
```

保存 `.bash_aliases`，使用 `source .bash_aliases` 命令重新加载它，别名将不再生效。但如果你以后再次需要它，打开 `.bash_aliases`，删除井号，保存并重新加载文件，它就可以再次使用了。

### 查看进程树 (Process Tree)

**ps axjf**

在 Linux 世界中，进程通常以父子关系组织。

```bash
$ ps axjf

UID  PPID PID TTY S TIME COMMAND

root    1 1 ? S 0:00 /systemd

root    1 2 ? S 0:00 /systemd-journal-write

scott 1 24224 ? R 12:03 /home/scott/.coxoffice/bin/wine-preloader

scott 1 5594 pts/6 S+ 0:00 scott@humbug,machine.com

scott 1 14957 pts/7 S1 0:35 /usr/lib/openoffice2/program/soffice.bin -writer

scott 1 12369 ? Z 0:00 [wine-preloader]<defunct>

scott 1 14680 pts/5+ R 0:00 ps aux
```

### 查看特定用户拥有的进程

**ps U [username]**

到目前你一直在观察 `ps` 如何给出系统上所有进程的列表。如果你想将结果限制为单个用户，只需使用 `U` 选项，后加上用户名或数字。

```bash
$ ps U

PPID TTY STAT TIME COMMAND

7558 7561 ? root 00:00 /bin/bash

7561 7604 ? root 00:00 /usr/X11

8225 8279 ? scott 00:00 /sbin/sshd-agent

8225 8341 ? scott 00:00

8316 10842 ? scott 00:00 [kdeinit]

8316 1613 ? scott 00:00 /kwrite

8316 30906 ? scott 00:00 /analysis

17893 17960 ? scott 00:00 /usr/lib/opera/9.0

17893 17961 ? scott 00:00 /usr/lib/opera/pluginwrapper

17893 17962 ? scott 00:00 /usr/lib/opera/plugincer
```

当然，`ps` 并没有在列表中包含用户名，因为它们已经是命令的一部分了。

> **提示**
>
> 记住，如果你不知道用户的数字，只需查看 `/etc/passwd`。找到用户名，用户数字就在第三列。

### 终止运行中的进程

**kill**

有时候程序会发生故障，并且对关闭它的正常尝试没有响应。在图形界面（GUI）中，你反复点击关闭按钮，但什么也没有发生；或者在 shell 中，你按下 `Ctrl+C`，但它无法停止正在运行的命令。当这种情况发生时，是时候使用 `kill` 命令了。

你可以配合 `kill` 命令使用多种信号，其强度范围从“请你关闭自己，并在关闭时清理你留下的烂子”到“尽快关闭自己”，再到“现在死吧！”。我们将重点关注最重要的三个信号。当你使用 `kill` 时，可以使用数字或单词来指定进程死亡的“强度”，如表 12.1 所示。

**表 12.1. 与 `kill` 相关的常用信号**

| 信号数字 | 单词 | 含义 |
| :--- | :--- | :--- |
| `-1` | `HUP` (hang up) | 控制进程已死。关闭系统（如果应用于系统服务，则重新加载配置文件并重启）。 |
| `-15` | `TERM` | 优雅地终止，清理进程和文件。 |
| `-9` | `KILL` | 停止你正在做的一切，完事！ |

通常情况下，你应该先尝试 `-15`（事实上，如果你在不带任何选项运行 `kill`，它是默认选项）。这样，你给了程序一个机会去关闭任何依赖它的其他程序、它打开的文件等。如果你很有耐心等了“一会儿”（当然，这完全是主观的），而进程仍然失控运行或仍然失败，你就可以出出大杀器使用 `-9` 了。`-9` 选项相当于从正在运行的程序脚下抽走地子，虽然它能起作用，但会在你的系统中遗留大量散乱的文件和进程，这绝不是一个好主意。

至于 `-1`，或 `-HUP`，它主要用于 Samba 或无线连接等服务。你不会经常使用它，但你应该知道它的含义。

如果 `vim`（通常它运行良好；这仅用于演示）在你的系统上冻结，你可以这样操作：

```



```bash
$ ps U scott
```

| PID | TID | STAT | TIME | COMMAND |
| :--- | :--- | :--- | :--- | :--- |
| 14928 | ? | S | 0:00 | `/opt/oo2/program/soffice -writer` |
| 14957 | ? | S | 0:42 | `/opt/ooo2/program/soffice.bin -writer` |
| 4688 | pts/4 | S+ | 0:00 | `scott@humbug.machine.com` |
| 26751 | ? | Z | 0:00 | `[wine-preloader] <defunct>` |
| 27921 | ? | S | 0:00 | `47928k id 0.1% /usr/bin/vim` |
| 27955 | pts/5 | R+ | 0:00 | |

```bash
$ kill 27921

$ ps scott
```

| PID | TTY | STAT | COMMAND |
| :--- | :--- | :--- | :--- |
| 14928 | ? | S | 0:00 | `/opt/ooo2/program/soffice -writer` |
| 14957 | ? | S | 0:42 | `/opt/ooo2/program/soffice.bin -writer` |
| 4688 | pts/4 | S+ | 0:00 | `scott@humbug.machine.com` |
| 26751 | ? | Z | 0:00 | `[wine-preloader] <defunct>` |
| 27955 | pts/5 | R+ | 0:00 | `ps scott` |

要杀死`gvim`，你使用`ps gvim`获取`PID`，在本例中为`27921`。接着杀死该`PID`（记住`kill`默认使用`TERM`信号），然后再次用`ps`检查。是的，`gvim`不复存在了。

### 注意

为什么没有杀死`PID`为`26751`的进程？它的`STAT`为`Z`，表示它是一个僵尸进程（`zombie`）。因为`-9`对已经没有地址的僵尸进程无效，`kill`命令无法作用。重启是解决该（无关紧要）问题的唯一方法。

# 查看动态更新的运行进程列表

### top

有时你会发现你的`Linux`无缘无故变慢了。原因是某个程序在你的电脑上全负荷运行，并占用了处理器。或者你启动了一个运行命令，发现它占用的`CPU`周期比你想象的要得多。要找出导致问题的原因，或者你只是想知道系统上运行了哪些程序，可以使用`ps`，但`ps`不会自我更新。相反，它提供的是系统进程的快照，仅此而已。

相比之下，`top`命令提供了系统上运行进程的动态更新列表，以及每个进程使用的资源数量。在书中可能很难看，因为你会看到它每秒更新一次，但你至少能在某一时刻看到正在上方运行的内容。

```
$ top

time 18:05:83 up 4 days, 8:01, load average: 0.83, 0.82, 0.97

Tasks: 135 total, 3 running, 126 sleeping, 2 stopped, 4 zombie

Cpu(s): 22.9% us, 7.7% sy, 3.1% ni, 62.2% id, 3.5% wa, 0.1% hi

Mem: 103616k total, 79796k used, 48140k free, 27884k buff

Swap: 102400k total, 0k used, 102400k free

PID USER PR NI VIRT RES SHR SCPU %MEM TIME TIME+COMMAND

14928 root      20  0 123.4m  45.6m  10.2m S  0.0  0.4% 0:00:00 /opt/oo2/program/soffice -writer

14957 root      20  0 135.6m  58.7m  12.3m S  0.5  0.5% 0:00:42 /opt/ooo2/program/soffice.bin -writer

4688 scott     20  0  15.2m   5.4m   2.1m S+  0.0  0.0% 0:00:00 scott@humbug.machine.com

26751 root       Z  0  0.0m     0.0m   0.0m Z  0.0  0.0% 0:00:00 [wine-preloader] <defunct>

27921 scott     20  0 47.9m  22.1m   8.5m S  0.1  0.0% 0:00:00 /usr/bin/vim

27955 scott     20  0 10.1m   4.2m   1.5m R+  0.0  0.0% 0:00:00 ps scott
```

（注：由于示例中`top`输出内容不完整，此处在翻译时保持了其逻辑结构）

`top`命令提供了系统上运行进程的动态更新列表，以及每个进程使用的资源数量。在书中可能很难看，因为你会看到它每秒更新一次，但你至少能在某一时刻看到正在上方运行的内容。

# 第四部分：环境

### 查看文件打开情况

```bash
# lsof /usr/sbin/sshd  TYPE
```

| COMMAND | PID | USER | NAME |
| :--- | :--- | :--- | :--- |
| `sshd` | 7814 | root | `REG /usr/sbin/sshd` |
| `sshd` | 10542 | root | `REG /usr/sbin/sshd` |
| `sshd` | 10548 | scott | `REG /usr/sbin/sshd` |

这就是你想要的结果：两个用户，`root`和`scott`。如果这里出现了一个意料之外的用户，你就知道你的系统被攻破了。

### 注意

是的，`ssh`是一个程序，但记住，这是从你人类的角度来看的。对于`Linux`来说，`/usr/sbin/sshd`仅仅是另一个文件。

### 列出特定程序的进程列表

### `lsof -c [program]`

在上一节中，你看到了谁在用`/usr/sbin/sshd`。然而，你收到的结果并没有告诉全部情况。任何程序实际上都是由调用（可能是许多）其他进程、程序、套接字和设备而成的，所有这些内容在`Linux`看来都是文件。要找到与特定运行进程关联的所有其他文件，请在`lsof`后面加上`-c`选项，然后是（因此是“已打开的”）进程的名称。例如，`lsof /usr/sbin/sshd`显示与该特定文件关联有两个用户和三个打开的文件。那么整个`sshd`命令又是呢？

```bash
#### lsof -c ssh

COMMAND PID USER NAME

sshd 10542 root /lib/ld-2.3.5.so

sshd 10542 root /dev/null

sshd 10542 root 192.168.0.170:ssh->192.168.0.100:4577 (ESTABLISHED)

sshd 10548 scott /usr/sbin/sshd

sshd 10548 scott 192.168.0.170:ssh->192.168.0.100:4577 (ESTABLISHED)
```

在前面的代码中，你可以看到与`sshd`进程连接的`94`行（代表`94`个打开的文件）中的几行。其中一个是一个`.so`文件（共享对象，类似于`Windows`上的`DLL`），还有几处显示此机器与另一台机器之间发生了网络连接（实际上，该网络上的那台机器通过`SSH`连接到这里；关于这更多信息，请参见第`15`章“在网络工作”中的“安全地登录另一台计算机”）。

通过将`lsof`应用于计算机上的各种命令，你可以发现海量信息；至少，你会了解到现代程序有多复杂。尝试用你每天使用的软件试一下，你可能会对那些努力工作为你提供服务的程序员们产生全新的赞赏。

### 注意

`lsof`命令拥有惊人的选项数量，而你只会查看其中极小的一个子集。`lsof`的源代码包含一个名为`00QUICKSTART`的文件（开头有两个零），该文件是该命令一些更强大功能的教程。在`Google`上搜索该文件名并开始阅读即可。

### 显示系统内存信息

`free`

如今，大多数计算机都配备了数百兆甚至几`GB`的内存，但你仍然可能发现你的机器因为内存使用过多或虚拟内存交换而运行变慢。要查看系统内存的当前状态，请使用`free`命令。

```bash
$ free total used free buffers cached

Mem: 103616 995852 0 80816 332264

-/+ buffers/cache: 582772 453364

Swap: 1012084 49584 516500
```

默认情况下，`free`以千字节显示结果，与你使用的相同。然而，你可以更改它。`b`选项以字节显示内存使用情况，而`-m`（你可能大部分时候应该使用它）使用兆字节。

```bash
$ free -m total used free shared buffers cached

Mem: 1011 963 48 0 78 316

-/+ buffers/cache: 569 442

Swap: 988 483 504
```



# 第四部分：环境

## 显示系统内存信息

`free`

如今，大多数计算机都配备了数百兆甚至几 GB 的内存内存，但你仍然可能发现你的机器因为内存使用过多或虚拟内存交换而运行变慢。要查看系统内存的当前状态，请使用`free`命令。

```bash
$ free
             total       used       free     shared    buffers     cached
Mem:       1036160     995852       80816        0      332264     582772
-/+ buffers/cache:     453364      582772
Swap:      1012084      49584     1012084
```

默认情况下，`free`以千字节显示结果，与你使用的相同。然而，你可以更改它。`-b`选项以字节显示内存使用情况，而`-m`（你可能大部分时候应该使用它）使用兆字节。

```bash
$ free -m
             total       used       free     shared    buffers     cached
Mem:           1011        963         48        0         79        569
-/+ buffers/cache:        442        569
Swap:           988        483        504
```

从`free`输出中你可以看到这台机器有 101MB 的可用内存（实际上是 1024MB，`free`显示为 101MB 是因为内核占用了剩余的 13MB，所以它可以供其他用户使用）。第一行清楚地显示其中 96MB 正在使用，留下了 48MB 的空闲内存。这里有足够的交换空间（或虚拟内存），且 48MB 中的大约一半已经被使用。至少看起来是这样。

事情没那么简单。重要的一行是中间那行，标记为`-/+ buffers/cache`。硬盘使用缓冲区和缓存来加速访问，如果程序需要内存，可以快速释放。从运行这台 Linux 机器的应用程序来看，现在有 442MB 内存空闲可用，如果需要，还有 569MB 缓存可用。这还是你拥有的交换空间之外的额外。Linux 在内存内存方面并不高效。

### 提示

`lsof`命令拥有惊人的选项数量，而你只会查看其中极小的一个子集。`lsof`的源代码包含一个名为`00QUICKSTART`的文件（开头有两个零），该文件是该命令一些更强大功能的教程。在 Google 上搜索该文件名并开始阅读即可。

### 注意

（此处为提示部分结束，原文结构中的“提示”和“注意”标签已整合为三级标题，具体见上文“提示”标题下的内容，原文中重复的“注意”及后续内容实为对`lsof`的提示说明，为避免冗余，仅保留一次）



# 第四部分：环境

## 注意

`lsof` 命令拥有惊人的选项数量，而你只会查看其中极小的一个子集。`lsof` 的源代码包含一个名为 `00QUICKSTART` 的文件（开头有两个零），该文件是该命令一些更强大功能的教程。在 Google 上搜索该文件名并开始阅读即可。

### 显示系统内存信息

`free`

如今，大多数计算机都配备了数百兆甚至几 GB 的内存，但你仍然可能发现你的机器因为内存使用过多或虚拟内存交换而运行变慢。要查看系统内存的当前状态，请使用 `free` 命令。

```bash
$ free
             total       used       free     shared    buffers     cached
Mem:       103616     995852         0        80816      332264
-/+ buffers/cache:   582772     453364
Swap:      1012084      49584     516500
```

默认情况下，`free` 以千字节显示结果，与你使用的相同。然而，你可以更改它。`b` 选项以字节显示内存使用情况，而 `-m`（你可能大部分时候应该使用它）使用兆字节。

```bash
$ free -m
             total       used       free     shared    buffers     cached
Mem:          1011        963         48          0         78        316
-/+ buffers/cache:      569        442
Swap:          988        483        504
```

从 `free` 输出中你可以看到这台机器有 101MB 的可用内存（实际上是 1024MB，`free` 显示为 101MB 是因为内核占用了剩余的 13MB，所以它可以供其他用户使用）。第一行清楚地显示其中 96MB 正在使用，留下了 48MB 的空闲内存。这里有足够的交换空间（或虚拟内存），且 48MB 中的大约一半已经被使用。至少看起来是这样。事情没那么简单。重要的一行是中间那行，标记为 `-/+ buffers/cache`。硬盘使用缓冲区和缓存来加速访问，如果程序需要内存，可以快速释放。从运行这台 Linux 机器的应用程序来看，现在有 442MB 内存空闲可用，如果需要，还有 569MB 缓存可用。这还是你拥有的交换空间之外的额外。Linux 在内存内存方面并不高效。

## 报告目录使用的总空间

如果你不想获取目录下所有子目录的信息，可以使用 `-s` 选项让 `du` 仅报告总计。

```bash
$ cd music
$ du -hs
2.6G
```

简洁明了。

### 结论

在本章中，你看到的几乎每一个命令都有图形界面（GUI）。但如果你的系统没有响应、你正通过 SSH 连接到机器（在第 15 章介绍）且无法使用 GUI，或者你只是想使用最快的工具，你就需要使用命令行了。得益于精心设计的名称，本章中的命令很容易记忆：

- `ps`（运行中的进程）
- `kill`（杀死进程）
- `top`（运行进程的顶部列表）
- `lsof`（列出打开的文件）
- `free`（空、可用内存）
- `df`（磁盘剩余空间）
- `du`（磁盘使用情况）

在你的电脑上进行练习，不要忘记阅读每个命令的 `man` 页面（手册页），本章只能涵盖它们功能的一角。有很多选项可以供选择，特别是 `ps` 和 `top`，它们能让你在你监控的计算机上完成真正惊的工作。

## 第 13 章. 安装软件

Linux 发行版默认包含成千上万个优秀的软件包。在完成基础安装后，你就可以上网、编写报告、创建电子表格、查看和处理图像以及听音乐了。尽管有大量的软件，你可能仍然想要添加你遇到的新工具。幸运的是，Linux 让在你的电脑上安装软件变得非常简单。

关于 Linux 的传统观念认为你必须编译任何你想要的软件。如果你喜欢，仍然可以这样做（像很多人那样），但在当今这很少必要。相反，你可以使用一些简单的工具轻松地安装任何这些软件包。

在继续之前，你需要理解一点。在 Linux 世界中，软件包有多种格式，其中两种占据主导地位：RPM 和 DEB（意所当然，这就是我们在本章中将涵盖的两种）。RPM 由 Red Hat（事实上，RPM 代表 Red Hat Package Manager）、Fedora Core、SUSE 以及其他基于 RPM 的发行版使用。DEB 由基于 Debian 的发行版使用，例如 Debian 本身、Kali/Ubuntu、Linux Mint、Xandros 等许多其他发行版。你应该了解这两种者是如何工作的，但要关注与你的发行版匹配的系统。

### 提示

关于各种软件包管理系统及其使用它们的发行版的详细分类，请参见 DistroWatch 的“Linux Distributions Facts and Figures: What Is Your Distribution's Package Management?”，网址为 `http://distrowatch.com/stats?section=packagemanagement`。注意 DEB 领先（顺便提一下，我有偏见，因为这是使用 Kali/Ubuntu——也称为“正确实践的 Debian”——正在编写的）。

### 为基于 RPM 的发行版安装软件包

```bash
rpm -ivh [package]
rpm -Uhv [package]
```

`rpm` 命令安装以 `.rpm` 结尾的软件安装程序，这似乎很有逻辑。要安装一个 RPM 包，你需要下载它。让我们用行业标准的开源网络扫描器 `nmap` 作为示例。你可以从 `www.nmap.org/nmap/download.html` 下载 `nmap` 的 RPM 包；如果它已经在你的系统中，你只需运行 `rpm` 并带有三个选项：`-i`（安装）、`-h`（显示进度）和 `-v`（详细模式）。



简洁明了。

### 结论

在本章中，你看到的几乎每一个命令都有图形界面（GUI）。但如果你的系统没有响应、你正通过 `SSH` 连接到机器（在第 15 章介绍）且无法使用 GUI，或者你只是想使用最快的工具，你就需要使用命令行了。得益于精心设计的名称，本章中的命令很容易记忆：

-   `ps`（运行中的进程）
-   `kill`（杀死进程）
-   `top`（运行进程的顶部列表）
-   `lsof`（列出打开的文件）
-   `free`（空、可用内存）
-   `df`（磁盘剩余空间）
-   `du`（磁盘使用情况）

在你的电脑上进行练习，不要忘记阅读每个命令的 `man` 页面，本章只能涵盖它们功能的一角。有很多选项可以供选择，特别是 `ps` 和 `top`，它们能让你在你监控的计算机上完成真正惊的工作。

## 第 13 章. 安装软件

Linux 发行版默认包含成千上万个优秀的软件包。在完成基础安装后，你就可以上网、编写报告、创建电子表格、查看和处理图像以及听音乐了。尽管有大量的软件，你可能仍然想要添加你遇到的新工具。幸运的是，Linux 让在你的电脑上安装软件变得非常简单。

关于 Linux 的传统观念认为你必须编译任何你想要的软件。如果你喜欢，仍然可以这样做（像很多人那样），但在当今这很少必要。相反，你可以使用一些简单的工具轻松地安装任何这些软件包。

在继续之前，你还需要理解一点。在 Linux 世界中，软件包有多种格式，其中两种占据主导地位：`RPM` 和 `DEB`（意所当然，这就是我们在本章中将涵盖的两种）。`RPM` 由 `Red Hat`（事实上，`RPM` 代表 `Red Hat Package Manager`）、`Fedora Core`、`SUSE` 以及其他基于 `RPM` 的发行版使用。`DEB` 由基于 `Debian` 的发行版使用，例如 `Debian` 本身、`Kali/Ubuntu`、`Linux Mint`、`Xandros` 等许多其他发行版。你应该了解这两种是如何工作的，但要关注与你的发行版匹配的系统。

### 提示

关于各种软件包管理系统及其使用它们的发行版的详细分类，请参见 `DistroWatch` 的“Linux Distributions Facts and Figures: What Is Your Distribution's Package Management?”，网址为 `http://distrowatch.com/stats?section=packagemanagement`。注意 `DEB` 领先（顺便提一下，我有偏见，因为这是使用 `Kali/Ubuntu`——也称为“正确实践的 Debian”——正在编写的）。

### 为基于 RPM 的发行版安装软件包

```
rpm -ivh [package]
rpm -Uhv [package]
```

`rpm` 命令安装以 `.rpm` 结尾的软件安装程序，这似乎很有逻辑。要安装一个 `RPM` 包，你需要下载它。让我们用行业标准的开源网络扫描器 `nmap` 作为示例。你可以从 `www.nmap.org/nmap/download.html` 下载 `nmap` 的 `RPM` 包；如果它已经在你的系统中，你只需运行 `rpm` 并带有三个选项：`-i`（安装）、`-h`（显示进度）和 `-v`（详细模式）。

这实际上是你应该运行的命令，它看起来像这样：

```
# rpm -ihv nmap-4.01-1.i386.rpm
```

更好的选择是 `-Uhv`，其中 `-U` 代表升级。为什么 `-U` 比 `-i` 好？因为 `-i` 只安装，而 `-U` 升级并安装。如果系统中已存在软件包，且你正尝试放入一个更新的版本，`-U` 执行升级；如果软件包不在你的系统中，`-U` 则会安装它。因此，始终使用 `-U`，无论你是升级还是安装，它都会完成该做的工作，你不需要担心。

```
# rpm -Uhv nmap-4.01-1.i386.rpm
准备中... ########################### [100%]
1:nmap ################################# [100%]
```

如果你想安装多个 `RPM`，只需空格将它们分开，一个一个列出：

```
# rpm -Uhv nmap-4.01-1.i386.rpm nmap-frontend-4.01-1.i386.rpm
```

如果你在一个名为 `software` 的子目录下有很多 `.rpm` 文件，可以使用通配符来安装它们：

```
# rpm -Uhv software/*.rpm
```

### 注意事项

`-U` 选项总是更好的，除非是安装内核。那时你想要使用 `-i`。如果你用 `-U` 升级且新内核无法工作，你将陷入苦海。另一方面，如果你用 `-i` 安装新内核，你是安全的。

## 为基于 RPM 的发行版移除软件包

```
rpm -e [package]
```

## 为基于 Debian 的发行版安装软件包

```
apt-get install [package]
```

`apt-get` 命令是在基于 `Debian` 系统上安装软件的标准方法。它会自动处理依赖关系，这是相对于 `rpm` 的主要优势。要移除软件包，请使用：

```
apt-get remove [package]
```

(5/6): `libogg-1.1.2-1.138` 100% |========= 16 kB 00:00
(6/6): `libvorbis-1.1.0-1` 100% |========= 185 kB 00:00
正在执行事务

正在执行事务
正在安装: `libogg`        ###### [1/6]
正在安装: `libvorbis`      ###### [2/6]

...
已安装 `xmms.i386` 1:1.2.10-9
已安装依赖项: `gdk-pixbuf.i386` 1:0.22-07.el4.3 `gtk+.i386` 1:1.2.10-33 `libogg.i386` 2:1.1.2-1 `libvorbis.i386` 1:1.1.0-1 `mikmod.i386` 0:3.1.6-32.EL4

呼！`XMMS` 终于安装完成并可以使用了。现在决定不喜欢它，就来看看如何移除 `XMMS` 吧。

## 为基于 RPM 的发行版删除软件包及其依赖项

```
yum remove [package]
```

`yum` 的优点之一：它的命令语法非常用户友好。想安装包？`yum install`。想删除？`yum remove`。所以，如果你厌倦了 `XMMS`，只需运行此命令：

```
# remove xmms
正在设置删除进程
正在解析依赖关系
--> 包 xmms.i386 1:1.2.10-9 将被删除
```

包 架构 版本 仓库 大小

正在移除:
`xmms` `i386` `1:1.2.10-9` 已安装 5.2 M

是否确定 [y/N]:

即使是像删除一个软件包这么简单的操作，`yum` 依然延续它的习惯，抓住你的领子并向你长长大论它的情况。按 `y` 确认卸载，你会得到更多数据：

```
正在执行事务测试
正在执行事务
# 第四部分：环境
正在移除 : xmms ################# [1/1]
已移除: xmms.i386 1.1.20-9
完成！
```

现在 `XMMS` 消失了。请注意，由 `yum` 安装的依赖项（在详细章节“为基于 RPM 的发行版安装软件包及其依赖项”中）并没有随着 `xmms` 软件包一起移除。`XMMS` 运行需要这些依赖项，但它们仍然可以在你的电脑上供其他程序使用，`yum` 允许它们保留（这是 `apt` 的默认行为，你将在“为 Debian 删除软件包及其依赖项”中看到这一点）。

## 为基于 RPM 的发行版升级软件包及其依赖项

```
yum update
```

你的 Linux 系统包含成百上千个软件包，针对某个包或另一个包的更新在不断产生。跟踪每个软件的新版本并安装更新将是你的一项全职工作，但 `yum` 让这个过程变得简单。一个简单的更新命令告诉 `yum` 检查它跟踪的软件是否有任何更新。如果有新包可用，`yum` 会向你显示可选的包并请求许可安装它们。

```
# yum update
正在设置更新进程
正在设置仓库
update 100% |====================| 951 B 00:00
base 100% |================| 1.1 KB 00:00
```

```
正在解析依赖关系
--> 正在解析所选包的事务集。请等待。
--> 正在下载 cups-libs 的头部以放入事务集。
cups-libs-1.1.22-0.rcl9.10 100% |====================| 22 KB 00:00
--> 包 cups-lips.i386 1.1.22-0.rcl9.10 将被更新
--> 正在运行事务检查
依赖关系已解决
包 架构 版本
```



# 第四部分：环境

| | | | |
|---|---|---|---|
| `openssl` | `i386 0.9.7a-43.4` | `update` | 1.1 M |
| `pam` | `i386 07-66.13` | `update` | 1.8 M |
| `perl` | `i386 3.5.8-24.RHEL4` | | 11 M |
| `udev` | `i386 09.10-10.EL4.3` | `update` | 830 K |
| `wget` | `i386 1.1.20-0.40E` | `update` | 567 K |
| 事务摘要 | | | |

安装 1 个包(s)
更新 11 个包(s)
移除 0 个包(s)
总下载大小: 30 M

是否确定 `[y/N]`：

如果你在此处按 `y`，你就获得了 `yum` 许可下载并安装 12 个包。在许多 `yum update` 完成工作后，你的电脑现在是最新的。想生活在最前沿吗？每天运行 `yum update`。如果你不追求总是使用最新最强大的功能，可以按间隔运行 `yum update`，但务必定期运行它。软件的安全更新无处不在，保持更新是一个好主意。

## 在基于 RPM 的发行版中查找可下载的软件包

```
yum search [string]
yum list available
```

现在你知道如何使用 `yum` 安装和删除软件了，但最初如何找到软件呢？让我们来看看。

## 在 Debian 系发行版中查找和管理软件包

```
Hit http://ftp.free.fr breezy breezy/non-free Sources
Fetched 140kB in 1ms (217kB/s)
Reading package lists.. Done
[Results] truncated for length
# apt-get install sshfs
Reading package lists.. Done
Building dependency tree.. Done
The following extra packages will be installed:
fuse-utils libfuse2
The following NEW packages will be installed:
fuse-utils libfuse2 sshfs
```

需要下载 96.9kB 的存档。
解压后将使用 344kb 的额外空间。
你确定要继续吗？ `[Y/n]`
`Get: http://us.archive.ubuntu.com/universe sshfs 1.1-1 [19.3KB]`

```
Fetched 96.9kb in 10s (961kB/s)
Reading package fields.. Done
Reading package status.. Done
Preconfiguring packages....
Selecting previously deselected package sshfs.
Unpacking sshfs (from ...)/archives/sshfs/1.1-i386.deb)
Setting up sshfs (1.1-1)-
```

让我们过一下你之所以那样做，因为你运行了两个命令。`apt-get update` 从 `apt` 服务器或存储库下载当前软件包列表，这些存储库列在你的 `apt` 配置中，位于 `/etc/apt/sources.list`。如果你想查看存储库所在的位置，请运行 `cat /etc/apt/sources.list`。如果你在运行 `apt-get update` 后在某行开头看到 `Get`，意味着 `apt` 发现存储库中的列表较新，因此它正在下载该特定列表；而 `Ign` 则意味着存储库列表与你的计算机是同步的，因此不需要下载。在执行任何操作之前运行 `apt-get update`，可以确保你的软件包列表是最新的。

`apt-get install` 命令检索指定的软件包以及任何必要的依赖项（在本例中为 `fuse-utils` 和 `libfuse2`）。在这些文件到达你的本地后，`apt`（或应 `apt` 激活的 `dpkg`）会为你安装所有软件。请记住，你始终使用的是包名，而不是文件名。换句话说，使用 `apt-get install sshfs`，而不是 `apt-get install sshfs_1.1-1_i386.deb`。如果 `apt` 发现请求的软件包有额外的依赖项（如 `sshfs` 那样），你需要在 `apt` 获取它们之前确认你想要安装它们。

如果你想同时安装多个软件包，只需在命令行中列出所有包名即可。例如，如果你想安装 `sshfs` 和 `shfs-utils`，可以执行以下操作：

```
# apt-get install sshfs shfs-utils
```

`sshfs` 或 `shfs-utils` 的任何依赖项都会被发现，系统会询问你是否也安装它们。是的，就如此简单。

> 提示

不知道 `sshfs` 是什么吗？噢，你应该知道的！阅读我的博客文章《通过 SSH 使用 SSHFS 挂载远程驱动器》，你可以在 Open Source Weblog 上找到它，地址为：
`http://opensource.weblogs.com/2005/11/03/mount-remote-drives-via-ssh-with-shshfs/`

## 移除 Debian 软件包及其依赖项

`apt-get remove [package]`

如果你不再需要系统中的某个软件包，`apt` 让你轻松地卸载它：使用 `apt-get remove` 代替 `apt-get install`。该命令的运行机理与 `apt-get install` 完全相反：它会卸载你指定的软件包以及任何依赖项。再次强调，请引用包名，使用 `apt-get remove sshfs`，而不是 `apt-get remove sshfs_1.1-1_i386.deb`。

```
# apt-get remove sshfs
Password:
```

以下软件包将被 移除：
`sshfs`

解压后将释放 98.3KB 的磁盘空间。
你确定要继续吗 `[Y/n]`？

移除软件包实际上并不会移除该包的每一个痕迹，因为被移除软件包的配置文件会残留在你的计算机上。如果你确定要删除所有内容，请使用 `--purge` 选项。

```
# apt-get --purge remove sshfs
Password:
```

以下软件包将被 移除：
`sshfs*`
解压后将释放 98.3KB 的磁盘空间。
你确定要继续吗 `[Y/n]`？

使用 `--purge`，`apt` 准备移除的软件包将被标记上星号，表示相关的配置文件也将被移除。

## 升级 Debian 软件包及其依赖项

`# apt-get upgrade`

Linux 系统上安装有多个软件软件包，而且可以肯定，其中至少有一个包每天会被其维护者升级。通过 `apt`，保持你的系统更新非常简单。过程如下（记住，此命令必须以 `root` 身份运行）：

```
# apt-get update
Get:1 http://archive.ubuntu.com breezy Release.gpg [189B]
Get:2 http://archive.ubuntu.com breezy Release.gpg [189B]
Hit http://ftp.ubuntu.com/breezy Sources
Hit http://ftp.ubuntu.com/breezy Sources
Fetched 140kB in 1ms (217kB/s)
Reading package lists.. Done
[Results] truncated for length
# apt-get upgrade
Reading package lists.. Done
Building dependency tree.. Done
The following extra packages will be installed:
fuse-utils libfuse2
The following NEW packages will be installed:
fuse-utils libfuse2 sshfs
```

需要下载 96.9kB 的存档。
解压后将使用 344kb 的额外空间。
你确定要继续吗？ `[Y/n]`
`Get: http://us.archive.ubuntu.com/universe sshfs 1.1-1 [19.3KB]`

```
Fetched 96.9kb in 10s (961kB/s)
Reading package fields.. Done
Reading package status.. Done
Preconfiguring packages....
Selecting previously deselected package sshfs.
```



Unpacking `sshfs` (from `.../archives/sshfs/1.1-i386.deb`)

Setting up `sshfs` (`1.1-1`)

让我们过一下你之所以那样做，因为你运行了两个命令。`apt-get update` 从 `apt` 服务器或存储库下载当前软件包列表，这些存储库列在你的 `apt` 配置中，位于 `/etc/apt/sources.list`。如果你想查看存储库所在的位置，请运行 `cat /etc/apt/sources.list`。如果你在运行 `apt-get update` 后在某行开头看到 `Get`，意味着 `apt` 发现存储库中的列表较新，因此它正在下载该特定列表；而 `Ign` 则意味着存储库列表与你的计算机是同步的，因此不需要下载。在执行任何操作之前运行 `apt-get update`，可以确保你的软件包列表是最新的。

`apt-get install` 命令检索指定的软件包以及任何必要的依赖项（在本例中为 `fuse-utils` 和 `libfuse2`）。在这些文件到达你的本地后，`apt`（或应 `apt` 激活的 `dpkg`）会为你安装所有软件。请记住，你始终使用的是包名，而不是文件名。换句话说，使用 `apt-get install sshfs`，而不是 `apt-get install sshfs_1.1-1_i386.deb`。如果 `apt` 发现请求的软件包有额外的依赖项（如 `sshfs` 那样），你需要在 `apt` 获取它们之前确认你想要安装它们。

如果你想同时安装多个软件包，只需在命令行中列出所有包名即可。例如，如果你想安装 `sshfs` 和 `shfs-utils`，可以执行以下操作：

```
# apt-get install sshfs shfs-utils
```

`sshfs` 或 `shfs-utils` 的任何依赖项都会被发现，系统会询问你是否也安装它们。是的，就如此简单。

### 提示

#### 第四部分：环境

不知道 `sshfs` 是什么吗？噢，你应该知道的！阅读我的博客文章《通过 SSH 使用 SSHFS 挂载远程驱动器》，你可以在 Open Source Weblog 上找到它，地址为：
`http://opensource.weblogs.com/2005/11/03/mount-remote-drives-via-ssh-with-shshfs/`

### 移除 Debian 软件包及其依赖项

`apt-get remove [package]`

如果你不再需要系统中的某个软件包，`apt` 让你轻松地卸载它：使用 `apt-get remove` 代替 `apt-get install`。该命令的运行机理与 `apt-get install` 完全相反：它会卸载你指定的软件包以及任何依赖项。再次强调，请引用包名，使用 `apt-get remove sshfs`，而不是 `apt-get remove sshfs_1.1-1_i386.deb`。

```
# apt-get remove sshfs

Password:
```

以下软件包将被 移除：
`sshfs`

解压后将释放 98.3KB 的磁盘空间。
你确定要继续吗 [Y/n]?

移除软件包实际上并不会移除该包的每一个痕迹，因为被移除软件包的配置文件会残留在你的计算机上。如果你确定要删除所有内容，请使用 `--purge` 选项。

```
# apt-get --purge remove sshfs

Password:
```

以下软件包将被 移除：
`sshfs*`
解压后将释放 98.3KB 的磁盘空间。
你确定要继续吗 [Y/n]?

使用 `--purge`，`apt` 准备移除的软件包将被标记上星号，表示相关的配置文件也将被移除。

### 升级 Debian 软件包及其依赖项

#### 第四部分：环境

```
# apt-get upgrade
```

Linux 系统上安装有多个软件软件包，而且可以肯定，其中至少有一个包每天会被其维护者升级。通过 `apt`，保持你的系统更新非常简单。过程如下（记住，此命令必须以 `root` 身份运行）：

```
# apt-get update

Get:1 http://archive.ubuntu.com breezy Release.gpg [189B]

Get:2 http://archive.ubuntu.com breezy Release.gpg [189B]

Hit http://ftp.ubuntu.com/breezy Sources

Hit http://ftp.ubuntu.com/breezy Sources

Fetched 140kB in 1ms (217kB/s)

Reading package lists.. Done

[Results] truncated for length

# apt-get upgrade

Reading package lists.. Done

Building dependency tree.. Done

The following extra packages will be installed:

fuse-utils libfuse2

The following NEW packages will be installed:

fuse-utils libfuse2 sshfs
```

需要下载 96.9kB 的存档。
解压后将使用 344kb 的额外空间。
你确定要继续吗？ [Y/n]? 
`Get: http://us.archive.ubuntu.com/universe sshfs 1.1-1 [19.3KB]`

```
Fetched 96.9kb in 10s (961kB/s)

Reading package fields.. Done

Reading package status.. Done

Preconfiguring packages....

Selecting previously deselected package sshfs.

Unpacking sshfs (from ...)/archives/sshfs/1.1-i386.deb)

Setting up sshfs (1.1-1)-
```

让我们过一下你之所以那样做，因为你运行了两个命令。`apt-get update` 从 `apt` 服务器或存储库下载当前软件包列表，这些存储库列在你的 `apt` 配置中，位于 `/etc/apt/sources.list`。如果你想查看存储库所在的位置，请运行 `cat /etc/apt/sources.list`。如果你在运行 `apt-get update` 后在某行开头看到 `Get`，意味着 `apt` 发现存储库中的列表较新，因此它正在下载该特定列表；而 `Ign` 则意味着存储库列表与你的计算机是同步的，因此不需要下载。在执行任何操作之前运行 `apt-get update`，可以确保你的软件包列表是最新的。

`apt-get install` 命令检索指定的软件包以及任何必要的依赖项（在本例中为 `fuse-utils` 和 `libfuse2`）。在这些文件到达你的本地后，`apt`（或应 `apt` 激活的 `dpkg`）会为你安装所有软件。请记住，你始终使用的是包名，而不是文件名。换句话说，使用 `apt-get install sshfs`，而不是 `apt-get install sshfs_1.1-1_i386.deb`。如果 `apt` 发现请求的软件包有额外的依赖项（如 `sshfs` 那样），你需要在 `apt` 获取它们之前确认你想要安装它们。

如果你想同时安装多个软件包，只需在命令行中列出所有包名即可。例如，如果你想安装 `sshfs` 和 `shfs-utils`，可以执行以下操作：

```
# apt-get install sshfs shfs-utils
```

`sshfs` 或 `shfs-utils` 的任何依赖项都会被发现，系统会询问你是否也安装它们。是的，就如此简单。

### 提示

#### 第四部分：环境

不知道 `sshfs` 是什么吗？噢，你应该知道的！阅读我的博客文章《通过 SSH 使用 SSHFS 挂载远程驱动器》，你可以在 Open Source Weblog 上找到它，地址为：
`http://opensource.weblogs.com/2005/11/03/mount-remote-drives-via-ssh-with-shshfs/`

### 移除 Debian 软件包及其依赖项

`apt-get remove [package]`

如果你不再需要系统中的某个软件包，`apt` 让你轻松地卸载它：使用 `apt-get remove` 代替 `apt-get install`。该命令的运行机理与 `apt-get install` 完全相反：它会卸载你指定的软件包以及任何依赖项。再次强调，请引用包名，使用 `apt-get remove sshfs`，而不是 `apt-get remove sshfs_1.1-1_i386.deb`。

```
# apt-get remove sshfs
```



## 移除软件包并清理残留配置

执行 `apt-get remove sshfs` 命令时，系统会提示确认操作：

```
Password:

以下软件包将被 移除：
sshfs

解压后将释放 98.3KB 的磁盘空间。
你确定要继续吗 [Y/n]?
```

移除软件包实际上并不会移除该包的每一个痕迹，因为被移除软件包的配置文件会残留在你的计算机上。如果你确定要删除所有内容，请使用 `--purge` 选项。

```
# apt-get --purge remove sshfs

Password:

以下软件包将被 移除：
sshfs*
解压后将释放 98.3KB 的磁盘空间。
你确定要继续吗 [Y/n]?
```

使用 `--purge`，`apt` 准备移除的软件包将被标记上星号，表示相关的配置文件也将被移除。

## 升级 Debian 软件包及其依赖项

Linux 系统上安装有多个软件软件包，而且可以肯定，其中至少有一个包每天会被其维护者升级。通过 `apt`，保持你的系统更新非常简单。过程如下（记住，此命令必须以 root 身份运行）：

```
# apt-get update

Get:1 http://archive.ubuntu.com breezy Release.gpg [189B]

Get:2 http://archive.ubuntu.com breezy Release.gpg [189B]

Hit http://ftp.ubuntu.com/breezy Sources

Hit http://ftp.ubuntu.com/breezy Sources

Fetched 140kB in 1ms (217kB/s)

Reading package lists.. Done
```

更新完成后，执行升级操作：

```
# apt-get upgrade

Reading package lists.. Done

Building dependency tree.. Done

The following extra packages will be installed:

fuse-utils libfuse2

The following NEW packages will be installed:

fuse-utils libfuse2 sshfs
```

## 查找 Debian 可下载的软件包

使用 `apt-cache search` 命令可以查找可用的软件包：

```
apt-cache search
```

我们已经讨论了许多使用 `apt` 安装软件的方法，但如何知道软件包首先是可用的呢？`apt` 工具箱中还有另一个工具可以帮助：`apt-cache search`。

当安装 `sshfs` 时，输出可能如下：

```
Reading package fields.. Done

Reading package status.. Done

Preconfiguring packages....

Selecting previously deselected package sshfs.

Unpacking sshfs (from ...)/archives/sshfs/1.1-i386.deb)

Setting up sshfs (1.1-1)-
```

## 清理 Debian 不必要的安装包

当使用 `apt` 下载并安装软件包时，`.deb` 文件会留在 `/var/cache/apt/archives/`。随着时间的推移，不必要的安装程序会占用大量的空间。移除所有不必要的 `.deb` 文件，请使用 `apt-get clean`（再次强调，此命令以 root 身份运行）：

```
$ ls -l /var/cache/apt/archives/

fuse-utils_2.3.0-ubuntu1.1_i386.deb

libfuse2_2.3.0-ubuntu1.1_i386.deb

lock

partial/

sshfs_1.1-1_i386.deb

# apt-get clean
```

如果下载由于某种原因被中断，你可能会在 `/var/cache/apt/archives/partial/` 中发现一个部分 `.deb` 文件。如果你确定所有的更新和升级已经完成并安装，那么如果你在该目录中发现了任何内容，删除它们是安全的。

## 排除 apt 的故障问题

当然，尽管 `apt` 非常强大，但你仍然可能会遇到问题。这里是一些问题及其解决方法。

一个会导致你产生额外开销的简单问题是“无法打开锁文件”（`Could not open lock file`）错误。当你尝试运行 `apt-get` 时，它没有工作，而是输出了此错误消息：

```
E: Could not open lock file /var/lib/dpkg/lock - open (13 Permission denied)

E: Unable to lock the administration directory (/var/lib/dpkg/), are you root?
```

该问题的解决方法就在第二行中：你没有以 root 身份登录！只需登录 root 并再次尝试，一切都应该正常工作。

**注意**

如果你运行的是 K/Ubuntu 或任何其他使用 `sudo` 代替 root 的发行版，该错误意味着你没有在命令前加上 `sudo`。换句话说，你运行了以下命令：

```
$ apt-get upgrade
```

你看到错误消息是因为你应该运行这个命令：

```
$ sudo apt-get upgrade
```

下一种常见问题是 `apt` 抱怨依赖关系损坏（broken dependencies）。当 `apt` 鼓励你运行 `apt-get -f install` 时，你就知道发生了这种情况。这个建议是程序在告诉你，系统存在损坏的依赖关系，导致 `apt` 无法完成工作。

有两个可能的解决方案。你可以遵循 `apt` 的建议，运行 `apt-get -f install`，它会尝试通过下载并安装必要的包来修复问题。通常，这会解决问题，你就可以继续。

如果你不想这样做，可以尝试运行 `apt-get -f remove`，它会尝试通过移除 `apt` 认为有问题的包来修复问题。这些步骤听起来可能是潜在的危险操作，如果你不注意的话确实如此，但每个选项都给了你审查任何拟议更改并给予许可的机会。只需在确认之前检查 `apt` 的提议即可。

最后，`apt` 通知你某些软件包“被留待”（have been kept back）。这是在告诉你 `apt` 在请求的软件包或其依赖项与系统中已安装的另一个软件包之间发现了冲突。要解决此问题，尝试使用 `-u` 选项安装被留待的软件包，这将为你提供关于具体哪些内容需要升级的信息。

### 结论

基于 RPM 和基于 Debian 的发行版尽管存在差异，但在软件包管理方面有一些相似之处，因为它们都被设计用于简化软件的安装、删除和管理。基于 RPM 的发行版使用 `rpm` 命令来安装、升级和删除软件，而基于 Debian 的发行版使用 `dpkg` 实现相同目的。为了解决依赖地狱的烦恼，基于 RPM 的发行版有 `yum`（`rpm` 的封装），而基于 Debian 的发行版有 `apt`（`dpkg` 的封装）。尽管如此，它们仍然存在差异，主要体现在成熟度和易用性上。在这些领域，`apt` 绝对优于 `yum`，但 `yum` 正在不断改进。

最后，两者都比 Windows 用户必须忍受的要好。`Windows Update` 只更新微软自己的软件和少数第三方驱动程序，而 `apt` 和 `yum` 都能处理 Linux 系统上的几乎每一个软件。这是 Linux 相比于其微软表亲的巨大优势，也是一个让我们自豪的优势。

## 第五部分：网络

- 第 14 章：连接性
- 第 15 章：在网络工作
- 第 16 章：Windows 网络

## 第 14 章：连接性

网络自 Linux 诞生初以来就是它的一部分（当时它只是由一小群程序员修改的简单内核），而且它是让 Linux 变得伟大的核心。Linux 网络在大多数情况下都能运行，为你提供一个固若金汤的连接，并可以无限地调整和调优以满足你的精确需求。

本章完全关于测试、测量和管理你的网络设备和连接。当一切运行正常时，你在大多数时间里会使用工具来监控系统的网络连接；如果你遇到问题，本章将帮助你解决一些最棘手的问题。

**提示**

本章的信息假设你正在使用 IPv4 地址，格式为 `xxx.xxx.xxx.xxx`。IPv6 最终会取代 IPv4，但那是未来的事情。到那时，`route` 以及你将要检查的其他命令将发生变化。目前，本章的信息就是你需要的。有关 IPv6 的更多信息，请参见维基百科的“IPv6”（http://en.wikipedia.org/wiki/IPv6）。

### 查看网络接口状态

```
ifconfig
```



本章的所有内容取决于你的网络连接。在本章的末尾，“排除网络问题”部分，你将学习修复网络连接问题的方法。在这里，让我们看看你建立了哪些网络连接及其状态。

要快速查看所有网络设备（无论它们是否正在运行），请使用 `ifconfig`（`interface configuration` 的缩写）并配合 `-a`（`all` 选项）。以下是你在笔记本上可能看到的内容（注意某些发行版需要以 `root` 登录后使用 `ifconfig`）：

```
$ ifconfig -a

eth0 Link:Ethernet HWaddr:00:14:6C:06:6B:8FD

inet addr:192.168.0.101 Bcast:192.168.0.255 Mask:255.255.255.250

inet6: fe80::214:6ff:fe06:6bd/64 Scope:Link

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:1257 errors:759 dropped:0 overruns:0 frame:7557

TX packets:549 errors:2 dropped:0 overruns:0 carrier:0

collisions:0 tqueuelen:1000

RX bytes:195869 (191.2 KB) TX bytes:95727 (93.4 KB)
```

# Up: Networking

## 第五部分：网络

注意
你可能会看到你的网络设备的其他名称，例如用于无线网卡的 `wlan0`。

`ifconfig -a` 显示所有接口，即使是处于关闭（`down`）状态的；单独使用 `ifconfig` 只显示处于开启（`up`）的连接。这是检查网络接口状态的快速方法，特别是当你需要快速查找 IP 地址时。

注意
你也可以使用 `ifconfig` 配置你的网络接口，该过程在后文的“配置网络接口”中会有描述。

## 验证计算机正在运行并接受请求

```
ping
ping -c
```

`ping` 命令向指定地址发送一种特殊的数据包，即 `ICMP ECHO_REQUEST` 消息。如果一台机器正在监听 ICMP 消息，它将用 `ICMP REPLY` 进行应答。（防火墙确实会拦截 ICMP 消息，导致 `ping` 无效，但大多数情况下这不是问题。）成功的 `ping` 意味着两台机器之间存在网络连通性。

```
$ ping www.google.com

ping www.google.com

PING www.google.com (72.14.203.99) 56(84) bytes of data.

64 bytes from 72.14.203.99: icmp_seq=1 ttl=245 time=17.1 ms

64 bytes from 72.14.203.99: icmp_seq=2 ttl=245 time=18.1 ms

[结果因长度被截断]--- www.google.com

ping statistics ---

6 packets transmitted, 5 received, 16% packet loss, time 501ms

tr min/avg/max/mdev = 16.939/17.560/18.136/0.460 ms
```

在你按下 `Ctrl+C` 之前，`ping` 命令不会停止。如果你正在使用 `ping`，这可能会导致问题，因为它会持续运行，直到被停止或你的机器的网络连接断开。如果有人忘记并让一个 `ping` 会话运行 18 天，向你的其中一台服务器发送了近 140 万次 `ping`。

如果你想限制 `ping` 的次数，可以使用 `-c` 选项设置 `ping` 要发送的数据包数量，后跟一个数字。在 `ping` 发送指定数量的数据包后，就会停止并报告结果。

```
$ ping -c 3 www.granneman.com

PING granneman.com (216.23.180.5) 56(84) bytes of data.

64 bytes from 216.23.180.5: icmp_seq=1 ttl=44 time=65.4 ms

64 bytes from 216.23.180.5: icmp_seq=2 ttl=44 time=64.5 ms

64 bytes from 216.23.180.5: icmp_seq=3 ttl=44 time=65.7 ms

---

3 packets transmitted, 3 received, 0% packet loss,

time 4006ms

rtt min/avg/max/mdev = 64.515/64.258/64.700/0.510 ms
```

`ping` 命令是确定基本网络连通性的标准方法；更好的是，如果你包含了 `-c` 选项，你就永远不会不小心让 `ping` 意外运行 18 天。

有关关于如何使用 `ping` 诊断网络连通性问题的信息，请参见“排除网络问题”。

## 追踪两个主机之间的数据包路由

`traceroute`

`traceroute` 命令显示了从你的机器到指定主机路径上经过的每一个步骤。假设你想知道为什么无法访问 `www.google.com`。你昨天还能加载它，但今天网页却超时了。出了什么问题？

```
$ traceroute www.google.com (216.23.180.5) 30 hops max 38 packets

traceroute to google.com (216.23.180.5) 1.245 ms 0.827 ms 0.839 ms

  2 10.29.64.1 (10.29.64.1) 8.582 ms 19.930 ms 7.083 ms

  3 24.217.2.165 (24.217.2.165) 10.152 ms 36.667 ms

  4 12.124.129.97 (12.124.129.97) 9.203 ms 8.003 ms 11.307 ms

  5 12.124.129.101 (12.124.129.101) 50.619 ms 51.235 ms

  6 tbr2-p01350.s91.ip.at (12.122.101.113) 51.625 ms 52.166 ms 50.156 ms

  7 tbr2-p01350.s91.ip.at (12.122.101.113) 50.669 ms 54.049 ms 69.934 ms

  8 tbr2-p01350.s91.ip.at (12.122.101.113) 50.167 ms 48.970 ms 49.636 ms

  9 border202.bb22.lap.net (216.252.255.101) 59.414 ms 62.148 ms 51.337 ms

  10 internet-3.border202.14.lap.net (216.252.253.234) 51.930 ms 51.947 ms 50.748 ms

  11 * * *

  12 * * *

  13 * * *

  14 * * *

  15 * * *
```

`*` 代表什么？每个 `*` 都表示一个超时。`traceroute` 无法理解 `*`，但它可以告诉你哪些节点没有响应。如果你想让 `traceroute` 运行更长时间，可以使用 `-w` 选项。

## 第五部分：网络

当你使用 `Ethereal` 时，别忘记关闭混杂模式。

```
# ifconfig eth0 -promiscuous

# ifconfig eth0

eth0 link encap:Ethernet Rx Haddr 00:02:8A:36:48:8A

inet addr:192.168.0.143 Bcast:192.168.0.255 Mask:255.255.255.0

inet6 addr:fe80::258:8ff:fe36:a84/64 Scope:Link

UP BROADCAST MULTICAST MTU:1500 Metric:
```

你可以更改（或“伪造”）你网络设备的硬件 MAC 地址。这通常仅用于绕过互联网服务提供商（`ISP`）将互联网服务绑定到特定机器的尝试。在伪造 MAC 地址时要小心，因为错误可能会与其他网络设备发生冲突，导致问题。如果你决定伪造 MAC 地址，请确保你先单独使用 `ifconfig` 获取默认 MAC 地址，以便以后可以回滚（顺便说，此示例显示的 MAC 地址完全是虚造的，不要尝试使用它）。

```
# ifconfig eth0 hw ether 00:14:CC:00:01:A0
```



`ifconfig` 命令是处理网络接口的基础。确保你理解它的工作原理，以便充分利用它提供的所有功能。

## 查看你的网络接口状态

### `ifconfig`

`ifconfig` 命令显示你网络接口的状态，即使是无线接口也是。然而，它无法显示与无线接口相关的所有数据，因为 `ifconfig` 根本不知道它的。要获取与无线卡相关的最多的数据，你必须使用 `iwconfig` 而不是 `ifconfig`。

```
$ iwconfig

lo  wireless extensions.

eth0  wireless extensions.

ath0 IEEE 802.11g ESSID:"stein"

Mode:Managed Frequency:2.43 GHz Access Point: 00:12:17:31:4F:C6

Bit Rate:48 Mb/s Tx-Power:18 dB Sensitivity:0/3

Retries: thro8 Fragment: thro8

Power Management:off

Link Quality:41/94 Signal level=-54 db Noise level=-95 dm

Rx invalid nwid:104 Rx crypt:0 Rx invalid frag:0

Tx exceed retries:73 Invalid misc:73 Missing beacon:21
```

你可以看到 `iwconfig` 提供的数据，包括连接类型（在本例中为 802.11）、ESSID 或网络名称（此网络的 ESSID 为 einstein）、你所连接的网络模式或类型、无线接入点的 MAC 地址（此处为 00:12:17:31:4F:C6）以及关于无线连接的各种细节。

`ifconfig` 和 `iwconfig` 的结合告诉了你关于无线网络接口需要的所有信息。而且，正如你也可以使用 `ifconfig` 配置有线网卡一样，你也可以使用 `iwconfig` 配置无线网卡，正如你将在下一节看到的。

## 配置无线网络接口

### `iwconfig`

在上一节“查看你的无线网络接口状态”中，你使用了 `iwconfig` 来查看关于无线网卡及其连接的重要细节。然而，你也可以使用 `iwconfig` 来配置无线网卡及其连接。如果这听起来像 `ifconfig`，那确实如此，`iwconfig` 是基于 `ifconfig` 及其行为的。

**注意**

你可以通过 `iwconfig` 进行若干更改，但你只会查看其中几个（更多详情，请参见 `man iwconfig`）。

与有线网络相关的网络拓扑（例如星型、总线型和环型等）早已为人知并理解了很长时间。无线网络引入了新的拓扑结构，包括：

- `Managed`（管理模式：接入点创建一个无线设备连接的网络；无线网络中最常见的拓扑）
- `Ad-Hoc`（节点：两个或多个无线设备形成一个网络相互工作）
- `Master`（主节点：无线设备充当接入点）
- `Repeater`（中继：无线设备将数据转发到其他无线设备）

还有其他的，但这些是主要的。使用 `iwconfig`，你可以告诉无线网卡你想根据新的拓扑以不同的方式运行。

**提示**

关于星型、总线型、环型等的更多信息，请访问维基百科的“网络拓扑”：`http://en.wikipedia.org/wiki/Network_topology`。

```
iwconfig ath0 mode ad-hoc
```

在指定接口后，只需在你想要使用的模式名称后使用模式选项即可。

**注意**

记住你在这些示例中使用的网卡接口名称为 `eth0`；你的可能是 `eth1`、`wlan0` 或完全不同的名称。要找到你的接口名称，请如上一节所述，单独使用 `iwconfig`。

扩展服务集标识符（ESSID）是你已加入或想要加入的无线网络的名称。在大多数情况下，任何 ESSID 名称都可以很好地工作，前提是你能够满足网络的其他需求，例如加密（如果需要的话）。然而，某些网络要求你指定精确的 ESSID。

```
# iwconfig eth0 essid einstein
```

在此处，你指定 ESSID 紧跟其后的是名称。然而，更多的网络要求你指定精确的 ESSID。

`ifconfig` 命令显示你网络接口的状态，即使是无线接口也是。然而，它无法显示与无线接口相关的所有数据，因为 `ifconfig` 根本不知道它的。要获取与无线卡相关的最多的数据，你必须使用 `iwconfig` 而不是 `ifconfig`。

`ifconfig` 命令是处理网络接口的基础。确保你理解它的工作原理，以便充分利用它提供的所有功能。

你可以更改（或“伪造”）你网络设备的硬件 MAC 地址。这通常仅用于绕过 互联网服务提供商（ISP）将互联网服务绑定到特定机器的尝试。在伪造 MAC 地址时要小心，因为错误可能会与其他网络设备发生冲突，导致问题。如果你决定伪造 MAC 地址，请确保你先单独使用 `ifconfig` 获取默认 MAC 地址，以便以后可以回滚（顺便说，此示例显示的 MAC 地址完全是虚造的，不要尝试使用它）。

```
# ifconfig eth0 hw ether 00:14:CC:00:01:A0
```

当你使用 Ethereal 时，别忘记关闭混杂模式。

```
# ifconfig eth0 -promiscuous

# ifconfig eth0

eth0 link encap:Ethernet Rx Haddr 00:02:8A:36:48:8A

inet addr:192.168.0.143 Bcast:192.168.0.255 Mask:255.255.255.0

inet6 addr:fe80::258:8ff:fe36:a84/64 Scope:Link

UP BROADCAST MULTICAST MTU:1500 Metric:
```

## 查看你的网络接口状态

### `ifconfig`

`ifconfig` 命令显示你网络接口的状态，即使是无线接口也是。然而，它无法显示与无线接口相关的所有数据，因为 `ifconfig` 根本不知道它的。要获取与无线卡相关的最多的数据，你必须使用 `iwconfig` 而不是 `ifconfig`。

```
$ iwconfig

lo  wireless extensions.

eth0  wireless extensions.

ath0 IEEE 802.11g ESSID:"stein"

Mode:Managed Frequency:2.43 GHz Access Point: 00:12:17:31:4F:C6

Bit Rate:48 Mb/s Tx-Power:18 dB Sensitivity:0/3

Retries: thro8 Fragment: thro8

Power Management:off

Link Quality:41/94 Signal level=-54 db Noise level=-95 dm

Rx invalid nwid:104 Rx crypt:0 Rx invalid frag:0

Tx exceed retries:73 Invalid misc:73 Missing beacon:21
```



你可以看到`iwconfig`提供的数据，包括连接的类型（在本例中为 802.11）、ESSID 或网络名称（此网络的 ESSID 为`einstein`）、你所连接的网络模式或类型、无线接入点的 MAC 地址（此处为`00:12:17:31:4F:C6`）以及关于无线连接的各种细节。

`ifconfig`和`iwconfig`的结合告诉了你关于无线网络接口需要的所有信息。而且，正如你也可以使用`ifconfig`配置有线网卡一样，你也可以使用`iwconfig`配置无线网卡，正如你将在下一节看到的。

## 配置无线网络接口

### `iwconfig`

在上一节“查看你的无线网络接口状态”中，你使用了`iwconfig`来查看关于无线网卡及其连接的重要细节。然而，你也可以使用`iwconfig`来配置无线网卡及其连接。如果这听起来像`ifconfig`，那确实如此，`iwconfig`是基于`ifconfig`及其行为的。

**注意**

你可以通过`iwconfig`进行若干更改，但你只会查看其中几个（更多详情，请参见`man iwconfig`）。

与有线网络相关的网络拓扑（例如星型、总线型和环型等）早已为人知并理解了很长时间。无线网络引入了新的拓扑结构，包括：

- `Managed`（管理模式：接入点创建一个无线设备连接的网络；无线网络中最常见的拓扑）
- `Ad-Hoc`（节点：两个或多个无线设备形成一个网络相互工作）
- `Master`（主节点：无线设备充当接入点）
- `Repeater`（中继：无线设备将数据转发到其他无线设备）

还有其他的，但这些是主要的。使用`iwconfig`，你可以告诉无线网卡你想根据新的拓扑以不同的方式运行。

**提示**

关于星型、总线型、环型等等的更多信息，请访问维基百科的“网络拓扑”：http://en.wikipedia.org/wiki/Network_topology。

```bash
iwconfig ath0 mode ad-hoc
```

在指定接口后，只需在你想要使用的模式名称后使用模式选项即可。

**注意**

记住你在这些示例中使用的网卡接口名称为`eth0`；你的可能是`eth1`、`wlan0` 或完全不同的名称。要找到你的接口名称，请如上一节所述，单独使用`iwconfig`。

扩展服务集标识符（ESSID）是你已加入或想要加入的无线网络的名称。在大多数情况下，任何 ESSID 名称都可以很好地工作，前提是你能够满足网络的其他需求，例如加密（如果需要的话）。然而，某些网络要求你指定精确的 ESSID。

```bash
# iwconfig eth0 essid einstein
```

在此处，你指定 ESSID 紧跟其后的是名称。然而，更多的网络要求你指定精确的 ESSID。

## 使用 DHCP 获取新地址

### `dhclient`

大多数网络和许多业务网络使用动态主机主机协议（DHCP）为新机器分配 IP 地址和其他信息。没有 DHCP，任何新机器都必须硬编码其所有的网络信息；有了 DHCP，新机器只需接入网络，请求 DHCP 服务器提供 IP 地址，然后自动将 DHCP 服务器的回复整合到其配置中。

**注意**

以下讨论假设你已将网络设备配置为使用 DHCP 而不是硬编码设置。各种 Linux 发行版位于不同的配置：基于 Debian 的发行版在 `/etc/network/interfaces` 中查找 `[interface] net dhcp`。红帽发行版希望在 `/etc/sysconfig/network-scripts/ifcfg-[interface]` 中使用 `IPPROTO=dhcp`。在这些示例中，将 `[interface]` 替换为你的接口名称。更多信息，请在 Google 上搜索“dhcp your-distro”。

有时你的网络无法连接到 DHCP 服务器，或者你需要手动初始化 DHCP 请求。你可能有需要新 IP 地址的网络问题。无论原因如何，`dhclient` 命令都会查询任何可用 DHCP 服务器获取所需数据（`dhclient` 必须运行）。

```bash
# dhclient eth0
```

```
# 第五部分：网络

DHCPACK from 192.168.0.1
bound to 192.168.0.104 -- renewal in 37250 seconds.
# ifconfig eth0
eth0 link enc:Ethernet HWaddr 00:0BC:CD:3B:20:E2
inet addr:192.168.0.104 Broadcast:192.168.0.255 Mask:255.255.255.0
inet6 addr: fe80::200:cff:fe3b:20e2/64 Scope:Link
```

要释放 DHCP 服务器分配给你的 IP 地址，请使用 `-r`（release）选项。

```bash
# dhclient -r eth0
sit0: unknown hardware address type 776
sit0: unknown hardware address type 776
sit0 listening on LPF/eth0/00:00:cd:3b:20:e2
Sending on LPF/eth0/00:00:cd:3b:20:e2
Sending on Socket/fallback
```

理想情况下，`dhclient` 命令应该在你启动电脑、插入无线 PCMCIA 卡或将以太网线连接有线接口时自动运行，但它有时并不这样做。当 DHCP 正常工作时，请使用 `dhclient`。特别方便的是 `dhclient` 会自动开启详细模式，你可以看到发生了什么并在需要时进行诊断。

### 注意

某些 Linux 发行版仍在使用较旧的程序 `DHCPpump` 而不是 `dhclient`。有关 `pump` 的信息，请查看 `man pump`，或者阅读 Red Hat 和 Mandrake 的博客 HOWTO：www.faqs.org/docs/Linux-mini/DHCPtemp0279.html#REDHAT6。

# 激活网络连接

## `ifup`

实际上，你一直在在没有察觉的情况下使用 `ifup` 命令。当你启动电脑发现已成功连接到互联网时，你可以感谢 `ifup`。当你向 Linux 盒的端口插入以太网线，几秒钟后你就能再次收发邮件，那是 `ifup` 承担了大量工作。本质上，`ifup` 在检测到网络事件（如重启或插入电缆）时运行，并执行你的网络接口配置文件中找到的指令（如果你感兴趣，预测部分中的一个说明讨论了这些文件的名称和位置）。

有时，你可能会遇到网络问题并需要手动运行 `ifup`。这非常简单：以 root 身份登录，然后在 `ifup` 后面跟上你想要激活的网络接口名称。

```bash
# ifconfig
lo Link enc:Local Loopback
inet addr:127.0.0.1 Mask:255.255.0.0
```

```bash
# ifup eth0
# ifconfig
eth0 encap:Ethernet Hwaddr 00:0B:CD:3B:20:E2
inet addr:192.168.0.14 Mask:255.255.255.0
inet6 addr: fe80::20c:cdff:fe3b:202/64 Scope:Link
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
```

```bash
lo Link encap:Local Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
```

请注意，`ifup` 并不会告诉你它执行成功了。事实上，像大多数 Unix 应用一样，`ifup` 在成功时是沉默的，只有在遇到失败或错误时才会提示。要查看 `ifup` 完成了什么，请使用 `ifconfig`。

### 注意

你也可以 `ifconfig [interface] up` 或 `iwconfig [interface] up` 来激活有线或无线连接。

# 关闭网络连接

## `ifdown`

`ifup` 命令激活连接，而 `ifdown` 命令将其关闭。你为什么需要关闭网络连接？很多时候，你尝试激活它，但 `ifconfig` 报告它已启用，所以你先关闭它，然后再激活它。

```bash
# ifup eth0
ifup: interface0 already configured
# ifdown eth0
# ifup eth0
```

注意 `ifdown` 和 `ifup` 一样，在成功时是沉默的。如果你输入 `ifdown` 后没有看到输出，说明命令执行成功，该网络接口不再工作。

### 注意

你也可以使用 `ifconfig eth0 down` 或 `iwconfig eth0 down` 来关闭有线或无线连接。

# 显示你的路由表



当你尝试使用安全 Shell (`SSH`) 连接局域网内的另一台电脑时（将在第 15 章介绍），答案是你的 Linux 内核有一个跟踪这些内容的路由表。查看当前的路由表，只需在 shell 中输入`route`（注意，查看路由表不需要`root`权限，但修改需要，如下文所示）。

```
route
Kernel IP routing table
| Destination | Gateway | Genmask | Flags | Metric | Ref | Iface |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 192.168.0.0 | * | 255.255.255.0 | U | 0 | | eth0 |
| default | 192.168.0.1 | 0.0.0.0 | UG | 0 | | eth0 |
```

### 注意

这台机器只有一个网络接口，这是一个简单的路由表。在同时拥有以太网口和无线卡的笔记本电脑上，你会看到额外的条目。IP 地址由四个字节组成，显示为`xxx.xxx.xxx`，如`192.168.0.1`。当你从机器发送数据包时，数据包的 IP 地址与路由表中的`Destination`列进行比较。`Genmask`与`Destination`列配合工作，确定应该检查四个字节中的哪一个。例如，允许你在 shell 中输入`192.168.0.124`。掩码为`255.255.255.0`的掩码只识别由`.124`表示的地址。换句话说，当查找`192.168.0.124`时，`.124`是路由数据包的目标。任何指向`192.168.0.1`的数据包匹配 IP 地址的限制，因此它们留在局域网内并避免经过路由器。这就是为什么`192.168.0.0`旁边的 Gateway 列是`*`的原因，因为流量是局部的。另一方面，其他所有内容都指向路由器，即 Gateway 列中的`192.168.0.1`。这里的掩码是`0.0.0.0`，表示任何不匹配`192.168.0.1`到`192.168.0.255`的地址都应该通过`192.168.0.1`发送（因为`192.168.0.1`是网关，这是一个特殊情况）。`72.14.203.99`、`82.211.81.166`和`216.23.180.5`都匹配`0.0.0.0`，所以它们必须通过网关。表中另一个有趣的地方是`Flags`，它提供了有关路由的信息。有多种标记，常见的是`U`（路由已启用）和`G`（网关）。在上表中，你可以看到两条路由都是启用的，但只有……

# 修改你的路由表

`route`命令不仅可以用于查看路由表，还可以用于修改它。然而，你需要小心，因为你可能会破坏网络并实际上锁定你的电脑。假设你的机器不断丢失网关，导致任何数据包都无法离开局域网到达互联网（这种情况以前很愉快地发生在我一台机器上）。运行`route`命令验证网关是否缺失，然后在`route`中添加它（尽管可以用普通用户身份查看路由，但修改`route`需要`root`权限）。

```
# route
Kernel IP routing table
| Destination | Gateway | Genmask | Flags | Metric | Ref | Interface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 192.168.0.0 | * | 255.255.255.0 | U | 0 | | eth0 |
```

```
# route add -net default 192.168.0.1 dev eth0
# route
Kernel IP routing table
| Destination | Gateway | Genmask | Flags | Metric | Ref | Interface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 192.168.0.0 | * | 255.255.255.0 | U | 0 | | eth0 |
| default | 192.168.0.1 | 0.0.0.0 | UG | 0 | | eth0 |
```

让我们拆解如何添加。`add`表示你正在添加一个网络（要删除一个请使用`del`）。`-net`选项表示你要添加的是一个网络，在此处是默认路由。`gw`表示你想要路由数据包的网关，在此处是`192.168.0.1`（使用了`0.0.0.0`的掩码）。最后，`dev`指定使用的设备，在此处是以太网卡`eth0`。

假设除了以太网口`eth0`之外，你还有一张无线卡`ath0`。你想让无线卡访问局域网内的资源，局域网使用`10.1.xxx.xxx`。你希望无线卡能够访问互联网。为了添加匹配规则的路由，使用这些命令：

```
route
Kernel IP routing table
| Destination | Gateway | Genmask | Flags | Metric | Ref | Interface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 192.168.0.0 | * | 255.255.255.0 | U | 0 | | eth0 |
| default | 192.168.0.1 | 0.0.0.0 | UG | 0 | | eth0 |
# route add -net 10.1.0.0 netmask 255.255.255.0 dev ath0
# route
Kernel IP routing table
| Destination | Gateway | Genmask | Flags | Metric | Ref | Interface |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 192.168.0.0 | * | 255.255.255.0 | U | 0 | | eth0 |
| default | 192.168.0.1 | 0.0.0.0 | UG | 0 | | eth0 |
| 10.1.0.0 | * | 255.255.255.0 | U | 0 | | ath0
```

## 第五部分：网络

```
| 目标 | 网关 | 子掩码 | 标志 | 标量 | 引用 | 接口 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 192.168.0.0 | * | 255.255.255.0 | U | 0 | 0 | eth0 |
| 10.1.0.0 | * | 255.255.255.0 | U | 0 | 0 | eth0 |
| default | 192.168.0.1 | 0.0.0.0 | UG | | 0 | eth0 |

# route -net 10.1.0.0 netmask 255.255.255.0 dev eth0
# route
| 目标 | 网关 | 子掩码 | 标志 | 标量 | 引用 | 接口 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 192.168.0.0 | * | 255.255.255.0 | U | 0 | 0 | eth0 |
| default | 192.168.0.1 | 0.0.0.0 | UG | | 0 | eth0 |
```

一切都是那样的，你只需使用替换而不是添加。现在太简单了！

## 网络故障排除

如今的 Linux 在网络方面通常是“开箱即用”，但你可能仍然遇到问题。这里是一些用于网络故障排除的基本提示。

如果你的网络接口无法运行和绑定，导致无法上网，请首先尝试`ping`你的本地设备设备`127.0.0.1`。如果无效，请停止并不要继续，因为你的系统已经遭受了严重损坏。如果有效，`ping`你的机器的外部 IP 地址。如果无效，请确保你的机器上开启了网络功能。如果有效，尝试`ping`网络中的其他机器（假设你有其他机器的话）。如果你不确定，那可能是接口的问题（假设你的路由器是好的）。确保你的电缆已插好（认真的）。使用`ifconfig`（如果是`ifconfig`则忽略）来验证接口状态，并在必要时使用`ifup`开启接口。然后再次`ping`。

如果你尝试`ping`另一台本地计算机成功了，尝试`ping`你的路由器。如果你可以访问网络上的其他机器，但无法访问路由器，那么是时候使用`route`检查你的路由表了，详见“显示你的 IP 路由表”章节。如果你的路由表中缺少项，请添加它们，方法如“更改你的 IP 路由表”。

如果你有一个可以参考的工作基准，诊断和修复问题会容易得多。在确定机器的网络是正确的后，运行`route`并保存结果，这样当路由表出现混乱且你以后需要恢复某些时，可以使用蓝图。



如果你能到达路由器，`ping` 一个你将上网的机器，例如 `www.google.com` 或 `www.apple.com`。如果无效，尝试 `ping` 该机器的 IP 地址。这意味着你需要在便利签或文本文件中为电脑记录一些 IP 地址，以备不时之需。这里有几个目前好用的；当然，它们会变化，所以你真的应该自己去查。

| 站点 | IP 地址 |
| :--- | :--- |
| `www.google.com` | `72.144.203.99` |
| `www.apple.com` | `17.254.0.991` |
| `www.ubuntu.com` | `82.211.81.166` |
| `www.ibm.com` | `129.42.16.99` |
| `www.granneman.com` | `216.23.180.5` |

### 注意

你是如何获取 IP 地址的？你可以使用域名 `ping` 机器，`ping` 会给你 IP 地址，或者你可以通过 `traceroute` 获取相同的结果。更快的方法是使用 `host` 命令，这在之前的“执行 DNS 查询”中介绍过。

如果你可以获取 IP 地址但无法获取域名，说明你有 DNS 问题。如果你正在使用 DHCP，是时候运行 `dhclient` 来“使用 DHCP 获取新地址”，以尝试刷新由 DHCP 服务器提供的 DNS 信息。如果你没有使用 DHCP，请通过查看路由器或询问你的管理员或 ISP 获取所需的 DNS 信息，然后将其手动添加到 `/etc/resolv.conf` 中，例如如下所示：

```
nameserver 24.217.0.5
nameserver 24.217.0.55
```

那是 `nameserver`（一个必须的单词），后面跟着你应该用于 DNS 的 IP 地址。如果你的路由器可以处理，并且你知道它的 IP（假设是 `192.168.0.1`），你总是可以尝试这样做：

```
nameserver 192.168.0.1
```

尝试 `ifdown` 然后执行 `ifup` 看看是否有效。如果你仍然遇到问题，是时候重新开始了，从始终检查开始。一切都安装得当吗？一切都插好了吗？在检查软件后，最坏的情况是你的硬件没有适用于 Linux 的驱动程序。这很少见，而且也很少总是这样，但仍然会发生。

无线网卡与那些不想提供帮助的 Linux 厂商极度不兼容。为了防止头疼，最好在使用之前先查看无线信息（假设在 `http://madwifi.org/` 或 `http://linux.org/` 或 `http://dell.com/`）。

### 结论

你已经掌握了 Linux 下的许多工具，诸如 `ifconfig`、`ifup`、`ping`、`route`、`traceroute` 等。

## 无需密码安全登录另一台机器

本节的名称似乎是一个误名之实，但通过 `ssh` 登录机器而无需提供密码是完全可能的。如果你每天都要登录某台特定的电脑（我有几台机器每天可能会登录好几次），那么本节中的技术将让你非常开心。

假设你想从 `pound`（用户名：`ezra`）登录到 `eliot`（用户名：`tom`），而不需要你输入密码。首先，在 `pound` 上使用以下命令创建一个 `ssh` 身份认证密钥：

```
$ ssh-keygen -t dsa
Generating public/private dsa key pair.
Enter file in which to save the key (/home/ezra/.ssh/id_dsa):
Enter passphrase (empty for no passphrase):
Enter passphrase again:
Your identification has been saved in /home/ezra/.ssh/id_dsa.
Your public key has been saved in /home/ezra/.ssh/id_dsa.pub
The key fingerprint is:
30:a4:a7:31:27:d61:821e:76:e:ed:6b:96:3c:24:ezrapound
```

按回车键接受默认的密钥保存位置，并按两次回车键留空密码。你刚刚在 `~/.ssh/id_rsa` 创建了一个密钥，并在 `~/.ssh/id_rsa.pub` 创建了一个公钥。

现在，你需要将公钥从 `pound` 传输到 `eliot`。`ssh` 的开发者们正与你站在一起，他们创建了一个程序，让这一切变得像掉木桩一样简单。要将你的公钥从 `pound` 拷贝到 `eliot`，请使用以下命令：

```
$ ssh-copy-id -i ~/.ssh/id_dsa.pub tom@192.168.0.25
```

现在尝试使用 `ssh@192.168.0.25` 登录机器，并检查 `.ssh/authorized_keys` 以确保你没有添加意料之外的额外密钥。

大功完成了（尽管如果你想遵循 `ssh-copy-id` 提供的建议，尽管可以这样做）。现在看一看你从 `pound` 运行 `eliot` 使用 `ssh` 命令时会发生什么：

```
$ ssh@192.168.0.25
Linux eliot 2.6.2-10-386 #1 Mon Jan 16 17:18:08 UTC 2006 i686 Linux
Last login: Mon Feb 22:40:31 2006 from 192.168.0.15
```

现在你没有被要求输入密码，这正是你想要的。

你们中可能有些人会好奇这种技巧的安全性。没有密码？随意交换密钥？确实如此，但请思考一下。如果有人进入了 `pound`，他现在就可以无密码连接到 `eliot`。这仅仅意味着你需要在 `pound` 上养成良好的安全防护习惯。如果 `pound` 被攻破，无论攻击者是否意识到他也可以进入 `eliot`，你都会面临巨大的问题。此外，你经常在互联网上到处发送密码。如果攻击者获取了你的密码，他们可以造成巨大的破坏。你的私钥难道不像密码一样重要吗？而且你不是会对其备份并保护它吗？当你从这些角度考虑时，通过 `ssh` 交换密钥至少和密码一样安全，在许多方面更安全。

尽管如此，如果你倾向于保留密码，那当然是你的权利。这正是开源和 Linux 的意义所在：选择。

# 第五部分：网络

## 在机器间安全传输文件

`SFTP` 远优于 `FTP`。正如 `ssh` 远优于 `telnet` 一样，`SFTP` 也远优于 `FTP`。像 `telnet` 一样，`FTP` 将你的用户名密码以及所有传输的数据都明文发送，任何嗅探数据包的人都可以窃听。相反，`SFTP` 使用 `ssh` 加密所有内容：用户名、密码和流量。除了安全了大约百万倍之外，它在命令上与 `FTP` 非常相似，这使其易于学习和使用。

如果你通过 `ssh` 访问机器，你也可以对其进行 `SFTP`。从 `pound`（`192.168.0.15`；用户名 `ezra`）使用 `sftp` 命令访问 `eliot`（`192.168.0.25`；用户名 `tom`），只需使用此命令：

```
$ sftp tom@192.168.0.25
Connecting to 192.168.0.25...
tom@192.168.0.25's password:
sftp>
```

如果你读过上一节“无需密码登录另一台机器”，你可能在奇怪为什么会提示你输入密码。你是正确的：之前的示例是在设置无需密码的连接之前取的。在你完成操作后，你将看到类似这样的登录：

```
$ sftp tom@192.168.0.25
Connecting to 192.168.0.25...
sftp>
```

在通过 `sftp` 登录后，你可以运行的命令相当标准。表 15.1 列出了一些最常用的命令；如需完整列表，请查阅 `man sftp`。

### 表 15.1. 有用的 SFTP 命令

| 命令 | 含义 |
| :--- | :--- |
| `cd` | 切换目录 |
| `exit` | 关闭连接 |
| `get` | 从远程下载文件到本地 |
| `help` | 获取帮助 |
| `ls` | 列出远程文件 |
| `put` | 将文件上传到远程服务器 |
| `rm` | 删除远程服务器的文件 |

## 主机间的安全拷贝文件

由于 `ssh` 远优于 `telnet`，`SFTP` 也远优于 `FTP`。当你需要从一台机器向另一台机器拷贝文件时，`scp` 是非常有用的。但是，如果你有大量文件需要拷贝，你会发现 `scp` 变得非常繁琐。在这种情况下，你可能想使用通配符。`scp` 基本上是由 `ssh` 的开发者们创建的，他们正与你站在一起，他们创建了一个程序，让这一切变得像掉木桩一样简单。假设你想从 `pound`（`192.168.0.15`；用户名 `ezra`）向 `eliot`（`192.168.0.25`）拷贝一些文件，只需使用此命令：

```
$ scp * tom@192.168.0.25:/path/to/destination
Connecting to 192.168.0.25...
```

（此处上）

在你完成操作后，你将看到类似这样的登录：

```
$ scp * tom@192.168.0.25:/path/to/destination
Connecting to 192.168.0.25...
```



在通过 `sftp` 登录后，你可以运行的命令相当标准。表 15.1 列出了一些最常用的命令；如需完整列表，请查阅 `man sftp`。

### 表 15.1. 有用的 SFTP 命令

| 命令 | 含义 |
| :--- | :--- |
| `cd` | 切换目录 |
| `exit` | 关闭连接 |
| `get` | 从远程下载文件到本地 |
| `help` | 获取帮助 |
| `ls` | 列出远程文件 |
| `put` | 将文件上传到远程服务器 |
| `rm` | 删除远程服务器的文件 |

## 主机间的安全拷贝文件

当你需要从一台机器向另一台机器拷贝文件时，`scp` 是非常有用的。但是，如果你有大量文件需要拷贝，你会发现 `scp` 变得非常繁琐。在这种情况下，你可能想使用通配符。`scp` 基本上是由于 `ssh` 的开发者们正与你站在一起，他们创建了一个程序，让这一切变得像掉木桩一样简单。假设你想从 `pound`（192.168.0.15；用户名 `ezra`）向 `eliot`（192.168.0.25）拷贝一些文件，只需使用此命令：

在 `/home/ezra` 目录下：

```bash
$ scp *.jpg tom@192.168.0.25:/home/tom/
```

此命令会将当前目录下所有的 `.jpg` 文件拷贝到 `eliot` 的 `/home/tom` 目录。

如果你想拷贝整个目录，可以使用 `-r` 参数：

```bash
$ scp -r /home/ezra/pictures tom@192.168.0.25:/home/tom/
```

由于，如果你读过上一节“无需密码登录另一台机器”，你可能在奇怪为什么会提示你输入密码。你是正确的：之前的示例是在设置无需密码的连接之前取的。在你完成操作后，你将看到类似这样的登录：

```bash
$ tom@192.168.0.25
Connecting to 192.168.0.25...
sftp>
```

## 第五部分：网络连接

这里有一个在 `coleridge` 上运行的命令，可以将 `documents` 目录的所有内容传输到备份 `dwords` 中。查看该命令，查看结果，然后你就可以了解选项的含义（为了可读性，命令内部使用了长选项，随后给出了单字母选项的对比）。

```bash
rsync --verbose --progress --stats --recursive --times --perms --links --compress
--rsync -sh --delete /home/sam/documents/will/wordsworth/media/backup/documents
```

```bash
$ rsync -v --progress --stats -r t -p -l -e ssh --delete /home/sam/documents/
will@media/backup/documents
```

当然，如果你想合并所有选项，可以再次运行此命令：

```bash
rsync --vrtple ssh --progress --stats --delete /home/sam/documents/will@/media/backup/documents
```

在使用列出的任何方法运行 `rsync` 后，你会看到类似的内容：

```text
file list ...
107805 files to consider
deleting cliente/Linux_Magazine/do_it_yourself/13/gant_chart.txt
deleting Security/diebold_voting/black_box_voting/bbv_voting-9.pdf
deleting E-Commerce/Books/20050081 Eay LIB AN DAILIES 6 1940.txt
Security/electronic_voting/diebold/black_box_voting/bbv_chapter-9.pdf
legal_issues/free_speech/Timeline A history of free speech.txt
E-Commerce/Books/20050081 Eay LIB AN DAILIES 6 1940.txt
connectivity/info.txt
[Results greatly truncated for length]
Number of files: 107805
Number of files transferred: 120
Total file size: 672042249 bytes
Total transferred file size: 15337159 bytes
File list size: 2344115
Total bytes sent: 2345101
Total bytes received: 986
sent 2345101 bytes received 986 bytes 7507.48 bytes/sec
total size is 672042249 speedup in 22856.66
```

查看这些结果，`rsync` 首先构建一个它必须考虑的所有文件列表（在本例中为 107805 个），删除目标端（`wordsworth`）上在源端（`coleridge`）已不存在的文件。在这个示例中，有三个文件被备份删除：一个来自《Linux Magazine》的文章（通过 `~` 符看出）、一个关于电子投票的 PDF，以及一份购买书籍的收据。

在删除文件后，`rsync` 会复制任何已更改的文件；如果是相同的文件，则只复制文件的更改部分，这就是 `rsync` 如此高效的原因。在这种情况下，复制了四个文件。然后它发现该 PDF 实际上被 `rsync` 移动到了子目录并生成了新文件，因此被完整地复制了。

文本收据也是如此。`history of free speech.txt` 是一个全新的文件，因此它也被复制到了 `wordpress`。



在完成更改后，`rsync` 会向你提供关于整个传输过程的信息。传输了 120 个文件，从 672042249 字节（约 6.4GB）传输了 15337159 字节（约 14MB）。汇总中包含其他数据点，但这些是关键的。

现在看看你要求计算机的操作。命令的开头和结尾很容易理解：开头的 `rsync` 命令，后面的选项，然后是你从中复制的源目录（`/home/sam/documents/`，位于 `coleridge`），最后是你要复制到的目标目录（`/media/backup/documents/`，位于 `wordpress`）。在检查选项之前，你需要关注指定的源目录和目标目录，因为其中有一个陷阱，如果你不注意将会导致严重的后果。

你统计的是 `coleridge` 上 `documents` 目录的内容，而不是目录本身，这就是为什么你使用 `documents/` 而不是 `documents`。`/home/sam/documents/` 中 `documents` 之后的斜杠告诉 `rsync` 你统计的是位于 `wordpress` 上的该目录的内容；如果你使用 `documents`，你将复制整个目录及其内容，导致在 `worthless` 上生成 `/media/backup/documents/`。

> **注意**
>
> 斜杠仅在源端很重要；目标目录上使用斜杠并不重要。

有一个之前没有列出的选项，但在运行 `rsync` 命令时包含它是个好主意，即：`-n`（或 `--dry-run`）。如果你包含该选项，`rsync` 会运行但不会自动删除或复制任何内容。如果你的选择可能会导致重要文件被删除，这将是救命稻草。在提交 `rsync` 命令之前（特别是当你使用 `--delete` 选项时），请帮自己先进行一次干运行（`dry run`）。

现在来看你使用的选项。`-v`（或 `--verbose`）选项配合 `--progress` 非常有用，因为它向你展示正在发生什么。`-z`（或 `--compress`）选项在传输期间压缩数据，这在慢连接上非常有用。`-r`（或 `--recursive`）选项让 `rsync` 复制子目录。`-t`（或 `--times`）选项保留修改时间。`-p`（或 `--perms`）选项保留权限。`-l`（或 `--links`）选项复制符号链接。`-e`（或 `--rsh-ssh`）选项允许你通过 `ssh` 隧道传输。

第一行是解释作业用途的注释，第二行告诉 `cron` 每天凌晨 3:05 自动运行 `/home/scott/bin/backup.sh`。

现在将该作业添加到 `cron` 中：

```bash
$ crontab /home/scott/bin/cronfile
```

现在，你再也不需要担心你的备份问题了。一切都为你自动化了——只需确保你晚上让电脑一直开着即可！

（有关 `cron` 的更多信息，请参阅 `man cron` 或 `www.unixgeeks.org/security/newbie/unix/cron-1.html` 上的“新手：`cron` 简介”）。

## 非交互式下载文件

```bash
wget
```

互联网是可以下载的图片、电影和音乐的宝。问题是，手动从包含 200 个 `MP3` 的集中下载每个文件会迅速变得枯燥，导致大脑腐化和无法控制的口水。`wget` 命令用于在不受任何干扰的情况下下载文件和网站；使用该命令，它会乐意地下载你指定的任何内容，持续数小时直到结束。

困难之处在于，在设置命令时，`wget` 是另一个真正的超级力量，它能为你节省大量书的时间，所以我们没有空间保存你可能下载的所有内容。相反，你将通过 `wget` 关注两件事：下载一大堆文件（这里在这里讨论），以及下载我们想要的所有内容（将在下一节中介绍）。

这里是前提：你发现了一个名为“The Old Radio Archives”（老式收音机存档）的优秀网站。这个网站上有大量的复古收音机声音可以以 `MP3` 格式下载——准确来说有 365 个 `MP3`，对应于每年的每一天。如果能获取这些 `MP3` 就好了，但对每个 `MP3` 超链接点击右键、选择“链接另存为”并点击确定保存下载的愿景并不吸引人。

```
http://www.oldtimeradioarchives.com/mp3/
season_10/
season_11/
...
season_20/
...
season_3/
season_4/
...
season_9/
```

## 第五部分：网络

### 注意事项

目录不是按照人类习惯的数字顺序排序，而是按照字母顺序排序的，除非另有说明，否则计算机就是这样对数字的。毕竟，“ten”在字母顺序上排在“three”之前。

每个目录内部都有 `MP3` 文件。有些目录只有几个文件，而有些则接近 20 个。如果你点击目录链接，你将得到一个列出该目录下文件的网页，如下所示：

| 名称 | 日期/时间 | 大小 |
| :--- | :--- | :--- |
| [BACK] 父级目录 | 2002-5月19日 01:03 | - |
| [SND]1944-12-24_532.mp3 | 2002-7月06日 13:54 | 6.0M |
| [SND]1944-12-31_533.mp3 | 2002-7月06日 14:28 | 6.5M |
| [SND]1945-01-07_534.mp3 | 2002-7月06日 20:05 | 6.8M |

`[SND]` 是一个音符的 `GIF` 图片，显示在每个文件列表前面。

所以问题是，你如何下载这些文件名不同且存在于不同目录中的 `MP3` 文件？答案是使用 `wget`！

首先在你的计算机上创建一个目录，并在其中下载 `MP3` 文件。

```bash
$ mkdir radio_mp3
```

现在使用 `cd` 进入该目录，然后运行 `wget`：

```bash
$ cd radio_mp3
$ wget -r -l2 -w 5 -A.mp3 -temp0281.html http://www.oldtimeradioarchives.com/mp3/
```

让我们梳理一下这个命令及其选项。

`wget` 当然是你正在运行的命令，最末端是你想要使用的 URL：`http://www.oldtimeradioarchives.com/mp3`。不过，重要的内容位于命令和 URL 之间。

`wget` 的 `-r`（或 `--recursive` 递归）选项会让 `wget` 跟踪并进入搜索目录，告诉 `wget` 执行递归操作；你确保了 `wget` 会遍历每个季节的目录，抓取它找到的所有 `MP3`。

`-l2`（或 `--level=#`）选项非常关键且巧妙。它告诉 `wget` 在递归检索文件时进入多深。`level` 代表 `wget` 应该下降的深度。如果你指定层级为 1，`wget` 只查找 `/mp3` 目录。这将导致什么也下载不到。记住，`/mp3` 目录包含了你想要的 `MP3`。通过指定 `-l2`，你是在要求 `wget` 先获取 `/mp3`（这是第一层），然后逐个进入 `season_#` 目录并取其中的任何内容。你需要非常小心地指定层级。如果你不小心，可能会在极短时间内拉满你的硬盘。

避免下载内容超过预期的方法之一是使用 `-np`（或 `--parent`）选项，它能防止 `wget` 递归进入父目录。如果你回看文件列表，你会注意到第一行是父级目录。换句话说，在 `/season_10` 中，父目录是 `/mp3`。换句话说，在 `/season_11` 中，父目录是 `/mp3`。换句话说，在 `/season_12` 中，父目录是 `/mp3`。你不想让 `wget` 向上移动，也不想浪费时间进入你所在的目录（即季节目录）。

下一个选项是必须的，但如果你使用它会显得很有礼貌。`-w`（或 `--wait=#`）选项在每个文件下载之间引入简短的等待。这有助于防止持续请求文件导致服务器过载。默认情况下，`wget` 将数字解释为秒；如果你需要，也可以在数字后添加 `m` 来指定分钟，甚至可以加天。

现在变得有趣了。`-A`（或 `--accept`）选项指定你只想下载特定类型的文件，而不包含其他内容。`A` 代表 `accept`（接受），后面跟着你想要的文件后缀，除非你只需要一种文件：`-Amp3`。

另一方面，`-R`（或 `--reject`）选项告诉 `wget` 你不想要什么：`HTML` 和 `GIF` 文件。

所以问题是，你如何下载这些文件名不同且存在于不同目录中的 `MP3`？答案是 `wget`！

首先在你的计算机上创建一个目录，并在其中下载 `MP3` 文件。

```bash
$ mkdir radio_mp3
```

现在使用 `cd` 进入该目录，然后运行 `wget`：

```bash
$ cd radio_mp3
$ wget -r -l2 -w 5 -A.mp3 -temp0281.html http://www.oldtimeradioarchives.com/mp3/
```

让我们梳理一下这个命令及其选项。



`wget` 当然是你正在运行的命令，最末端是你想要使用的 URL：`http://www.oldtimeradioarchives.com/mp3`。不过，重要的内容位于命令和 URL 之间。

`wget` 的 `-r`（或 `--recursive`递归）选项会让 `wget` 跟踪并进入搜索目录，告诉 `wget` 执行递归操作；你确保了 `wget` 会遍历每个季节的目录，抓取它找到的所有 MP3。

`-l2`（或 `--level=#`）选项非常关键且巧妙。它告诉 `wget` 在递归检索文件时进入多深。`level` 代表 `wget` 应该下降的深度。如果你指定层级为 1，`wget` 只查找 `/mp3` 目录。这将导致什么也下载不到。记住，`/mp3` 目录包含了你想要的 MP3。通过指定 `-l2`，你是在要求 `wget` 先获取 `/mp3`（这是第一层），然后逐个进入 `season_#` 目录并取其中的任何内容。你需要非常小心地指定层级。如果你不小心，可能会在极短时间内拉满你的硬盘。

避免下载内容超过预期的方法之一是使用 `-np`（或 `--parent`）选项，它能防止 `wget` 递归进入父目录。如果你回看文件列表，你会注意到第一行是父级目录。换句话说，在 `/season_10` 中，父目录是 `/mp3`。换句话说，在 `/season_11` 中，父目录是 `/mp3`。换句话说，在 `/season_12` 中，父目录是 `/mp3`。你不想让 `wget` 向上移动，也不想浪费时间进入你所在的目录（即季节目录）。

下一个选项是必须的，但如果你使用它会显得很有礼貌。`-w`（或 `--wait=#`）选项在每个文件下载之间引入简短的等待。这有助于防止持续请求文件导致服务器过载。默认情况下，`wget` 将数字解释为秒；如果你需要，也可以在数字后添加 `m` 来指定分钟，甚至可以加天。

现在变得有趣了。`-A`（或 `--accept`）选项指定你只想下载特定类型的文件，而不包含其他内容。`A` 代表 `accept`（接受），后面跟着你想要的文件后缀，除非你只需要一种文件：`-Amp3`。

另一方面，`-R`（或 `--reject`）选项告诉 `wget` 你不想要什么：`HTML` 和 `GIF` 文件。

所以问题是，你如何下载这些文件名不同且存在于不同目录中的 MP3？答案是 `wget`！

## 第五部分：网络

此选项不仅修复了指向页面的链接，还修复了指向图片、层级样式表文件的链接。你会庆幸自己做了。

提到层级样式表 (CSS) 和图像，这就是你想要使用 `-p` 或 `--page-requisites` 选项的原因。为了让网页能够正确显示，网站开发者可能指定了与 HTML 使用图像、CSS 和 JavaScript 文件。`-p` 选项要求 `wget` 下载显示你正在查看的网页所需的任何文件。有了它，在你的机器上查看该页面后的结果将与你在 Web 上看到的内容完全相同；如果没有它，你可能会得到一个无法使用的文件。

`wget` 的页面非常冗长且详细，如果你想以更高级的方式使用 `wget`，你最终会去那里。如果你觉得 `wget` 听起来很有趣，就开始阅读吧。你会学到很多。

### Note: curl

乍一看，`wget` 和 `curl` 似乎相似：两者都可以非交互式地下载许多文件。然而，在许多细微区别中，它们各有一个巨大的区别：`curl` 在指定下载内容时支持序列和集合，而 `wget` 不支持；而 `wget` 支持递归，这是 `curl` 缺失的一个功能。

### Note

这些程序之间还有许多其他区别。`curl` 功能的完整列表可以在“curl 能做什么”(http://curl.haxx.se/features.html) 中查看，而 `wget` 的某些功能则列在“概述”(www.gnu.org/software/wget/html_node/Overview.html) 中。`curl` 网站有一张图表，通过“将 curl 功能与其他 FTP+HTTP 工具比较”(http://curl.haxx.se/docs/comparison-table.html) 比较 `curl` 与其他类似的程序；虽然该图表很有参考价值，但稍微偏向 `curl`。

这里有一个使用 `curl` 支持的序列能力来指定下载内容的示例。《美国生活》(This American Life) 这档优秀国家公共节目对其文件进行了存档，以便以 Real Audio 格式在你的网站上显示下载（你看到的是 Real 而不是更开放的格式，这是一个谜团）。如果你想下载 100 个 Real Audio 文件，只需使用以下命令：

```
$ curl -O http://www.wbez.org/ta/[1-10].rm
[1/10] http://www.wbez.org/ta/1.rm --> 1.rm
--curl--http http://www.wbez.org/ta/1.rm
```

注意你如何使用 `[1-10]` 来指定你想下载 `1.rm`、`2.rm`、`3.rm` 等。WBEZ 而是将文件命名为 `one.rm`、`two.rm` 和 `three.rm`，例如，你可以使用部分集：

```
$ curl -O http://www.wbez.org/ta/(one,two,three).rm
```

`-O` 或 (`--remote-name`) 选项是绝对要求的。如果你不使用它，`curl` 将其下载的内容输出到标准输出 (`STDOUT`)，你的终端会迅速充满无法使用的 `goodygoodbook`。`-O` 要求 `curl` 将下载的内容写入文件，并使用下载的文件名作为本地文件名。

我们仅仅触及了 `curl` 的冰角。它的手册页（man page）虽然没有 `wget` 那么长，但也充满了如果你想最大限度利用 `curl` 时需要阅读的有用信息。请将其视为必须的。

### 结论

本章中的命令是我个人最喜爱的一些，因为它们允许我完成那些原本会很枯燥、不安全或困难的任务。所有这些命令让网络成为你的数据、程序和想象力的另一个途径，这真的让 Linux 发放异彩。通过为用户提供如 `ssh`、`rsync`、`wget` 和 `curl` 这样强大的工具，Linux 以一种在许多操作系统上无法实现的方式鼓励了创新和安全。



注意你如何使用 `[1-10]` 来指定你想下载 `1.rm`、`2.rm`、`3.rm` 等。WBEZ 而是将文件命名为 `one.rm`、`two.rm` 和 `three.rm`，例如，你可以使用部分集：

```
$ curl -O http://www.wbez.org/ta/(one,two,three).rm
```

## 第五部分：网络

`-O` 或 `--remote-name` 选项是绝对要求的。如果你不使用它，`curl` 将其下载的内容输出到标准输出 (STDOUT)，你的终端会迅速充满无法使用的 `goodygoodbook`。`-O` 要求 `curl` 将下载的内容写入文件，并使用下载的文件名作为本地文件名。

我们仅仅触及了 `curl` 的冰角。它的手册页（man page）虽然没有 `wget` 那么长，但也充满了如果你想最大限度利用 `curl` 时需要阅读的有用信息。请将其视为必须的。

### 结论

本章中的命令是我个人最喜爱的一些，因为它们允许我完成那些原本会很枯燥、不安全或困难的任务。所有这些命令让网络成为你的数据、程序和想象力的另一个途径，这真的让 Linux 发放异彩。通过为用户提供如 `ssh`、`rsync`、`wget` 和 `curl` 这样强大的工具，Linux 以一种在许多操作系统上无法实现的方式鼓励了创新和安全。

## 第五部分：网络

此选项不仅修复了指向页面的链接，还修复了指向图片、层级样式表文件的链接。你会庆幸自己做了它的。

提到层级样式表 (CSS) 和图像，这就是你想要使用 `-p` 或 `--page-requisites` 选项的原因。为了让网页能够正确显示，网站开发者可能指定了与 HTML 使用图像、CSS 和 JavaScript 文件。`-p` 选项要求 `wget` 下载显示你正在查看的网页所需的任何文件。有了它，在你的机器上查看该页面后的结果将与你在 Web 上看到的内容完全相同；如果没有它，你可能会得到一个无法使用的文件。

`wget` 的页面非常冗长且详细，如果你想以更高级的方式使用 `wget`，你最终会去那里。如果你觉得 `wget` 听起来很有趣，就开始阅读吧。你会学到很多。

### Note: curl

乍一看，`wget` 和 `curl` 似乎相似：两者都可以非交互式地下载许多文件。然而，在许多细微区别中，它们各有一个巨大的区别：`curl` 在指定下载内容时支持序列和集合，而 `wget` 不支持；而 `wget` 支持递归，这是 `curl` 缺失的一个功能。

### Note: 其他区别

这些程序之间还有许多其他区别。`curl` 功能的完整列表可以在“curl 能做什么”(`http://curl.haxx.se/features.html`) 中查看，而 `wget` 的某些功能则列在“概述”(`www.gnu.org/software/wget/html_node/Overview.html`) 中。`curl` 网站有一张图表，通过“将 curl 功能与其他 FTP+HTTP 工具比较”(`http://curl.haxx.se/docs/comparison-table.html`) 比较 `curl` 与其他类似的程序；虽然该图表很有参考价值，但稍微偏向 `curl`。

这里有一个使用 `curl` 支持的序列能力来指定下载内容的示例。《美国生活》(This American Life) 这档优秀国家公共节目对其文件进行了存档，以便以 Real Audio 格式在你的网站上显示下载（你看到的是 Real 而不是更开放的格式，这是一个谜团）。如果你想下载 100 个 Real Audio 文件，只需使用以下命令：

```
$ curl -O http://www.wbez.org/ta/[1-10].rm
[1/10] http://www.wbez.org/ta/1.rm --> 1.rm
--curl--http http://www.wbez.org/ta/1.rm
```

注意你如何使用 `[1-10]` 来指定你想下载 `1.rm`、`2.rm`、`3.rm` 等。WBEZ 而是将文件命名为 `one.rm`、`two.rm` 和 `three.rm`，例如，你可以使用部分集：

```
$ curl -O http://www.wbez.org/ta/(one,two,three).rm
```

## 第五部分：网络

`-O` 或 `--remote-name` 选项是绝对要求的。如果你不使用它，`curl` 将其下载的内容输出到标准输出 (STDOUT)，你的终端会迅速充满无法使用的 `goodygoodbook`。`-O` 要求 `curl` 将下载的内容写入文件，并使用下载的文件名作为本地文件名。

我们仅仅触及了 `curl` 的冰角。它的手册页（man page）虽然没有 `wget` 那么长，但也充满了如果你想最大限度利用 `curl` 时需要阅读的有用信息。请将其视为必须的。

### 结论

本章中的命令是我个人最喜爱的一些，因为它们允许我完成那些原本会很枯燥、不安全或困难的任务。所有这些命令让网络成为你的数据、程序和想象力的另一个途径，这真的让 Linux 发放异彩。通过为用户提供如 `ssh`、`rsync`、`wget` 和 `curl` 这样强大的工具，Linux 以一种在许多操作系统上无法实现的方式鼓励了创新和安全。

## 第五部分：网络

此选项不仅修复了指向页面的链接，还修复了指向图片、层级样式表文件的链接。你会庆幸自己做了它的。

提到层级样式表 (CSS) 和图像，这就是你想要使用 `-p` 或 `--page-requisites` 选项的原因。为了让网页能够正确显示，网站开发者可能指定了与 HTML 使用图像、CSS 和 JavaScript 文件。`-p` 选项要求 `wget` 下载显示你正在查看的网页所需的任何文件。有了它，在你的机器上查看该页面后的结果将与你在 Web 上看到的内容完全相同；如果没有它，你可能会得到一个无法使用的文件。

`wget` 的页面非常冗长且详细，如果你想以更高级的方式使用 `wget`，你最终会去那里。如果你觉得 `wget` 听起来很有趣，就开始阅读吧。你会学到很多。

### Note: curl

乍一看，`wget` 和 `curl` 似乎相似：两者都可以非交互式地下载许多文件。然而，在许多细微区别中，它们各有一个巨大的区别：`curl` 在指定下载内容时支持序列和集合，而 `wget` 不支持；而 `wget` 支持递归，这是 `curl` 缺失的一个功能。

### Note: 其他区别

这些程序之间还有许多其他区别。`curl` 功能的完整列表可以在“curl 能做什么”(`http://curl.haxx.se/features.html`) 中查看，而 `wget` 的某些功能则列在“概述”(`www.gnu.org/software/wget/html_node/Overview.html`) 中。`curl` 网站有一张图表，通过“将 curl 功能与其他 FTP+HTTP 工具比较”(`http://curl.haxx.se/docs/comparison-table.html`) 比较 `curl` 与其他类似的程序；虽然该图表很有参考价值，但稍微偏向 `curl`。

这里有一个使用 `curl` 支持的序列能力来指定下载内容的示例。《美国生活》(This American Life) 这档优秀国家公共节目对其文件进行了存档，以便以 Real Audio 格式在你的网站上显示下载（你看到的是 Real 而不是更开放的格式，这是一个谜团）。如果你想下载 100 个 Real Audio 文件，只需使用以下命令：

```
$ curl -O http://www.wbez.org/ta/[1-10].rm
[1/10] http://www.wbez.org/ta/1.rm --> 1.rm
--curl--http http://www.wbez.org/ta/1.rm
```

注意你如何使用 `[1-10]` 来指定你想下载 `1.rm`、`2.rm`、`3.rm` 等。WBEZ 而是将文件命名为 `one.rm`、`two.rm` 和 `three.rm`，例如，你可以使用部分集：

```
$ curl -O http://www.wbez.org/ta/(one,two,three).rm
```

## 第五部分：网络

`-O` 或 `--remote-name` 选项是绝对要求的。如果你不使用它，`curl` 将其下载的内容输出到标准输出 (STDOUT)，你的终端会迅速充满无法使用的 `goodygoodbook`。`-O` 要求 `curl` 将下载的内容写入文件，并使用下载的文件名作为本地文件名。

我们仅仅触及了 `curl` 的冰角。它的手册页（man page）虽然没有 `wget` 那么长，但也充满了如果你想最大限度利用 `curl` 时需要阅读的有用信息。请将其视为必须的。

### 结论

本章中的命令是我个人最喜爱的一些，因为它们允许我完成那些原本会很枯燥、不安全或困难的任务。所有这些命令让网络成为你的数据、程序和想象力的另一个途径，这真的让 Linux 发放异彩。通过为用户提供如 `ssh`、`rsync`、`wget` 和 `curl` 这样强大的工具，Linux 以一种在许多操作系统上无法实现的方式鼓励了创新和安全。



本章中的命令是我个人最喜爱的一些，因为它们允许我完成那些原本会很枯燥、不安全或困难的任务。所有这些命令让网络成为你的数据、程序和想象力的另一个途径，这真的让 Linux 发放异彩。通过为用户提供如 `ssh`、`rsync`、`wget` 和 `curl` 这样强大的工具，Linux 以一种在许多操作系统上无法实现的方式鼓励了创新和安全。

## 第五部分：网络

此选项不仅修复了指向页面的链接，还修复了指向图片、层级样式表文件的链接。你会庆幸自己做了它的。

提到层级样式表 (CSS) 和图像，这就是你想要使用 `-p` 或 `--page-requisites` 选项的原因。为了让网页能够正确显示，网站开发者可能指定了与 HTML 使用图像、CSS 和 JavaScript 文件。`-p` 选项要求 `wget` 下载显示你正在查看的网页所需的任何文件。有了它，在你的机器上查看该页面后的结果将与你在 Web 上看到的内容完全相同；如果没有它，你可能会得到一个无法使用的文件。

`wget` 的页面非常冗长且详细，如果你想以更高级的方式使用 `wget`，你最终会去那里。如果你觉得 `wget` 听起来很有趣，就开始阅读吧。你会学到很多。

### curl

乍一看，`wget` 和 `curl` 似乎相似：两者都可以非交互式地下载许多文件。然而，在许多细微区别中，它们各有一个巨大的区别：`curl` 在指定下载内容时支持序列和集合，而 `wget` 不支持；而 `wget` 支持递归，这是 `curl` 缺失的一个功能。

这些程序之间还有许多其他区别。`curl` 功能的完整列表可以在“curl 能做什么”(`<http://curl.haxx.se/features.html>`) 中查看，而 `wget` 的某些功能则列在“概述”(`<www.gnu.org/software/wget/html_node/Overview.html>`) 中。`curl` 网站有一张图表，通过“将 curl 功能与其他 FTP+HTTP 工具比较”(`<http://curl.haxx.se/docs/comparison-table.html>`) 比较 `curl` 与其他类似的程序；虽然该图表很有参考价值，但稍微偏向 `curl`。

这里有一个使用 `curl` 支持的序列能力来指定下载内容的示例。《美国生活》(This American Life) 这档优秀国家公共节目对其文件进行了存档，以便以 Real Audio 格式在你的网站上显示下载（你看到的是 Real 而不是更开放的格式，这是一个谜团）。如果你想下载 100 个 Real Audio 文件，只需使用以下命令：

```
$ curl -O http://www.wbez.org/ta/[1-10].rm
[1/10] http://www.wbez.org/ta/1.rm --> 1.rm
--curl--http http://www.wbez.org/ta/1.rm
```

注意你如何使用 `[1-10]` 来指定你想下载 `1.rm`、`2.rm`、`3.rm` 等。WBEZ 而是将文件命名为 `one.rm`、`two.rm` 和 `three.rm`，例如，你可以使用部分集：

```
$ curl -O http://www.wbez.org/ta/(one,two,three).rm
```

`-O` 或 (`--remote-name`) 选项是绝对要求的。如果你不使用它，`curl` 将其下载的内容输出到标准输出 (STDOUT)，你的终端会迅速充满无法使用的 `goodygoodbook`。`-O` 要求 `curl` 将下载的内容写入文件，并使用下载的文件名作为本地文件名。

我们仅仅触及了 `curl` 的冰角。它的手册页（man page）虽然没有 `wget` 那么长，但也充满了如果你想最大限度利用 `curl` 时需要阅读的有用信息。请将其视为必须的。

### 结论

本章中的命令是我个人最喜爱的一些，因为它们允许我完成那些原本会很枯燥、不安全或困难的任务。所有这些命令让网络成为你的数据、程序和想象力的另一个途径，这真的让 Linux 发放异彩。通过为用户提供如 `ssh`、`rsync`、`wget` 和 `curl` 这样强大的工具，Linux 以一种在许多操作系统上无法实现的方式鼓励了创新和安全。



### Note: curl

乍一看，`wget` 和 `curl` 似乎相似：两者都可以非交互式地下载许多文件。然而，在许多细微区别中，它们各有一个巨大的区别：`curl` 在指定下载内容时支持序列和集合，而 `wget` 不支持；而 `wget` 支持递归，这是 `curl` 缺失的一个功能。

### Note

这些程序之间还有许多其他区别。`curl` 功能的完整列表可以在“curl 能做什么”(http://curl.haxx.se/features.html) 中查看，而 `wget` 的某些功能则列在“概述”(www.gnu.org/software/wget/html_node/Overview.html) 中。`curl` 网站有一张图表，通过“将 curl 功能与其他 FTP+HTTP 工具比较”(http://curl.haxx.se/docs/comparison-table.html) 比较 `curl` 与其他类似的程序；虽然该图表很有参考价值，但稍微偏向 `curl`。

这里有一个使用 `curl` 支持的序列能力来指定下载内容的示例。《美国生活》(This American Life) 这档优秀国家公共节目对其文件进行了存档，以便以 Real Audio 格式在你的网站上显示下载（你看到的是 Real 而不是更开放的格式，这是一个谜团）。如果你想下载 100 个 Real Audio 文件，只需使用以下命令：

```
$ curl -O http://www.wbez.org/ta/[1-10].rm
[1/10] http://www.wbez.org/ta/1.rm --> 1.rm
--curl--http http://www.wbez.org/ta/1.rm
```

注意你如何使用 `[1-10]` 来指定你想下载 `1.rm`、`2.rm`、`3.rm` 等。WBEZ 而是将文件命名为 `one.rm`、`two.rm` 和 `three.rm`，例如，你可以使用部分集：

```
$ curl -O http://www.wbez.org/ta/(one,two,three).rm
```

## 第五部分：网络

`-O` 或 `--remote-name` 选项是绝对要求的。如果你不使用它，`curl` 将其下载的内容输出到标准输出 (STDOUT)，你的终端会迅速充满无法使用的 `goodygoodbook`。`-O` 要求 `curl` 将下载的内容写入文件，并使用下载的文件名作为本地文件名。

我们仅仅触及了 `curl` 的冰角。它的手册页（man page）虽然没有 `wget` 那么长，但也充满了如果你想最大限度利用 `curl` 时需要阅读的有用信息。请将其视为必须的。

### 结论

本章中的命令是我个人最喜爱的一些，因为它们允许我完成那些原本会很枯燥、不安全或困难的任务。所有这些命令让网络成为你的数据、程序和想象力的另一个途径，这真的让 Linux 发放异彩。通过为用户提供如 `ssh`、`rsync`、`wget` 和 `curl` 这样强大的工具，Linux 以一种在许多操作系统上无法实现的方式鼓励了创新和安全。

## 第五部分：网络

此选项不仅修复了指向页面的链接，还修复了指向图片、层级样式表文件的链接。你会庆幸自己做了它的。

提到层级样式表 (CSS) 和图像，这就是你想要使用 `-p` 或 `--page-requisites` 选项的原因。为了让网页能够正确显示，网站开发者可能指定了与 HTML 使用图像、CSS 和 JavaScript 文件。`-p` 选项要求 `wget` 下载显示你正在查看的网页所需的任何文件。有了它，在你的机器上查看该页面后的结果将与你在 Web 上看到的内容完全相同；如果没有它，你可能会得到一个无法使用的文件。

`wget` 的页面非常冗长且详细，如果你想以更高级的方式使用 `wget`，你最终会去那里。如果你觉得 `wget` 听起来很有趣，就开始阅读吧。你会学到很多。



### 序列与集合

这里有一个使用 `curl` 支持的序列能力来指定下载内容的示例。《美国生活》(*This American Life*) 这档优秀国家公共节目对其文件进行了存档，以便以 Real Audio 格式在你的网站上显示下载（你看到的是 Real 而不是更开放的格式，这是一个谜团）。如果你想下载 100 个 Real Audio 文件，只需使用以下命令：

```bash
$ curl -O http://www.wbez.org/ta/[1-10].rm
[1/10] http://www.wbez.org/ta/1.rm --> 1.rm
--curl--http http://www.wbez.org/ta/1.rm
```

注意你如何使用 `[1-10]` 来指定你想下载 `1.rm`、`2.rm`、`3.rm` 等。WBEZ 而是将文件命名为 `one.rm`、`two.rm` 和 `three.rm`，例如，你可以使用部分集：

```bash
$ curl -O http://www.wbez.org/ta/(one,two,three).rm
```

### 远程文件名选项

`-O` 或 `--remote-name` 选项是绝对要求的。如果你不使用它，`curl` 将其下载的内容输出到标准输出 (STDOUT)，你的终端会迅速充满无法使用的 `goodygoodbook`。`-O` 要求 `curl` 将下载的内容写入文件，并使用下载的文件名作为本地文件名。

我们仅仅触及了 `curl` 的冰山一角。它的手册页（man page）虽然没有 `wget` 那么长，但也充满了如果你想最大限度利用 `curl` 时需要阅读的有用信息。请将其视为必须的。

### 结论

本章中的命令是我个人最喜爱的一些，因为它们允许我完成那些原本会很枯燥、不安全或困难的任务。所有这些命令让网络成为你的数据、程序和想象力的另一个途径，这真的让 Linux 焕发异彩。通过为用户提供如 `ssh`、`rsync`、`wget` 和 `curl` 这样强大的工具，Linux 以一种在许多操作系统上无法实现的方式鼓励了创新和安全。

### 页面资源选项

此选项不仅修复了指向页面的链接，还修复了指向图片、层级样式表文件的链接。你会庆幸自己做了它的。

提到层级样式表 (CSS) 和图像，这就是你想要使用 `-p` 或 `--page-requisites` 选项的原因。为了让网页能够正确显示，网站开发者可能指定了与 HTML 使用图像、CSS 和 JavaScript 文件。`-p` 选项要求 `wget` 下载显示你正在查看的网页所需的任何文件。有了它，在你的机器上查看该页面后的结果将与你在 Web 上看到的内容完全相同；如果没有它，你可能会得到一个无法使用的文件。

`wget` 的手册页非常冗长且详细，如果你想以更高级的方式使用 `wget`，你最终会去那里。如果你觉得 `wget` 听起来很有趣，就开始阅读吧。你会学到很多。

### 提示：curl 与 wget 的区别

乍一看，`wget` 和 `curl` 似乎相似：两者都可以非交互式地下载许多文件。然而，在许多细微区别中，它们各有一个巨大的区别：`curl` 在指定下载内容时支持序列和集合，而 `wget` 不支持；而 `wget` 支持递归，这是 `curl` 缺失的一个功能。

### 提示：更多区别

这些程序之间还有许多其他区别。`curl` 功能的完整列表可以在“curl 能做什么”([http://curl.haxx.se/features.html](http://curl.haxx.se/features.html)) 中查看，而 `wget` 的某些功能则列在“概述”([www.gnu.org/software/wget/html_node/Overview.html](www.gnu.org/software/wget/html_node/Overview.html)) 中。`curl` 网站有一张图表，通过“将 curl 功能与其他 FTP+HTTP 工具比较”([http://curl.haxx.se/docs/comparison-table.html](http://curl.haxx.se/docs/comparison-table.html)) 比较 `curl` 与其他类似的程序；虽然该图表很有参考价值，但稍微偏向 `curl`。



`-O`或(`--remote-name`)选项是绝对要求的。如果你不使用它，`curl`将其下载的内容输出到标准输出(`STDOUT`)，你的终端会迅速充满无法使用的`goodygoodbook`。`-O`要求`curl`将下载的内容写入文件，并使用下载的文件名作为本地文件名。

我们仅仅触及了`curl`的冰角。它的手册页(man page)虽然没有`wget`那么长，但也充满了如果你想最大限度利用`curl`时需要阅读的有用信息。请将其视为必须的。

### 结论

本章中的命令是我个人最喜爱的一些，因为它们允许我完成那些原本会很枯燥、不安全或困难的任务。所有这些命令让网络成为你的数据、程序和想象力的另一个途径，这真的让`Linux`发放异彩。通过为用户提供如`ssh`、`rsync`、`wget`和`curl`这样强大的工具，`Linux`以一种在许多操作系统上无法实现的方式鼓励了创新和安全。

## 第五部分：网络

此选项不仅修复了指向页面的链接，还修复了指向图片、层级样式表文件的链接。你会庆幸自己做了它的。

提到层级样式表(`CSS`)和图像，这就是你想要使用`-p`或`--page-requisites`选项的原因。为了让网页能够正确显示，网站开发者可能指定了与`HTML`使用图像、`CSS`和`JavaScript`文件。`-p`选项要求`wget`下载显示你正在查看的网页所需的任何文件。有了它，在你的机器上查看该页面后的结果将与你在`Web`上看到的内容完全相同；如果没有它，你可能会得到一个无法使用的文件。

`wget`的页面非常冗长且详细，如果你想以更高级的方式使用`wget`，你最终会去那里。如果你觉得`wget`听起来很有趣，就开始阅读吧。你会学到很多。

### Note

`curl`

乍一看，`wget`和`curl`似乎相似：两者都可以非交互式地下载许多文件。然而，在许多细微区别中，它们各有一个巨大的区别：`curl`在指定下载内容时支持序列和集合，而`wget`不支持；而`wget`支持递归，这是`curl`缺失的一个功能。

### Note

这些程序之间还有许多其他区别。`curl`功能的完整列表可以在“curl 能做什么”(`http://curl.haxx.se/features.html`)中查看，而`wget`的某些功能则列在“概述”(`www.gnu.org/software/wget/html_node/Overview.html`)中。`curl`网站有一张图表，通过“将 curl 功能与其他 FTP+HTTP 工具比较”(`http://curl.haxx.se/docs/comparison-table.html`)比较`curl`与其他类似的程序；虽然该图表很有参考价值，但稍微偏向`curl`。

这里有一个使用`curl`支持的序列能力来指定下载内容的示例。《美国生活》(`This American Life`) 这档优秀国家公共节目对其文件进行了存档，以便以`Real Audio`格式在你的网站上显示下载（你看到的是`Real`而不是更开放的格式，这是一个谜团）。如果你想下载 100 个`Real Audio`文件，只需使用以下命令：

```
$ curl -O http://www.wbez.org/ta/[1-10].rm
[1/10] http://www.wbez.org/ta/1.rm --> 1.rm
--curl--http http://www.wbez.org/ta/1.rm
```

注意你如何使用`[1-10]`来指定你想下载`1.rm`、`2.rm`、`3.rm`等。WBEZ 而是将文件命名为`one.rm`、`two.rm`和`three.rm`，例如，你可以使用部分集：

```
$ curl -O http://www.wbez.org/ta/(one,two,three).rm
```



此选项不仅修复了指向页面的链接，还修复了指向图片、层级样式表文件的链接。你会庆幸自己做了它的。

提到层级样式表 (CSS) 和图像，这就是你想要使用 `-p` 或 `--page-requisites` 选项的原因。为了让网页能够正确显示，网站开发者可能指定了与 HTML 使用图像、CSS 和 JavaScript 文件。`-p` 选项要求 `wget` 下载显示你正在查看的网页所需的任何文件。有了它，在你的机器上查看该页面后的结果将与你在 Web 上看到的内容完全相同；如果没有它，你可能会得到一个无法使用的文件。

`wget` 的页面非常冗长且详细，如果你想以更高级的方式使用 `wget`，你最终会去那里。如果你觉得 `wget` 听起来很有趣，就开始阅读吧。你会学到很多。

### Note

`curl`

乍一看，`wget` 和 `curl` 似乎相似：两者都可以非交互式地下载许多文件。然而，在许多细微区别中，它们各有一个巨大的区别：`curl` 在指定下载内容时支持序列和集合，而 `wget` 不支持；而 `wget` 支持递归，这是 `curl` 缺失的一个功能。

### Note

这些程序之间还有许多其他区别。`curl` 功能的完整列表可以在“curl 能做什么”(`http://curl.haxx.se/features.html`) 中查看，而 `wget` 的某些功能则列在“概述”(`www.gnu.org/software/wget/html_node/Overview.html`) 中。`curl` 网站有一张图表，通过“将 curl 功能与其他 FTP+HTTP 工具比较”(`http://curl.haxx.se/docs/comparison-table.html`) 比较 `curl` 与其他类似的程序；虽然该图表很有参考价值，但稍微偏向 `curl`。

这里有一个使用 `curl` 支持的序列能力来指定下载内容的示例。《美国生活首页This American Life) 这档优秀国家公共节目对其文件进行了存档，以便以 Real Audio 格式在你的网站上显示下载（你看到的是 Real 而不是更开放的格式，这是一个谜团）。如果你想下载 100 个 Real Audio 文件，只需使用以下命令：

```
$ curl -O http://www.wbez.org/ta/[1-10].rm
[1/10] http://www.wbez.org/ta/1.rm --> 1.rm
--curl--http http://www.wbez.org/ta/1.rm
```

注意你如何使用 `[1-10]` 来指定你想下载 `1.rm`、`2.rm`、`3.rm` 等。WBEZ 而是将文件命名为 `one.rm`、`two.rm` 和 `three.rm`，例如，你可以使用部分集：

```
$ curl -O http://www.wbez.org/ta/(one,two,three).rm
```

## 第五部分：网络

`-O` 或 (`--remote-name`) 选项是绝对要求的。如果你不使用它，`curl` 将其下载的内容输出到标准输出 (STDOUT)，你的终端会迅速充满无法使用的 `goodygoodbook`。`-O` 要求 `curl` 将下载的内容写入文件，并使用下载的文件名作为本地文件名。

我们仅仅触及了 `curl` 的冰角。它的手册页（man page）虽然没有 `wget` 那么长，但也充满了如果你想最大限度利用 `curl` 时需要阅读的有用信息。请将其视为必须的。

### 结论

本章中的命令是我个人最喜爱的一些，因为它们允许我完成那些原本会很枯燥、不安全或困难的任务。所有这些命令让网络成为你的数据、程序和想象力的另一个途径，这真的让 Linux 发放异彩。通过为用户提供如 `ssh`、`rsync`、`wget` 和 `curl` 这样强大的工具，Linux 以一种在许多操作系统上无法实现的方式鼓励了创新和安全。



## 第五部分：网络

### Note

#### curl

乍一看，`wget` 和 `curl` 似乎相似：两者都可以非交互式地下载许多文件。然而，在许多细微区别中，它们各有一个巨大的区别：`curl` 在指定下载内容时支持序列和集合，而 `wget` 不支持；而 `wget` 支持递归，这是 `curl` 缺失的一个功能。

### Note

这些程序之间还有许多其他区别。`curl` 功能的完整列表可以在“curl 能做什么”（`http://curl.haxx.se/features.html`）中查看，而 `wget` 的某些功能则列在“概述”（`www.gnu.org/software/wget/html_node/Overview.html`）中。`curl` 网站有一张图表，通过“将 `curl` 功能与其他 `FTP+HTTP` 工具比较”（`http://curl.haxx.se/docs/comparison-table.html`）比较 `curl` 与其他类似的程序；虽然该图表很有参考价值，但稍微偏向 `curl`。

这里有一个使用 `curl` 支持的序列能力来指定下载内容的示例。《美国生活（This American Life）》这档优秀国家公共节目对其文件进行了存档，以便以 `Real Audio` 格式在你的网站上显示下载（你看到的是 `Real` 而不是更开放的格式，这是一个谜团）。如果你想下载 `100` 个 `Real Audio` 文件，只需使用以下命令：

```
$ curl -O http://www.wbez.org/ta/[1-10].rm
[1/10] http://www.wbez.org/ta/1.rm --> 1.rm
--curl--http http://www.wbez.org/ta/1.rm
```

注意你如何使用 `[1-10]` 来指定你想下载 `1.rm`、`2.rm`、`3.rm` 等。`WBEZ` 而是将文件命名为 `one.rm`、`two.rm` 和 `three.rm`，例如，你可以使用部分集：

```
$ curl -O http://www.wbez.org/ta/(one,two,three).rm
```

`-O` 或 `--remote-name` 选项是绝对要求的。如果你不使用它，`curl` 将其下载的内容输出到标准输出（`STDOUT`），你的终端会迅速充满无法使用的 `goodygoodbook`。`-O` 要求 `curl` 将下载的内容写入文件，并使用下载的文件名作为本地文件名。

我们仅仅触及了 `curl` 的冰角。它的手册页（`man` page）虽然没有 `wget` 那么长，但也充满了如果你想最大限度利用 `curl` 时需要阅读的有用信息。请将其视为必须的。

### 结论

本章中的命令是我个人最喜爱的一些，因为它们允许我完成那些原本会很枯燥、不安全或困难的任务。所有这些命令让网络成为你的数据、程序和想象力的另一个途径，这真的让 `Linux` 发放异彩。通过为用户提供如 `ssh`、`rsync`、`wget` 和 `curl` 这样强大的工具，`Linux` 以一种在许多操作系统上无法实现的方式鼓励了创新和安全。

此选项不仅修复了指向页面的链接，还修复了指向图片、层级样式表文件的链接。你会庆幸自己做了它的。

提到层级样式表（`CSS`）和图像，这就是你想要使用 `-p` 或 `--page-requisites` 选项的原因。为了让网页能够正确显示，网站开发者可能指定了与 `HTML` 使用图像、`CSS` 和 `JavaScript` 文件。`-p` 选项要求 `wget` 下载显示你正在查看的网页所需的任何文件。有了它，在你的机器上查看该页面后的结果将与你在 `Web` 上看到的内容完全相同；如果没有它，你可能会得到一个无法使用的文件。

`wget` 的页面非常冗长且详细，如果你想以更高级的方式使用 `wget`，你最终会去那里。如果你觉得 `wget` 听起来很有趣，就开始阅读吧。你会学到很多。



`$ curl -O http://www.wbez.org/ta/[1-10].rm`
[1/10] `http://www.wbez.org/ta/1.rm` --> `1.rm`
`--curl--http` `http://www.wbez.org/ta/1.rm`

注意你如何使用`[1-10]`来指定你想下载`1.rm`、`2.rm`、`3.rm`等。WBEZ 而是将文件命名为`one.rm`、`two.rm`和`three.rm`，例如，你可以使用部分集：

`$ curl -O http://www.wbez.org/ta/(one,two,three).rm`

## 第五部分：网络

`-O`或`--remote-name`选项是绝对要求的。如果你不使用它，`curl`将其下载的内容输出到标准输出 (STDOUT)，你的终端会迅速充满无法使用的`goodygoodbook`。`-O`要求`curl`将下载的内容写入文件，并使用下载的文件名作为本地文件名。

我们仅仅触及了`curl`的冰角。它的手册页（man page）虽然没有`wget`那么长，但也充满了如果你想最大限度利用`curl`时需要阅读的有用信息。请将其视为必须的。

### 结论

本章中的命令是我个人最喜爱的一些，因为它们允许我完成那些原本会很枯燥、不安全或困难的任务。所有这些命令让网络成为你的数据、程序和想象力的另一个途径，这真的让 Linux 发放异彩。通过为用户提供如`ssh`、`rsync`、`wget`和`curl`这样强大的工具，Linux 以一种在许多操作系统上无法实现的方式鼓励了创新和安全。

## 第五部分：网络

此选项不仅修复了指向页面的链接，还修复了指向图片、层级样式表文件的链接。你会庆幸自己做了它的。

提到层级样式表 (CSS) 和图像，这就是你想要使用`-p`或`--page-requisites`选项的原因。为了让网页能够正确显示，网站开发者可能指定了与 HTML 使用图像、CSS 和 JavaScript 文件。`-p`选项要求`wget`下载显示你正在查看的网页所需的任何文件。有了它，在你的机器上查看该页面后的结果将与你在 Web 上看到的内容完全相同；如果没有它，你可能会得到一个无法使用的文件。

`wget`的页面非常冗长且详细，如果你想以更高级的方式使用`wget`，你最终会去那里。如果你觉得`wget`听起来很有趣，就开始阅读吧。你会学到很多。

### Note

curl

乍一看，`wget`和`curl`似乎相似：两者都可以非交互式地下载许多文件。然而，在许多细微区别中，它们各有一个巨大的区别：`curl`在指定下载内容时支持序列和集合，而`wget`不支持；而`wget`支持递归，这是`curl`缺失的一个功能。

### Note

这些程序之间还有许多其他区别。`curl`功能的完整列表可以在“curl 能做什么”(`http://curl.haxx.se/features.html`)中查看，而`wget`的某些功能则列在“概述”(`www.gnu.org/software/wget/html_node/Overview.html`)中。`curl`网站有一张图表，通过“将 curl 功能与其他 FTP+HTTP 工具比较”(`http://curl.haxx.se/docs/comparison-table.html`)比较`curl`与其他类似的程序；虽然该图表很有参考价值，但稍微偏向`curl`。

这里有一个使用`curl`支持的序列能力来指定下载内容的示例。《美国生活 This American Life) 这档优秀国家公共节目对其文件进行了存档，以便以 Real Audio 格式在你的网站上显示下载（你看到的是 Real 而不是更开放的格式，这是一个谜团）。如果你想下载 100 个 Real Audio 文件，只需使用以下命令：

`$ curl -O http://www.wbez.org/ta/[1-10].rm`
[1/10] `http://www.wbez.org/ta/1.rm` --> `1.rm`
`--curl--http` `http://www.wbez.org/ta/1.rm`

注意你如何使用`[1-10]`来指定你想下载`1.rm`、`2.rm`、`3.rm`等。WBEZ 而是将文件命名为`one.rm`、`two.rm`和`three.rm`，例如，你可以使用部分集：

`$ curl -O http://www.wbez.org/ta/(one,two,three).rm`

## 第五部分：网络

此选项不仅修复了指向页面的链接，还修复了指向图片、层级样式表文件的链接。你会庆幸自己做了它的。

# 第五部分：网络

要获取更多关于主节点（Master）的信息，请使用带有`-S`（或`--status`）选项的`nmblookup`，它会返回 SMB 主节点使用的主机。

```
$ nmblookup -SA 192.168.1.151
querying 192.168.1.151 on 192.168.1.255
name_query failed to find name 192.168.1.151
```

这样做不起作用，因为`-S`期望的是 NetBIOS 名称而不是 IP 地址。遗憾的是，你不知道机器的 NetBIOS 名称，只知道它的 IP 地址。这并不是问题。你只需添加`-A`（或`--lookup-by-ip`）选项，这会告诉`nmblookup`你提供的是 IP 地址而不是 NetBIOS 名称。

```
$ nmblookup -SA 192.168.1.151
Looking up status of 192.168.1.151
JANSMAC <00> B <ACTIVE>
JANSMAC <03> B <ACTIVE>
JANSMAC <20> B <ACTIVE>
..MSBROWSE_ <01> <GROUP> B <ACTIVE>
MILTON <00> <GROUP> B <ACTIVE>
MILTON <1d> B <ACTIVE>
MILTON <1e> <GROUP> B <ACTIVE>
```

`MAC地址 = 00-00-00-00-00-00`

现在你知道`192.168.1.151`标识自己为`JANSMAC`（它一定是一台 Mac OS 机器），并且是`MILTON`工作组的主节点。那么另一个 IP 地址呢？

```
$ nmblookup -SA 192.168.1.104
Looking up status of 192.168.1.104
ELIOT <00> B <ACTIVE>
ELIOT <03> B <ACTIVE>
ELIOT <20> B <ACTIVE>
..MSBROWSE_ <01> <GROUP> B <ACTIVE>
TURING <00> <GROUP> B <ACTIVE>
TURING <1d> B <ACTIVE>
TURING <1e> <GROUP> B <ACTIVE>
```

`MAC地址 = 00-00-00-00-00-00`

在`192.168.1.104`找到的计算机 NetBIOS 名称为`ELIOT`，并且是`TURING`工作组的主节点。你实际上不需要担心这个，因为这两台机器是各自独立工作组的主节点。自标识为`MILTON`的机器会向`JANSMAC`获取信息，而认为自己是`TURING`一部分的机器则会为了相同的目的使用`ELIOT`。

注意

关于这些示例中输出内容含义的更多信息，请参阅微软知识库中的：`http://support.microsoft.com/kb/q163409/`。

# 查询并映射 NetBIOS 名称与 IP 地址

`nmblookup -T`

你可以使用`nmblookup`作为快速查找任何通过 Samba 共享文件和打印机的机器的方法。在命令后附加`-T`选项，后面跟上`"*"`（是的，你必须包含引号），以告诉系统你不是在使用`*`作为代表当前工作目录下的文件的通配符。

```
$ nmblookup -T * *
querying * on 192.168.1 * <00
192.168.1.151 *<00
192.168.1.104 *<00
192.168.1.110 *<00
```

此局域网上有三台带有 Samba 共享的机器。要找出其中哪些是主浏览器（Master Browser），请上一节；要生成每台计算机提供的共享列表，请继续下一节。

# 列出机器的 Samba 共享

`smclient`

通过上一节概述的命令，你可以知道某台机器上有 Samba 共享，但并不知道这些共享是什么。`smclient`命令是一个多功能工具，可以用于连接并与其交互；在更简单的层，它还可以列出计算机上可用的共享。只需使用`-L`（或`--list`）选项，后跟 NetBIOS 名称或 IP 地址。当提示输入密码时，直接按回车即可。



## 第五部分：网络

可以使用`smclient`访问Samba共享，这很酷，但如果你想使用图形界面，或者想在共享上进行大量工作，它就会很痛苦。在这种情况下，你应该使用`smbmount`，它将Samba共享挂载到你的本地文件系统中，就像它是硬盘的一部分一样。一旦挂载，你就可以使用自己的文件管理器轻松地访问共享上的文件，甚至可以打开如文字处理器之类的程序并直接使用fuss打开文件。

要在你的文件系统上挂载Samba共享，你必须创建一个挂载点以获得访问权限。如果你要挂载来自ELIOT的文档，可能会创建一个这样的目录：

```
$ mkdir /home/scott/eliot_documents
```

现在你运行`smbmount`命令，并带有一系列选项。

```
$ smbmount //eliot/documents/home/scott/eliot_documents -o credentials=/home/scott/bin/credentials_eliot,fmask=644,mask=755,uid=1001,gid=1001,workgroup=TURING
smbmount must be installed sudo root for direct user mounts (1000,1000)
smbmount failed: 1
```

在查看之前，我们先聊聊`smbmount failed`。第二行告诉你：`smbmount`命令只能由root运行。如果你的非root用户能够挂载Samba共享，这就会成为一个问题。解决方法是将`smbmount`设置为suid root（你在第 7 章的“设置并清除 suid”中学习过 suid）。

**注意**

是的，你正在赋予他人像root一样使用`smbmount`的能力，但这并不真的是一个大问题。这显然比给他们root密码，或者要求他们他们每次想挂载Samba共享时都需要你的参与要好得多。

以下是将`smbmount`设置为suid root的方法。

**注意**

为了节省空间，去除了你通常通过`ls -l`看到的某些细节。

```
$ ls /usr/bin/smbmount
-rwxr-xr-x 1 root /usr/bin/smbmount
# chmod u+s /usr/bin/smbmount
# ls -l /usr/bin/smbmount
-rwxr-xr-x 1 root /usr/bin/smbmount
```

现在让我们再次尝试`smbmount`。

```
$ smbmount //eliot/documents/home/scott/eliot_documents -o credentials=/home/scott/credentials_eliot,fmask=644,mask=755,uid=1001,gid=1001,workgroup=TURING
```

```
$ ls -F /home/scott/eliot_documents
presentations/ to_print/
```

让我们过一遍你使用的命令。在`smbmount`之后，`//credentials`指定了你正在连接的Samba服务器和共享。然后是你的挂载点路径`/home/scott/eliot_documents/`，`-o`表示后面是选项。

与其使用`credentials=/home/scott/credentials_eliot`，你可以以下任何一种：

- `username=scott,password=123456`
- `username=scott%123456`
- `username=scott`

第一个和第二个选择完全不安全，因为密码会出现在`.bash_history`中。不要那样做！最后一个选择会提示你输入密码，这是安全的，因为密码不会出现在`.bash_history`中。但你正尝试自动化挂载Samba共享的过程，所以最后一个选择也不行。

这让你留下了`credentials=/home/scott/credentials_eliot`。这告诉`smbmount`用户和密码存储在一个文件中，格式如下：

```
username = scott
password = 123456
```

这与之前在“使用类似 FTP 的客户端访问 Samba 资源”中讨论的凭据一样，作为一个例子，在创建文件后使用`chmod`来严格限制谁可以查看它。如果你不在乎日志过程，大尽管使用`username=scott`并让它提示输入密码，这完全足够了。

`fmask`和`dmask`选项分别控制挂载到Samba共享的任何新文件和目录的默认权限。`644`会为文件生成`rw-r--r--`权限，而`755`则会让目录变为`rwx-xr-x`。

**注意**

不记得我们在说什么了？请回顾一下第 7 章中的“理解权限的基础”。

记住，所有用户名和组名都是数字的引用，你可以在`/etc/passwd`和`/etc/group`中看到它们。你当前机器上的用户ID可能是1000，但在Samba服务器上，可能是完全不同的用户，你的组ID也是如此。`uid=1001`和`gid=1001`标识你在Samba服务器上的身份。换句话说，你需要在Samba服务器的`/etc/passwd`和`/etc/group`中查找这些数字，而不是在本地机器上。如果你创建了你并不真正拥有的文件目录，你就无法使用它们。

最后，`workgroup=TURING`指定了工作组，这显而易见。

共享挂载后，你可以打开文件管理器并开始`eliot_documents`的内容，打开OpenOffice.org并直接打开`eliot_documents/presentations/`内部的文件。如果你将以下行内容放入你机器的`/etc/fstab`文件中，该共享将自动挂载：

```
//eliot_documents /home/scott/eliot_documents -o credentials=/home/scott/credentials_eliot,fmask=644,dmask=755,uid=1001,gid=1001,workgroup=TURING
```

**注意**

小心修改`/etc/fstab`文件，因为错误会导致系统无法启动，你可以谨慎解决这个问题。关于fstab文件，请参`man fstab`。如果你决定不再访问Samba共享，可以使用`smbmount`卸载（注意`smbmount`必须安装为suid）。真沮丧！你只需要将`smbmount`设置为suid root。



```
$ ls -l /usr/bin/smbmount
-rwxr-xr-x 1 root /usr/bin/smbmount
sudo chmod u+s /usr/bin/smbmount
$ ls -l /usr/bin/smbmount
-rwxr-xr-x 1 root /usr/bin/smbmount
```

现在你已经挂载了 `eliot_documents`，且用户也可以卸载它，因为 `root` 可以做任何事情。

```
$ smbmount //eliot_documents
```

就是这样。如果你想通过 `ls -l eliot_documents` 验证 `smbmount` 是否成功，那里不应该有任何东西。你已经断开了 `Samba` 共享。

### 总结

尽管 `Linux` 用户希望假装微软不存在，但你意识到你生活在一个 `Windows` 世界里。`Samba` 让这种共存变得容易得多，因为它允许 `Linux` 用户访问 `Windows` 机器上的资源，并让其他操作系统的用户可以使用 `Linux` 机器上的资源。微软可能不喜欢它，但 `Samba` 是一项成熟、稳定、强大的技术，得益于它的开源特性，它帮助将整个计算世界联系得更加紧。`Samba` 帮助你减少家庭和企业对 `Windows` 服务器的需求，正如某位名士所说，这是一件好事。

# 第五部分：网络

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

+ 大小写敏感，文件名

- `cat` 命令

- `cd` 命令

- `chgrp` 命令

- `chmod` 命令

- `-R` 选项

- 字母表示法

- 数字表示法

- `sgid`, 设置与清除

- 粘位 (`sticky bit`)，设置与清除

- `suid`, 设置与清除

- `chown`

- 冒号

- 彩色编码输出，`ls` 命令

- 列式输出，`ls` 命令

- 逗号分隔列表，`ls` 命令

- 命令文档 [另参 `info` 命令，`man`]

- 命令默认值，识别 [另参 默认打印机，`manpages`]

- 路径，源文件和 `manpages`，查找搜索

- 语法概要

- 命令

- 用于 ... 的 `-R` 选项

- 将输出追加到文件

- 顶部 (`celing`)

- 命令别名 [另参 `Alias`]

- 命令叠加

- 命令替换

- 文件，使用 `for` 命令输入

- 输出重定向 2nd

- 输出，使用 `grep` 搜索

- 重复命令

- 通用 `Unix` 打印系统 [另参 默认打印机，`CUPS`，取消打印作业]

- `compress` 命令

- 压缩文件，损坏测试 2nd

- 合并

- `cp` 命令

- 使用 ... 创建备份

- 目录，复制

- 交互式选项

- 详细选项

- 通配符，使用

- `Ctrl+c` 命令

- `CUPS` (通用 `Unix` 打印系统) [另参 文件，打印]

第五部分：网络

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- `-` 折线 (`-`)

- `DEB` 包

- 默认打印机

- `CUPS`

  - 取消打印作业

    - 确定

    - 打印到

  - 任务 ID 号

- `Linux Journal` 概述

  - 使用 `lpstat` 收集系统信息

    - `manpages`

  - 打印作业

    - 取消所有

    - 列出相应的副本

    - 多个副本，打印

  - 任何打印机

    - 到任何打印机，取消

    - 到默认打印机，取消

  - 打印机连接

- 打印机状态，确定

- 删除目录

- 删除文件

  - 意外删除，防止

  - 详细选项

  - 文件名中带有特殊字符

  - 使用通配符

- `df` 命令

- `dhclient` 命令

- `DHCP` (动态主机配置协议)

- 目录

  - 内容列出 [另参 `ls` 命令]

  - 复制

  - 创建新的

  - 包含子目录的创建

  - 确定当前目录

  - 带内容的删除

  - 磁盘空间使用，仅总计

第五部分：网络

+ `-` 空，移除

- 文件空间使用，监控

- 移动和重命名

- 所有权 [另参 文件所有权]

- 权限 [另参 权限]

- 目录节点，`info` 命令

- 磁盘使用，监控

- `DNS` (域名系统)

- `dog` 命令

- 域名

- 双与与符号 (`&&`)

- 双感叹号 (`!`)

- 双或 (`||`)

- 正则表达式中的双引号

- 双右角

- `dpkg` 命令

- `du` 命令

- 动态主机配置协议 (`DHCP`)

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- `- echo` 命令

- 加密密钥

- 环境变量

- `ESSID` (扩展服务集标识符)

- `eth0`

- 以太网卡 2nd

- 可执行文件，查找

- `Expert Info`，`info` 命令

- 扩展服务集标识符 (`ESSID`)

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- `-` 文件

- 归档 [另参 归档]

- 使用 `for` 命令输入

- 压缩

- 复制

- 避免覆盖

第五部分：网络

+ `-` 备份

- 使用 `cat` 命令和输出重定向

- 使用通配符

- 主机之间复制

- 删除

  - 意外删除，防止

  - 特殊字符，处理

  - 使用通配符

- 创建空文件

- 文件属性

- 文件描述符

- 文件大小，列出

- 文件类型，显示

- 文件名

- `find` [另参 `find` 命令；`locate` 命令]

- 查看隐藏文件

- 列出 [另参 `ls` 命令]

- 移动

- 列出打开的文件

- 所有权 [另参 文件所有权]

- 权限和类型字符

- 权限 [另参 权限]

- 打印

- 重命名

- 在其中搜索 [另参 `grep` 命令]

- 安全网络传输

- 主机之间的安全传输和备份

- 修改时间

- 列出用户

- 查看

- 起始字节

- 起始行

- 使用 `cat` 命令

- 最后十行

- 一次一屏

- 重复查看，追加更新

+ `- find` 命令

  - `-a` (`AND`) 选项

  - `-exec` 选项

  - `-f` 选项

  - `-n` (`NOT`) 选项

  - `-o` (`OR`) 选项

  - 文件类型

  - 名称

  - 所有权

  - 大小

+ 标志 (`Flags`)

- 正斜杠 (`/`)

- `free` 命令

第五部分：网络

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- `-` 网关 (`Gateways`)

- 掩码 (`Genmasks`)

- 组 ID (`GID`)

- `grep` 命令

  - `-R` (递归) 选项

  - 不区分大小写选项

  - 输出匹配结果

  - 输出匹配项的文件

  - 输出匹配的行数

  - 输出匹配的词

  - 正则表达式

- 搜索命令输出

- 搜索非匹配项

- 搜索模式

- 在其中搜索

- 结果

- 版本

- 限制到

- 组 ID (`GID`)

- `gunzip` 命令

- `gzip` 命令 2nd

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- `-` 头部

- 使用通配符

- `head` 命令

- 左尖括号 (`<`)

- `less` 命令

- 相关的在线资源

- `Linux` 发行版

- `lo`

- `locate` 命令

- 不区分大小写选项

- 管道输出到分页器

- 更新数据库

- 文件的重复查看

- 回环地址

- `lpq` 命令/`pr` 命令

- `ICMP` 消息

- `ifconfig` 命令 2nd

- `MAC` 地址欺骗

- 使用网络配置

- 网络检查

- `ifdown` 命令

- `ifup` 命令

- `info` 命令 [另参 搜索命令文档]

- 目录节点

- `Expert Info`

- 导航

- 输入流

- 输入/输出流

- 安装软件 [另参 包管理]

- `IP` 地址

- `IPv4` 和 `IPv6`

- `iwconfig` 命令

- 连接加密方案

- `ESSID`



### WEP

### 无线接口配置

### 无线接口状态检查

### 无线网络拓扑

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- 任务 ID 号，打印
- `kill` 命令

## 第五部分：网络

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- 命令行
- `less`
- 不区分大小写选项
- 管道输出到分页器
- 文件的更新
- `lpstat` 命令 2nd
- `Is` 命令
- 彩色编码输出
- 列式输出
- 逗号分隔列表
- 目录内容列出
- 文件大小输出
- 文件类型显示
- 文件列表
- 隐藏文件和文件夹列出、权限和大小
- 长选项
- 管道输出到 `less`
- 倒序输出
- 排序
- `lsof` 命令
- 输出文件的用户
- 管道输出到 `less`
- 特定程序进程列表
- 用户打开的文件

## 第五部分：网络

# MAC (介质访问控制) 地址 2nd

- `man` 命令 [另参 搜索命令文档。]
  - `apropos` 选项
  - 显示 synopsis
  - manpage 分类
  - manpage 章节
  - manpage 更新
  - 输出输出
- man pages [另参 `man` 命令。]
  - 命令分类
  - 数据库重建和更新
  - 查找
  - 打印
  - 使用 `whatis` 访问
- 主机浏览器。
- 内存使用，监控
- `mkdir` 命令
- `mtr` 命令
- `mv` 命令

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- 域名
- 使用 `info` 命令导航
- 网络
- 激活连接
- 停用连接
- DHCP
- DNS
- 加密
- 文件下载
- IP 地址
- IP 路由表
- 网络配置 [另参 `ifconfig` 命令。]
- 网络拓扑
- 网络设备
- 使用非交互式网站连接
- `ping` 检查连接
- 远程登录 [另参 `ssh` 命令。]
- 修改路由表
- 主机之间的安全复制
- 安全文件传输和备份
- 安全文件传输
- 顺序文件下载
- 故障排除
- 无线接口 [另参 `iwconfig` 命令。]
- 与 Windows 机器连接 [另参 Samba].

## 第五部分：网络

- `nmbd`
- `smbclient` 命令
  - `-M` 选项
  - `-S` 选项
  - `-T` 选项
  - 查找文件和打印共享
  - 主浏览器 (Master Browsers)，查询
- `noclobber` 选项
- 节点 (nodes)
- 进制权限

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- 八进制权限
- 输出重定向
- 文件所有权更改
- 组所有者，更改
- 列出

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- 软件包管理
- Debian 发行版：`apt` 参见 `apt` 工具。
- 可下载软件包，查找
- 依赖关系处理 [参见 `apt` 工具]。
- 基于 RPM 的发行版
  - 依赖关系处理 [参见 `yum` (Yellow Dog Updater, Modified), `yum install` 命令。]
- 安装软件包
- 移除软件包
- 分页器 (pagers)
- 父进程 ID (PPID) 数字
- 路径
- 当前目录路径，显示
- 查找
- 周期 ()
- 权限字符
- 权限 第二
- 字母表示法，修改修改
- 文件属性，缩写
- 数字表示法
- 对文件和目录的递归应用
- 粘滞位 (sticky bit)，设置和清除
- suid，设置和清除
- PID (进程 ID) 数字
- `ping` 命令
- 管道 (l)
- PPID (父进程 ID) 数字
- 打印
- 命令行兼容格式
- CUPS (参见 默认打印机、CUPS、取消打印任务到。)
- 进程 ID (进程 ID) 数字
- 进程树
- 程序，不可管道的
- `ps` 命令
  - `grep`，配合使用
  - 将输出管道到 `grep`
  - 进程树
  - `STAT` 字母
- 用户拥有的进程
- `ps2pdf` 命令
- `pump` 命令
- `wd` 命令

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- 问号 (?)
- 引号 (") 第二

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- RAM 使用监控
- 输出重定向
- 正则表达式 (regex)
- 远程登录 [参见 `ssh` 命令。]
- 重命名文件和文件夹

## 第五部分：网络

+ 反序输出，`ls` 命令
- 右尖括号 ()>
- `rm` 命令
  - 交互选项
  - 递归强制选项
  - 详细模式选项
  - 通配符和
- `rmdir` 命令
- `root`
- `route` 命令
- `rpm` 命令
- RPM 软件包
- `rsync` 命令

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- `Samba`
  - 域名
  - 查找并打印共享
  - 登录共享
  - 主浏览器 (Master Browsers)，发现
  - 挂载文件系统
  - Samba 提示符
  - Samba 共享，列出
  - 服务端守护进程
  - 卸载文件系统
  - Samba 服务器上的用户名和组名
  - Windows 工作组
- `scp` 命令
- 截图
- 搜索
  - 命令文档
  - 用于文件 [参见 `locate` 命令。]
  - 文件内 [参见 `grep` 命令。]
  - 远程登录的安全性 [参见 `ssh` 命令。]
- 分号 (;)
- `sftp` 命令
- `smid` 第二
- 共享对象 (.so) 文件
- 单引号
- `sleep` 命令
- `slocate` 命令 第二
- SMB (Server Message Block) 协议
- `smbclient` 命令
  - `-A` 选项
  - `-U` 选项
  - 列出 Samba 共享

## 第五部分：网络

+ 登录共享
- `smbbd`
- `smbmnt` 命令，设置为 suid `root`
- `smbmount` 命令
  - 挂载软链接
- 软件安装 [参见软件包管理。]
- 日期和时间
- 文件扩展名
- 大小
- 源文件，查找
- 空格
- 特殊字符
- 文件名
- 正则表达式
- 欺骗
- 方括号 ([])
- `ssh` 命令
  - `KnownHosts`
  - `hosts` 文件
  - 远程登录
  - 密码登录
- 标准输入，输出和
- 粘滞位 第二
- `su` 命令
  - 登录选项
  - 进入 `root`
- 子文件夹，查看
- `sudo` 命令和 `apt`
- `sudo` 第二
- 系统监控
  - 目录用法
  - 仅总量
  - 文件系统用法
  - 杀死进程
  - 列出文件
  - 列出用户
  - 监控进程
  - 进程树
  - 程序，列出
  - RAM 使用监控
  - 用户拥有的进程
- 查看

## 第五部分：网络

# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- `tail` 命令
  - 多个文件，配合使用
  - 数字选项
  - 对文件的重复操作
- `tar` 命令 第二
  - 在解压前测试 `tar` 包
  - 解压和压缩 `tar` 包
  - 配合压缩
- 文本编辑器
- 波浪号 (--)
- 修改文件的时间
- `top` 命令
- `touch` 命令
  - 创建空文件，配合使用
  - 修改任意时间的文件
  - 更新为当前时间的文件
- `traceroute` 命令

# 索引



# 索引

+ [符号] [A] [B] [C] [D] [E] [F] [G] [H] [I] [J] [K] [L] [M] [N] [O] [P] [Q] [R] [S] [T] [U] [W] [Y] [Z]

- `UID` (用户 ID)
- 下划线 (`_`)
- `unzip` 命令 第二
- `updatedb` 命令
- `URIs` (统一资源标识符) 和 `CUPS`
- 用户 ID (`UID`)
- 用户
- 列出文件
- 切换
- 用户缩写

## 第五部分：网络

- `WEP` (等同加密)
- `WEP` 密钥生成器
- `wget` 命令
- 非交互式文件下载
- 非交互式网站下载
- `which` 命令
- `whereis` 命令
- `WPA` (无线安全网络)
- 通配符
- 复制文件
- 删除文件
- 目录内容，列出
- 正则表达式，对比
- Windows 网络 [参见 Samba。]
- 等同加密 (`WEP`)
- 无线网卡 第二
- 无线网络
- 工作组
- `yum` (`Yellow Dog Updater, Modified`) [另参见软件包管理。]
- `yum install` 命令 第二
- `yum list available` 命令
- `yum remove` 命令
- `yum search` 命令
- `yum update` 命令
