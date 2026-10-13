
## 重新组装分割文件：cat

如果你有一堆分割的文件想要重新组合起来，该怎么办？很简单——还记得 `cat` 命令吗？当你有一系列文件命名为类似 `<basename>`、`<basename>aa`、`<basename>ab`、`<basename>ac`... `<basename>zz` 时，你可以通过以下方式发出 `cat` 命令来重新组装它们：`cat <basename>* > complete.file`。`cat` 为你连接文件后，你可以将 `complete.file`（或你命名的任何名称）用 `mv` 移动到你想要的任何最终名称。

![](img/2c005cbaad58c25c7f54da948131a75e_108_0.png)

> **处理输出文件** 最好将输出文件命名为 complete file 之类的名称——与 `<basename>` 完全不同——然后再将其移动到目标位置或最终文件名。这可以避免在你真的希望最终文件名仅为 `<basename>` 的情况下可能出现的混淆

## 比较和修订文件：diff AND patch

你可能习惯于创建文档并发送修订版。不幸的是，大多数时候你可能不得不发送完整的文件副本，而实际上只有这里那里改动了几个词。在 UNIX 社区中，有大量的信息交流，源代码不断地在各方之间传递。与其总是发送完整文件，人们依靠 `diff` 和 `patch` 命令只传输修订之间发生变化的信息。

## 使用 diff

`diff` 函数接受两个文件——原始模板文件和更新后的文件——并生成一个输出 `patchfile`，其中包含足够的信息，仅凭 patchfile 和模板文件即可重建更新后的文件。假设你有原始文件 `templatefile.txt`，其内容如下：

```
Now is the time for all good
kiwis to come to the aid of
puppies.
```

你将此文件分发给所有同事。（这只是一个例子，大家。）然而，几天后你将这个精彩的文件更新为新文件——updatedfile.txt——看起来像这样：

```
Now is the time for all good and bad
kiwis to come to the aid of
puppies and children.
```

与其将新文件 (updatedfile.txt) 重新分发给每个人，你只需制作一个包含原始文件和新文件之间所有更改的补丁。为此，使用以下语法使用 diff 命令：diff <template file> <updated file> > <patchfile>。patchfile 可以是你想要的任何文件名。

> **重定向输出** 此示例中的独立 > 用于将输出重定向到特定文件，由你命名。你可以在第 12 课“输入和输出”中了解更多关于重定向的内容。

例如

```
>diff templatefile.txt updatedfile.txt > patchfile.txt
```

程序将运行并返回命令行，没有任何消息。如果你有兴趣查看 patchfile 的内容，可以随意使用 cat 或 more 查看它。在此示例中，生成的 patchfile 命名为 patchfile.txt；将其分发给拥有原始 templatefile.txt 并需要更新它的人。

> **文件比较** diff 命令在你只想知道两个相同文件的副本是否相同或不相同的情况下也很实用。如果你发现自己有多个相似文件的副本，diff 是快速了解它们是否相同的方法，如果不相同，则了解它们之间做了哪些更改。如果 diff 没有输出，则文件之间没有差异。

## 使用 patch

现在 patch 程序派上用场了。你只需为 patch 提供你想要修补的文件名，然后是 patchfile 的名称即可调用它。

例如

```
>patch templatefile.txt patchfile.txt
patching file 'templatefile.txt'
```

就是这样。文件 templatefile.txt 现在已被更新，并且与文件 updatedfile.txt 相同。你可以通过查看 templatefile.txt 来验证这一点：

```
>cat templatefile.txt
Now is the time for all good and bad
kiwis to come to the aid of
puppies and children.
```

如果你查看了 patchfile，你可能会注意到它的大小与 updatedfile.txt 差不多，那么为什么不直接分发整个文件而不是补丁呢？对于像本示例中使用的这样的小文件，创建补丁真的没有意义。然而，如果你处理的是几千行长的文件，其中中间只有一两行被更改，你会发现 patch 和 diff 是避免发送大量冗余信息的绝佳方法。

> **重要提醒** 请务必记住保留模板文件的副本。在此示例中，补丁直接应用于模板文件，并且模板文件已更新。如果所有后续补丁都是基于更新后的文件创建的，没有问题；然而，如果补丁是基于原始模板创建的，则 templatefile.txt 不再可以被修补。

