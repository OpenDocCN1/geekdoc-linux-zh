

## uncompress:

```
$ uncompress backup.tar.Z
$ ls -l backup.tar
-rw-r--r-- 1 taylor wheel 15800320 Feb  8 02:58 backup.tar
```

3. 原来压缩还有一个有用的标志，可以让你看到它压缩了多少：

```
$ compress -v backup.tar
backup.tar: 49.4% OK
```

用计算器快速算一下就能确认它大约小了 50%。在收尾之前，我想再解压一次：

```
$ uncompress -v backup.tar.Z
backup.tar.Z: 202.3% OK
```

4. 为了对比，我们快速看看 zip 命令，它提供了非常相似的功能：

```
$ ls -l backup.tar
-rw-r--r-- 1 taylor wheel 15800320 Feb  8 02:58 backup.tar
$ zip backup.tar.zip backup.tar
  adding: backup.tar (deflated 67%)
$ ls -l backup.tar.Z
ls: backup.tar.Z: No such file or directory
```

哎呀！我是在自动驾驶。事实上，当调用 zip 时，它有两个必需的参数：归档名和要放入归档的文件或文件夹名。所以不是 .Z 而是 .zip：

```
$ ls -l backup.tar.zip
-rw-r--r-- 1 taylor wheel 5214105 Feb  8 02:58 backup.tar.zip
$
```

你可以看到它对这个特定文件压缩得比 compress 好：只有 5.5MB，而不是 7.8MB。不同文件会有不同的 compress/zip 结果，而且由于压缩算法发明者才知道的原因，一些罕见文件压缩后也不会变小。

5. 要解压（展开）文件，使用 unzip，如前所示：

```
$ unzip backup.tar.zip
Archive: backup.tar.zip
replace backup.tar? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
  inflating: backup.tar
$
```

一切恢复正常！

## Note

根据你的 Unix 或 Linux 发行版，有多种不同的 zip 归档程序可用，包括 `gzip`、`bzip2` 和 `rzip`。它们在细节上有差异，但如果你经常发送大量归档文件或你的 Unix 系统空间紧张，都值得研究。

你拥有的大多数文件可能太小，不必担心压缩以节省空间。但如果你正在构建大型归档文件，或者计划通过 FTP 传输大型文件，`compress` 或 `zip` 可以成为你的新好朋友，为你节省大量传输时间。

## Exploring the Unix Tape Command: cpio

你不会感到惊讶，Unix 系统有通用备份程序，可选择写入磁带设备或其他归档数据存储单元。它叫做 `cpio`，使用方式与 Unix 的整体哲学一致。

## Action 19.4: A Quick Exploration of cpio

要更全面地了解这个命令的工作原理，有必要在实际操作中看到它。

- 1. `cpio` 与 `tar` 最重要的区别在于 `cpio` 期望从标准输入读取需要备份的文件列表，而不是作为命令行上指定的目录或一组文件名。

这看起来似乎不是什么大事，但实际上确实如此，特别是当你将 `cpio` 与 `find` 命令结合使用时。典型的用法如下：

```
$ find . -name "*.c" -print | cpio -oO sourcefiles.cpio
$
```

此调用（-o 表示我想要创建输出归档，-O 让我指定输出文件名）创建了一个名为 `sourcefiles.cpio` 的归档，其中包含当前目录及以下所有 `*.c` 源文件。用 `tar` 实现这一点会相当棘手。

- 2. 我可以检查归档的内容：

```
$ cpio -itI sourcefiles.cpio
./bin/fixit.c
./Src/Embot/embot.c
./Src/Embot/error.c
./Src/Embot/interact.c
./Src/Embot/log.c
./Src/Embot/mail_utils.c
./Src/Embot/savemsg.c
./Src/Embot/sendfile.c
./Src/Embot/utils.c
./Src/Misc/usage_summary.c
./Src/Misc/fixit.c
./Src/Misc/info.c
./Src/Misc/isnew.c
./Src/Misc/mydates.c
./Src/Misc/showmatches.c
./Src/Misc/change.c
./Src/change.c
./Src/cleanup.c
./Src/cribbage.c
./Src/expandurl.c
./Src/extract-mail.c
./Src/futuredate.c
./Src/import.c
./Src/assemble.c
./Src/make-html.c
./Src/old-import.c
./Src/process-data.c
./Src/showmatches.c
./Src/sum-up.c
./Src/text-counter.c
./Src/login.c
./Src/calc.c
$
```

在这种情况下，-i 标志表示我希望它读取现有归档，-t 表示我只想要文件列表，而不是提取它们，-I 让我指定输入文件名。

### 3. 最简单提取文件的方法是指定应进行比较的模式。

注意在这种情况下，我将把归档作为标准输入馈送给 cpio。这是使用该命令的常见方式：

```
$ cpio -i cribbage < sourcefile.cpio
cpio: WARNING! These patterns were not matched:
cribbage
$
```

不行。模式 cribbage 没起作用。事实上，它不是正则表达式，所以 cpio 有帮助地指出没有匹配项。这里是改进的尝试：

```
$ cpio -i "*cribbage*" < *cpio
cpio: Unable to create ./Src/cribbage.c <No such file or directory>
$
```

### 4. 我们几乎成功了，但仍然存在一个问题，尽管 cpio 的错误信息在解释发生了什么方面不是很有帮助。问题是 Src 目录不存在，而程序在没有添加新标志 -d 的情况下无法创建子目录。然而，错误信息比说明这一事实更令人困惑。

顺便说一下，我还会添加 -v 以确保在解包时有一些详细输出：

```
$ cpio -ivd '*cribbage*' < *cpio
./Src/cribbage.c
30 blocks
$
```

