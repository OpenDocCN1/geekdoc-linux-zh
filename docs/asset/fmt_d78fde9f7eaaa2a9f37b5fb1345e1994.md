
你也可以使用 `mv` 命令来更改文件的位置。如上一个示例所示，内容保持不变，但文件被移动并有了新名称。将移动想象成将东西从一个地方物理移动到另一个地方。它的位置变了，但内容没有。在下面的示例中，`x2.file` 被移动到 `dirA` 目录并重命名为 `y2.file`。

```
mv x2.file /dirA/y2.file
```

## 当源和目的名称相同时使用 mv 命令

源文件和目的文件具有相同唯一情况是当你将其移动到另一个目录时。如前所述，你不能将一个文件重命名为它当前的名称。然而，在示例 `mv /dirB/x2.file /dirA/x2.file` 中，实际文件名保持不变——`x2.file`。这是源目录名 `dirB` 和目的目录名 `dirA`。对于 Linux 来说，这产生了两个完全不同的文件名。

接下来将使用 `cp` 和 `mv` 命令来熟悉它们的工作原理。要复制和移动文件：

- 1. 以用户身份登录 Linux 系统，然后打开终端 `Terminal` 窗口。
- 2. 输入 `mkdir dirA`，然后按回车。
- 3. 首先，你需要创建一个文件进行复制。使用 `vi` 创建名为 `file.dat` 的文件。
- 4. 输入 `cp file.dat`，然后按回车复制你上一步创建的文件。
- 5. 输入 `ls`，然后按回车。注意文件列表包含了你刚刚创建的文件以及该文件的副本。
- 6. 输入 `cp file.dat file.dat`，然后按回车。该命令会交互式提示你是否要覆盖该文件。
- 7. 输入 `y`，然后按回车。
- 8. 输入 `mv file.dat file.dat`，然后按回车。`file.dat` 被移动到了 `dirA`。
- 9. 输入 `mv -i file.dat file.dat`，然后按回车。该命令会交互式提示你是否要覆盖该文件。
- 10. 输入 `y`，然后按回车。
- 11. 输入 `ls`，然后按回车。注意 `file.dat` 不再存在，但在 `dirA` 现在有了 `file.dat`（在复制或移动之前）。你还可以看到在 `cp` 和 `mv` 命令中使用 `-i` 选项时生成的信息，如图 2-12 所示。
- 12. 要退出终端仿真，输入 `exit`，然后按回车。

![](img/72e8a95d2755ff262251b6d24baa) 图 2-12 cp 和 mv 命令的输出

## sort 命令

`sort` 命令用于按升序或降序排序数据。例如，如果你想按字母顺序对包含名称的文件进行排序，可以使用此命令。或者，如果你想按降序对数字字段进行排序，也可以使用 `sort` 命令。`sort` 命令的基本语法为：

```
sort filename
```

为了对 `unsorted.dat` 文件运行 `sort` 命令，输入以下命令：

```
sort unsorted.dat
```

当你使用 `sort` 命令时，默认是将输出显示在屏幕上。然而，你可以使用大于符号 `>` 将输出重定向到文件。下面的示例对名为 `unsorted.dat` 的文件排序并输出到名为 `sort.dat` 的文件中。原始文件保持完好，因为输出被重定向到了文件。跟随大于符号的文件名是用户定义的。

```
sort unsorted.dat > sort.dat
```

默认情况下，`sort` 命令按升序排序。你可以使用 `-r` 选项按降序排序：

```
sort -r filename
```

## cut 命令

`cut` 命令允许你从文件中提取文本并显示在屏幕上或重定向到另一个文件。该命令通常用于提取文件中的字段。`cut` 不更改原始文件，它会自动为你打开文件。`cut` 命令的基本语法为：

```
cut filename
```

你需要注意两个重要的选项。`-d` 选项用于识别分隔符。冒号通常用作字段之间的分隔符，让字段的开始和结束。例如，`-d:` 指定冒号为分隔符。`-f` 选项用于根据分隔符识别你想要的字段。例如考虑以下记录：

```
1001:King Pup:Dog
```

