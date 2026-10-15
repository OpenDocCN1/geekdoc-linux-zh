
/bin/tar cf maggie.tar /home/maggie

你也可以使用连字符（`-`）来指定命令行参数。例如，你可以按照如下方式运行之前的命令：`tar -cf maggie.tar /home/maggie`

/home/maggie 目录下的所有文件都存储在 maggie.tar tar 文件中。
`f` 参数指定下一个参数将是 tar 文件。以下命令列出了 maggie.tar 的内容：

```
tar tf maggie.tar
```

列表 9-1 显示了 maggie.tar 的列出。

**列表 9-1: tar 格式的文件 maggie.tar**

```
+   /
.Xclients
.Xdefaults
.bash_logout
.bash_profile
.bashrc
.xsession
.bash_history
```

你可以使用详细模式 `verbose — v —` 参数来显示更多信息。如果你在创建或提取归档时使用它，每个文件会在复制或提取时显示出来。将其与列出选项 `t` 配合使用可以产生与 `ls` 命令的长格式（`ls -l`）类似的列表。

要恢复这些文件，请使用如下命令所示的提取选项：

```
tar xf maggie.tar
```

提取出的文件将放在当前目录中，除非你指定 tar 使用绝对路径 `- P —` 选项，在这种情况下，tar 会尝试将文件恢复到 /home/maggie 的原始位置。

# 第 9 章：网络与计算机管理

![](img/29df11d9c5c608cff7b4fa65d0c78e37_384_0.png)

随你的 CD-ROM（Red Hat 5.0）附带的 tar 版本足够聪明，不会将归档本身包含在其中。句话说，如果你将文件复制到恰好位于保存目录下的 tar 文件中，那么你正在创建的 tar 文件将不会被包含在。然而，旧版本会乐意将自己包含在所创建的 tar 文件中。

较新版本的 GNU tar（例如本书籍附带 CD-ROM 提供的版本）现在包含了 gzip 压缩作为选项。之前创建和提取 tar 文件的示例可以包含使用 `gzip -z -` 的压缩，如下命令所示：

```
tar czf maggie.tgz /home/maggie

tar xzf maggie.tgz /home/maggie
```
