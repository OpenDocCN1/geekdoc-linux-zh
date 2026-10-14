
`[me@linuxbox ~]$ ls /usr/bin | grep`

这列出了`/usr/bin`目录下所有名称包含子字符串`grep`的文件。

`grep`程序以这种方式接受选项和参数：

```
grep [options] regex [file...]
```

其中`regex`是一个正则表达式。

表 19-1 列出了常用的`grep`选项。

| 选项 | 说明 |
|---|---|
| `-i` | 忽略大小写。不区分大写和小写字母。也可以指定`--ignore-case`。 |
| `-v` | 反向匹配。通常，`grep`打印包含匹配项的行。此选项导致`grep`打印不包含匹配项的每一行。也可以指定`--invert-match`。 |
| `-c` | 输出匹配项的数量，如果指定了`-v`选项，则打印非匹配项的数量，而不是行本身。也可以指定`--count`。 |

216 第 7 章

## 表 19-1（续）

| 选项 | 说明 |
|---|---|
| `-l` | 打印每个包含匹配项的文件名，而不是行本身。也可以指定`--files-with-matches`。 |
| `-L` | 类似于`-l`选项，但只打印不包含匹配项的文件。也可以指定`--files-without-match`。 |
| `-n` | 在每个匹配行开头加上该行在文件中的行号。也可以指定`--line-number`。 |
| `-h` | 对于多次搜索，抑制文件名输出。也可以指定`--no-filename`。 |

为了充分探索`grep`，让我们创建一些文本文件进行搜索：

```
me[linuxbox ~]$ ls /bin > distlist-bin.txt
me[linuxbox ~]$ ls /usr/bin > distlist-usr-sbin.txt
```
