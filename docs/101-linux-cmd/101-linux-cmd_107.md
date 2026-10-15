
# `grep` 命令

`grep` 过滤器在文件中搜索特定的字符模式，并显示所有包含该模式的行。`grep` 代表全局搜索正则表达式并打印出来。在文件中搜索的模式被称为正则表达式。

## 示例

1. 为了在 `destination.txt` 文件的内容中搜索字符串（`"KeY"`）而不区分大小写。

```sh
grep -i "KeY" destination.txt
```

2. 显示匹配项的数量

```sh
grep -c "key" destination.txt
```

3. 我们可以搜索多个文件，并且只显示包含给定字符串/模式的文件。

```sh
grep -l "key" destination1.txt destination2.txt destination3.txt destination4.txt
```

4. 显示包含匹配行的文件的行号。

```sh
grep -n "key" destination.txt
```

5. 如果你想搜索监控的日志文件，可以添加 `--line-buffered` 来实时搜索它们。

```sh
tail -f destination.txt | grep --line-buffered "key"
```

## 语法

`grep` 命令的一般语法如下：

```sh
grep [options] pattern [files]
```

## 其他标志及其功能

| 短标志 | 长标志 | 描述 |
| :-- | :-- | :-- |
| `-c` | `--count` | 为每个输入文件打印匹配行的计数 |
| `-h` | `--no-filename` | 显示匹配行，但不显示文件名 |
| `-i` | `--ignore-case` | 忽略大小写进行匹配 |
| `-l` | `--files-with-matches` | 仅显示文件名列表 |
| `-n` | `--line-number` | 显示匹配行及其行号 |
| `-v` | `--invert-match` | 此选项将打印出所有不匹配模式的行 |
| `-e` | `--regexp=` | 使用此选项指定表达式。可以多次使用 |
| `-f` | `--file=` | 从文件中读取模式，每行一个 |
| `-F` | `--fixed-strings=` | 将模式解释为固定字符串，而不是正则表达式 |
| `-E` | `--extended-regexp` | 将模式视为扩展正则表达式（ERE） |
| `-w` | `--word-regexp` | 匹配整个单词 |
| `-o` | `--only-matching` | 仅打印匹配行的匹配部分，每个部分单独一行输出 |
|  | `--line-buffered` | 强制输出为行缓冲 |

## 其他实用示例

1. 在目录中的所有文件中进行递归搜索

```sh
grep -r "pattern" /path/to/directory
```

2. 仅搜索整个单词（不匹配部分单词）

```sh
grep -w "key" destination.txt
```

3. 显示不包含该模式的行（反向匹配）

```sh
grep -v "unwanted" destination.txt
```

4. 使用扩展正则表达式搜索多个模式

```sh
grep -E "pattern1|pattern2" destination.txt
```

5. 搜索并显示匹配的前后文行（匹配前后的行）

```sh
# 显示每个匹配前 2 行和后 2 行
grep -C 2 "error" logfile.txt

# 仅显示每个匹配前 3 行
grep -B 3 "error" logfile.txt

# 仅显示每个匹配后 3 行
grep -A 3 "error" logfile.txt
```

6. 在行的开始或结束处搜索模式

```sh
# 显示以 "Error" 开头的行
grep "^Error" logfile.txt

# 显示以 ".txt" 结尾的行
grep "\.txt$" filelist.txt
```

7. 在多个文件中计算总匹配数

```sh
grep -c "pattern" file1.txt file2.txt file3.txt
```

8. 查找包含模式的文件并将结果传递给其他命令

```sh
# 查找所有包含 "import numpy" 的 Python 文件
grep -r "import numpy" --include="*.py" .

# 在压缩日志文件中搜索
zgrep "error" /var/log/syslog.*.gz
```