第一个字段 "1001"，第二个字段 "King Pup," 代表名称，第三个字段 "Dog," 代表类型。冒号在示例中用于分隔字段。你使用冒号或其他字符而不是空格来分隔字段。空格可能会分隔单词。假设文件名为 `animal.dat`，显示第一个和三个字段的命令为：

```
cut -d:-f1 animal.dat
cut -d:-f1,3 animal.dat
```

# 第 2 章 理解 Linux 文件系统

接下来你将创建一个包含若干员工记录的文件。每个记录将由两个字段组成——员工编号后跟冒号和员工名称。

在未使用 `cut` 命令：

- 1. 以用户身份登录 Linux 系统，然后打开终端窗口。
- 2. 输入 `mkdir dirA`，然后按回车。
- 3. 首先，你需要创建一个文件进行复制。使用 `vi` 创建名为 `file.dat` 的文件。
- 4. 输入 `cp file.dat`，然后按回车复制上一步创建的文件。
- 5. 输入 `ls`，然后按回车。注意文件列表包含了你刚刚创建的文件以及该文件的副本。
- 6. 输入 `cp file.dat file.dat`，然后按回车。该命令会交互式提示你是否要覆盖该文件。
- 7. 输入 `y`，然后按回车。
- 8. 输入 `mv file.dat file.dat`，然后按回车。`file.dat` 被移动到了 `dirA`。
- 9. 输入 `mv -i file.dat file.dat`，然后按回车。该命令会交互式提示你是否要覆盖该文件。
- 10. 输入 `y`，然后按回车。
- 11. 输入 `ls`，然后按回车。注意 `file.dat` 不再存在，但在 `dirA` 现在有了 `file.dat`（在复制或移动之前）。你还可以看到在 `cp` 和 `mv` 命令中使用 `-i` 选项时生成的信息。
- 12. 要退出终端仿真，输入 `exit`，然后按回车。

图 2-12 cp 和 mv 命令的输出

## 理解文件管理命令

```
$ sort -n unsorted.dat

1:Jessie James Garcia

2:Jessie James Garcia

3:Zachary Scott

4:Lorenzo Todd von Scholz

5:Mickey Sunday-Washington
```

```
$ cut -d:f2 unsorted.dat > name.dat

1:Jessie James Garcia

2:Jessie James Garcia

3:Zachary Scott

4:Lorenzo Todd von Scholz

5:Mickey Sunday-Washington
```

```
$ cat name.dat

1:Jessie James Garcia

2:Jessie James Garcia

3:Zachary Scott

4:Lorenzo Todd von Scholz

5:Mickey Sunday-Washington
```

## paste 命令

与 `cut` 命令从一个文件中提取字段不同，`paste` 命令是将数据从一个文件复制、粘贴或合并到另一个文件。上面的代码将文件二的每一行与文件一每一行合并。数据可以合并到一个新文件中。`paste` 命令的基本语法为：

```
paste filename_one filename_two
```

上面的代码将文件二的每一行与文件一每一行合并。例如，假设你有两个包含名称数据的文件。`last.dat` 文件的内容是 Smith Adams，而第一个文件的内容是 Mary Sue。如果你输入命令 `paste first.dat last.dat`，那么输出到屏幕的内容将是：

- Joe Smith
- Mary Jones
- Sue Adams

如果你输入命令 `paste last.dat first.dat`，那么输出将是：

- Joe Joe
- Jones Mary
- Adams Sue

原始文件的内容保持不变。你还可以使用重定向输出符号 `>` 创建一个全新的文件。如果你输入命令 `paste first.dat last.dat > first.dat, last.dat`，将创建一个名为 `first_last.dat` 的新文件，其中包含来自 `first.dat` 和 `last.dat` 的合并数据。

# 第 2 章 理解 Linux 文件系统

假设“妈妈硬件用品店”维护两个独立的文件。一个文件名为 `product`（产品），包含畅销商品的名称；另一个文件名为 `quantity`（数量），包含已订购销售商品的数量。店主们希望这些信息出现在一个名为 `orders`（订单）的文件中。为了实现这一点，你需要将这些文件合并在一起。图 2–14 显示了两个原始文件的内容，以及使用 `paste` 命令合并这些文件并将内容重定向到新文件的用法。
