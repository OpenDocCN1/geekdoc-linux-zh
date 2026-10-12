
`proxy:x:13:13:proxy:/bin:/sbin/nologin`

`gnats:x:41:41:Gnats Bu-Reporting System (admin):/var/lib/qnats:/usr/sbin/noloiq`

**图 5.35：使用 `grep` 命令的示例**

- 统计`/etc/legal`中空行的数量，并使用选项`-v` (`--invert-match`) 在显示内容时忽略空行；模式`^$`意味着行开始和结束都没有任何内容：

```
agonzalez@ubuntu:-$ grep -c ^ /etc/legal
3
agonzalez@ubuntu:-$ grep -v ^ /etc/legal
```

Ubuntu 系统自带的程序是免费软件；每个程序的具体分发条款在`/usr/share/doc/*/copyright`下的单独文件中说明。

在适用法律允许范围内，Ubuntu 绝对不提供任何保证。

**图 5.36：使用 `grep` 命令的示例**

**图 5.37 到 5.41 显示了使用高级模式和不同 `grep` 选项的不同示例：**

- 检查文件内容并过滤以字母`r`开头，后面跟一个字母`o`（可选）或多个`o`，并以字母`t`结尾：

```
agonzalez@ubuntu:~$ cat text
rt
rot
root
pen
peen
agonzalez@ubuntu:~$ grep -E ro* text
rt
rot
root
```

**图 5.37：使用 `grep` 命令的示例**

- 检查文件内容并过滤以字母`r`开头，后面跟一个或多个`o`，并以字母`t`结尾：

```
agonzalez@ubuntu:~$ grep -E ro+t text
root
```

**图 5.38：使用 `grep` 命令的示例**

- 检查文件内容并过滤以字母`r`开头，后面跟一个`o`（可选）并以字母`t`结尾：

```
agonzalez@ubuntu:~$ grep -E ro?t text
rt
rot
```

**图 5.39：使用 `grep` 命令的示例**

- 检查文件内容并过滤以字母`r`开头，后面跟两个字母`o`，并以字母`t`结尾。过滤以字母`p`开头，后面跟`1`或`2`个字母`e`并以字母`n`结尾：

```
agonzalez@ubuntu:~$ grep -E "ro{2}t" -e "pe{1,2}n" text
root
pen
peen
```

**图 5.40：使用 `grep` 命令的示例**

- 用两种不同的方式检查单词`agonzalez`和`root`：

```
agonzalez@ubuntu:~$ grep -e root agonzalez /etc/passwd
root:x:0:0:root:/:/bin/bash
agonzalez:x:1000:agonzalez,12,1234,1234568:/home/agonzalez:/bin/bash
agonzalez@ubuntu:~$ grep -E "root|agonzalez" /etc/passwd
root:x:0:0:root:/:/bin/bash
agonzalez:x:1000:agonzalez,12,1234,1234568:/home/agonzalez:/bin/bash
```

**图 5.41：使用 `grep` 命令的示例**

## `awk` 命令

`AWK` 是一种模式扫描和处理语言。`awk` 工具使用正则表达式匹配行，并允许它打印某些部分。该命令具有许多选项和复杂操作的可能性；图 5.42 和 5.43 仅显示了一些实际用例：

- 使用`shell` `bash` 的用户的用户名：

```
agonalez@ubuntu:-$ awk '/bash$/{print $1}' /etc/passwd
agonalez
testurer
```

**图 5.42：使用 `awk` 命令的示例**

- 搜索字符串`/home`并打印用户名、主目录和`shell`的列：

```
agonalez@ubuntu:-$ cat /passwd | awk -F: "/home/{print $1\":\"$6\":\"$7}"
syslog:home/syslog
agonzalez:home/agonzalez:/bin/bash
testurer:/home/bash
```

**图 5.43：使用 `awk` 命令的示例**

## 输出格式化

Linux 提供了几种格式化文件输出的工具。默认安装的`coreutils`表 5.18 显示了一些常用命令：

| 命令 | 描述 |
| :--- | :--- |
| `nl` | 给行编号 |
| `sort` | 排序行 |
| `tac` | 反序行 |
| `tr` | 翻译字符 |
| `sed` | 过滤文本 |
| `rev` | 反转行 |
| `wc` | 单词计数 |
| `fmt` | 简单格式化 |
| `uniq` | 消除重复行 |
| `join` | 合并行 |
| `shuf` | 生成随机排列 |

**表 5.18：常用命令**

图 5.44 到 5.55 显示了每个命令的示例：

- 使用`nl`进行行编号：

```
agonalez@ubuntu:-$ nl /etc/legal
```

- 使用`sort`进行字母排序：

```
agonalez@ubuntu:-$ awk -F: '{print $1}' /etc/passwd | sort
agonzalez
root
testurer
```

- 使用`tac`以反的方式可视化文件：

```
agonalez@ubuntu:-$ tac /etc/legal
```

- 使用`tr`转换文本中的字符：

```
agonalez@ubuntu:-$ echo "USER CASE LINE" | tr '[A-Z]' '[a-z]'
upper line
```

- 使用`sed`转换文本中的正则表达式：

```
agonalez@ubuntu:-$ cat /etc/hostname
ubuntu.example.com
agonalez@ubuntu:-$ cat /etc/hostname | sed 's/example.com/localdomain/'
ubuntu.localdomain
```

- 使用`rev`逐字符反转行：

```
agonalez@ubuntu:~$ echo "Hello world" | rev
row olleH
```

- 使用`wc`统计一个文件的行、单词和字符：

```
agonalez@ubuntu:~$ wc /etc/legal
8 38 267 /etc/legal
```

- 使用`fmt`格式化输出，重新格式化段落使用`60`个字符宽度：

```
agonalez@ubuntu:-$ fmt -w 60 /etc/legal
```

- 使用`uniq`删除输出中的重复行。重复行需要相邻：

```
agonalez@ubuntu:~$ cat uniq.txt
one
two
three
two
one
agonalez@ubuntu:~$ cat uniq.txt | sort | uniq
one
three
two
```

**图 5.52: `uniq` 命令的输出示例**

- 使用`join`合并两个具有共同字段的文件：

```
agonzalez@ubuntu:~$ cat names.txt
1 Alberto
2 John
3 Linus
agonzalez@ubuntu:~$ cat lastname.txt
1 Gonzalez
3 Torvalds
agonzalez@ubuntu:~$ join names.txt lastname.txt
1 Alberto Gonzalez
3 Linus Torvalds
```

**图 5.53: `join` 命令的输出示例**

- 使用`paste`按行合并两个文件：

```
zalez@ubuntu:~$ cat names1.txt
Alberto
Linus
John
agonzalez@ubuntu:~$ cat lastname1.txt
Gonzalez
Torvalds
agonzalez@ubuntu:~$ paste names1.txt lastname1.txt
Alberto Gonzalez
Linus Torvalds
```

**图 5.54: `paste` 命令的输出示例**

- 使用`shuf`随机排序行：

```
agonzalez@ubuntu:~$ shuf /etc/password | head -1
apt:x:100:65534::nonexistent/usr/sbin/nologin
agonzalez@ubuntu:~$ shuf /etc/password | head -1
systemd-resolve:x:102:103:systemd Resolver,,,:/run/usr/sbin/nologin
```

**图 5.55: `shuf` 命令的输出示例**

## 文件编辑器与文件管理器