## 摘要

你刚刚学习的命令展示了 UNIX 操作系统内置的一些强大功能。你可能在其他桌面系统上见过类似的实用工具，但它们是附加组件或商业软件的一部分。在 UNIX 的情况下，这一切都是操作系统的一部分，还有更多内容！以下是本课所学内容的回顾：

- **wc**—wc 命令可以为单个文件或一组文件提供快速的字符、行数和词数统计。
- **sort**—sort 使你能够对文本文件中单独行包含的信息进行排序。它理解数据列/字段的概念，因此你可以用它以多种不同的格式对数据进行排序。
- **split**—如果你有文件在发送电子邮件、写入软盘等时有点太大，可以使用 split 命令将其切分成更小的文件。split 可以创建包含一定数量行、千字节或兆字节的文件。
- **diff/patch**—diff 和 patch 的组合使你能够以高效的方式分发更新（文档、源代码等）。而不是发送整个更新文件的副本，你可以使用 diff 创建仅包含一个文件版本与下一个版本之间更改的 patchfile。

## 第 10 课

## 压缩和归档工具

![](img/2c005cbaad58c25c7f54da948131a75e_112_0.png)

*在本课中，你将学习用于压缩和归档文件的常见 UNIX 工具，以及一些可用于监控磁盘使用情况的工具。*

尽管节约磁盘空间几乎已成为过去，但偶尔仍有必要压缩文件或将其打包用于归档目的。

## 压缩文件

从历史上看，硬盘存储空间在企业和家庭使用环境中都是昂贵的商品。

> **时代确实在变** 纯粹从历史角度来看，一块 80Mb SCSI-1 驱动器在 1988 年售价为 369 美元，而作者的一位朋友最近找到的一块用于 PC-AT 的 20Mb MFM 替换驱动器包含了其原始包装收据——账单高达 720 美元！今天，500 美元可以买到 5GB 或更多的存储空间。

随着今天极其便宜的硬盘驱动器，最大化磁盘使用效率的压力比过去低得多；但在某些环境中，例如学校，压力仍然存在。如果你碰巧使用的是磁盘空间非常宝贵的环境，你可以使用本课压缩部分中的命令来减少文件占用的空间——或在允许的空间中容纳更多内容。即使磁盘空间不是你的问题，在通过电子邮件发送文件或通过互联网分发文件等情况下，压缩文件也可能是明智的选择。

使用 UNIX 时，你可能会遇到三种主要的压缩格式：使用 UNIX 程序 compress 制作的压缩文件、使用 UNIX 或个人计算机版本的 PKZIP 程序制作的 zip 文件，以及使用 GNU gzip 实用程序制作的 gzipped 文件。每种格式都有用于压缩和解压缩的程序集。最近出现的 bzip2 压缩实用程序也值得关注，尽管它是新来者，但对于紧密压缩看起来很有前景。

## compress/uncompress/zcat

创意命名的 compress 命令使用一种较旧的 UNIX 压缩格式，随着 gzip 格式流行度增加而逐渐消亡。使用 compress 命令创建的文件具有文件后缀 .Z。要使用 compress 命令压缩文件，你只需按 compress <filename> 发出命令。

同样创意命名的 uncompress 命令解压缩（惊喜！）compress 命令的结果。要使用 uncompress 命令，你按 uncompress <filename>.Z 发出命令。

zcat 命令（其名称略少直观）是 cat 的一个版本，它读取压缩文件而不是普通文本文件。

使用 zcat 与使用 compress 和 uncompress 一样直观；按 zcat <filename>.Z 发出命令。如果你想查看大文件，可以将输出通过管道传输到你偏好的分页器。为此，按 zcat <filename>.Z | more 发出命令。竖线 | 是 UNIX 管道字符——它将前一个命令的输出传输到后一个命令的输入。（你将在第 12 课“输入和输出”中了解更多相关内容。）

例如，如果你有一个名为 stuffed.Z 的压缩文件，并且想在不先解压缩的情况下读取 stuffed，你可以输入：

```
> zcat stuffed.Z | more
```
