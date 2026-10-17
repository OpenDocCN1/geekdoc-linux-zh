
# 高级文件处理

```bash
$ cat memo
```

亲爱的 Jim：

此信是为了通知你第二季度的收益看起来并不好。这些将在下周一《华尔街日报》报道公司收益时公布。当然，公司将受到打击，但我们需要保持员工的高士气。我将于明天早上 8:00 召开副总裁会议，在主会议室讨论这个问题。到时见。

Nem

```bash
$ mcrypt memo
```

输入密码（最多 512 个字符）

请使用大小写字母和数字的组合。

```bash
Enter passphrase: xxxxxxxxxx
Enter passphrase: xxxxxxxxxx
File memo was encrypted.nc
```

```bash
$ cat memo.nc
```

```text
mrijdaele-128 cmcrypt-sha1???????????r?<??^??^??sha1=7i=??@gnNrr??!p!!J??oB
???7n!!?3F67???a7??<7??<7i??fji(gp)??<7????K??l4L??.??|1???EPG5
F)??(N-7B7)??????Btm7Y7??7Jw??YG&??????77vcgb7??|D=??o??
??$7L????7???999??.a7??/oa??7J7Cy?#??RhRRB??=!!lW.D??ivav??
??????????????7??yxht??B7,zS
?????TTG$7s?MC6n???|@??Fhunqut??r<7??nrK??Q7??t????y??
??U=-ht-z23????gtq??????:7yb????7??QMmtx
~~~=(J7TJ3)????Q0P7karavmtInt18--lineueze/ch $
```

解密文件 `memo.nc` 并在 `memo` 中还原原始版本的命令如下。`cat` 命令确认原始文件已恢复。`ls -l` 的输出显示文件大小比原始文件大约 20%。

```bash
# Advanced File Processing
$ crypt -d memo.nc
mcrypt: memo already exists; do you wish to overwrite (y or n)?
Enter passphrase: xxxxxxxxxx
File memo.nc was decrypted.

$ more memo
Dear Jim,
此信是为了通知你第二季度的收益看起来并不好。这些将在下周一《华尔街日报》报道公司收益时公布。当然，公司将受到打击，但我们需要保持员工的高士气。我将于明天早上 8:00 召开副总裁会议，在主会议室讨论这个问题。到时见。确保这些信息在此之前不泄露。

$ ls -l
-rw------ 1 user faculty Feb 27 01:42 memo
-rw------ 1 user faculty Feb 27 01:42 memo.nc
```

你可以像下面的会话所示，使用 `-k` 选项在命令行指定关键字。

```bash
$ crypt memo -k 123
Warning: It is insecure to specify keywords in the command line
File memo.nc was encrypted.

$ crypt -d memo.nc -k 123
Warning: It is insecure to specify keywords in the command line
File was decrypted.
```

你可以使用 `-z`（或 `-p`）选项在加密前压缩文件。加密后的文件存放在 `memo.gz` 中。解密后，压缩文件位于 `memo.gz`，可以使用 `gunzip` 解压。

```bash
$ crypt -k 123 -z memo
Warning: It is insecure to specify keywords in the command line
File was encrypted.

$ ls -l
total 8
-rw------ 1 user faculty Feb 27 09:03 memo
-rw------ 1 user faculty Feb 27 09:03 memo.gz

$ crypt -d memo.gz -k 123
Warning: It is insecure to specify keywords in the command line
File memo.gz.nc was decrypted.

$ ls -l
total 12
-rw------ 1 user faculty Feb 27 09:03 memo
-rw------ 1 user faculty Feb 27 09:03 memo.gz
-rw------ 1 user faculty Feb 27 09:03 memo.gz.nc

$ gunzip -v memo.gz
gzip: memo.gz already exists; do you wish to overwrite (y or n)?
Enter
memo.gz: 38.4% -- replaced with memo
```

再次强调，`crypt` 命令不会删除它所加密（或解密）的文件，加密后删除原始文件是你的责任。注意，即使是超级计算机，没有正确的密钥无法解密加密文件。你可以在加密前后使用 `md5sum` 命令验证源文件和解密文件是否相同。

`crypt` 命令允许你使用它支持的多种加密算法之一。你可以运行 `crypt --list-hash` 命令显示这些算法的名称。你可以在下面的会话中使用 `-h` 选项使用这些算法对文件进行加密（和解密）。

```bash
$ crypt --list-hash
Supported Hash Algorithms:
crc32
md5
...
sha1
...
md2

$ crypt -h -k 123 memo
Warning: It is insecure to specify keywords in the command line
File memo.nc was encrypted.

$ ls -l memo.nc
-rw-r--r-- 1 user faculty Feb 27 01:42 memo.nc

$ crypt -d -k 123 memo.nc
Warning: It is insecure to specify keywords in the command line
crypt: memo.nc already exists; do you wish to overwrite (y or n)?
Enter
File memo was decrypted.
```

如果你的工作需要更高安全级别的文档和通信，你应该使用 `openssl` 工具，它允许你使用多种加密函数，包括：

- 使用密码进行加密和解密
- 公钥和私钥的创建与管理
- 公钥加密操作
- 处理加密电子邮件

`openssl` 和 `crypto` 的范围超出了本书的内容。你可以通过 `man openssl` 和 `crypto` 命令学习更多信息。此外，我们在书籍网站的第 26 章第 27.3–27.5 节介绍了如何使用 Linux `gpg` 加密工具执行各种形式的磁盘加密。`gpg` 是 GNU Privacy Guard (GnuPG) 的 OpenPGP 版本。

以下章内练习将让你练习使用 `mcrypt` 命令，并通过实际操作帮助你理解其语义。

### 练习 7.1

在你的系统上尝试本节提供的 `mcrypt` 命令会话。

## 总结

有时需要对文本和非文本文件执行一些高级操作。这些操作包括压缩和解压缩文件内容、排序文件、在文件系统结构中搜索文件和命令、搜索某些字符串或模式、执行类似数据库的操作（从表格中切割文件或粘贴表格）、将非 ASCII 文件转换为 ASCII，以及加密和解密文件。Linux 中有工具可以执行这些任务。

这些工具中的某些能够通过一个由常量和正则表达式组成的单个字符字符串来指定一组字符串。正则表达式通常被称为搜索模式，包括 `awk`、`egrep`、`grep`、`sed` 和 `vim`。在本章中，我们描述了正则表达式以及允许使用正则表达式的工具以及它们在 `vim`、`egrep` 和 `grep` 中的用法。

`sort` 命令可排序文本文件。每行包含一个带有多个字段的记录，所有行的字段数量相同。文本也可以像这样被处理

## 高级文件处理

使用 `cut` 和 `paste` 命令可以分别实现表格列的提取和表格合并。`sort`、`cut` 和 `paste` 命令可以通过管道（见第 9 章）组合，以根据不同的标准生成表格。

`find` 和 `where` 命令可用于搜索 Linux 文件系统结构，以确定文件和命令的位置（绝对路径）。`find` 命令尤其强大，允许你根据标准（如文件大小）搜索文件。`which` 命令用于确定执行的是哪一个命令，当系统中存在多个版本时。
