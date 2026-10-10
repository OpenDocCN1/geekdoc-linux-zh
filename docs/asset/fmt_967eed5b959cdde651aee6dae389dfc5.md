
`$ sleep 600`

`^Z`

`[8]+ Stopped sleep 600`

## 第 38 章：case 语句

### 第 38.1 节：简单 case 语句

在所有版本 bash 都支持的最简单形式中，`case` 语句执行匹配模式的 case 分支；`;` 运算符在第一次匹配后（如果有的话）中断。

```bash
#!/bin/bash

var=1

case $var in
1)
    echo "Antarctica"
    ;;
2)
    echo "Brazil"
    ;;
3)
    echo "Cat"
    ;;
esac
```

输出：

Antarctica

### 第 38.2 节：具有穿透（fall through）功能的 case 语句

**版本 ≥ 4.0**

从 bash 4.0 开始，引入了一个新运算符 `;&`，它提供了穿透机制。

```bash
#!/bin/bash

var=1

case $var in
1)
    echo "Antarctica"
    ;&
2)
    echo "Brazil"
    ;&
3)
    echo "Cat"
    ;&
esac
```

输出：

Antarctica
Brazil
Cat

### 第 38.3 节：仅当后续模式匹配时才穿透

**版本 ≥ 4.0**

从 Bash 4.0 开始，引入了另一个运算符 `;;&`，它也提供了穿透功能，但仅当后续 case 语句（如果有）中的模式匹配时才穿透。

```bash
#!/bin/bash

var=abc

case $var in
a)
    echo "Antarctica"
    ;;&
xyz)
    echo "Brazil"
    ;;&
*b)
    echo "Cat"
    ;;&
esac
```

输出：

Antarctica
Cat

在下例示例中，`abc` 匹配第一个和第三个 case，但不匹配第二个 case。因此，不执行第二个 case。

## 第 39 章：逐行（和或逐字段）读取文件（数据流、变量）？

| 参数 | 详情 |
| --- | --- |
| `IFS` | 内部字段分隔符 |
| `file` | 文件名/路径 |
| `-r` | 防止读取时解释反斜杠 |
| `-t` | 移除 `read` 读取的每行末尾的换行符 |
| `-d DELIM` | 继续直到读取到 `DELIM` 的第一个字符（使用 `read` 时），而不是换行符 |

### 第 39.1 节：逐行循环文件

```bash
while IFS= -r line; do
    echo "$line"
done < file
```

如果文件可能不包含末尾换行符，则：

```bash
while IFS= -r line || [ -n "$line" ]; do
    echo "$line"
done < file
```

### 第 39.2 节：逐字段循环命令输出

假设字段分隔符为：

```bash
while IFS= read -d : -r field || [ -n "$field" ]; do
    echo "$field"
done <(ping google.com)
```

使用管道时：

```bash
ping google.com | while IFS= read -d : -r field || [ -n "$field" ]; do
    echo "$field"
done
```

### 第 39.3 节：将文件行读入数组

```bash
readarray -t file
```

使用循环：

```bash
arr=()
while IFS= read -r line; do
    arr+=("$line")
done < file
```

### 第 39.4 节：将字符串行读入数组

```bash
var='line 1
line 2
line3'

readarray -t arr <<< "$var"
```

或者使用循环：

```bash
arr=()
while IFS= read line; do
    arr+=("$line")
done <<< "$var"
```

### 第 39.5 节：逐行循环字符串

```bash
var='line 1
line 2
line3'

while IFS= read -r line; do
    echo "$line"
done <<< "$var"
```

或者：

```bash
readarray -t arr <<< "$var"
for i in "${arr[@]}"; do
    echo "$i"
done
```

### 第 39.6 节：逐行循环命令输出

```bash
while IFS= read -r line; do
    echo "$line"
done <(ping google.com)
```

或者使用管道：

```bash
ping google.com | while IFS= read -r line; do
    echo "$line"
done
```

### 第 39.7 节：逐字段读取

假设文件中字段分隔符为 `:`

```bash
while IFS= read -d : -r field || [ -n "$field" ]; do
    echo "$field"
done < file
```

### 第 39.8 节：逐字段读取字符串

假设字段分隔符为 `:`

```bash
var='line 1:line 2:line3'
while IFS= read -d : -r field || [ -n "$field" ]; do
    echo "$field"
done <<< "$var"
```

### 第 39.9 节：将文件字段读入数组

假设字段分隔符为 `:`

```bash
arr=()
while IFS= read -d : -r field || [ -n "$field" ]; do
    arr+=("$field")
done < file
```

### 第 39.10 节：将字符串字段读入数组

假设字段分隔符为 `:`

```bash
var='1:2:3:4'
arr=()
while IFS= read -d : -r field || [ -n "$field" ]; do
    arr+=("$field")
done <<< "$var"
```

### 第 39.11 节：行和字段读取文件 (/etc/passwd)

在 unix 格式中，用户信息按行存储，每行由冒号分隔。在本示例中，逐行读取文件，行还使用冒号分隔为字段。

```bash
#!/bin/bash

FILENAME=/etc/passwd

while IFS=: read -r userid group; do
    echo "$userid, $group"
done < $FILENAME
```

**示例输入**

```
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
pulse:x:497:495:PulseAudio Daemon:/var/run/pulse:/sbin/nlogin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nlogin
tomcat:x:91:91:Apache Tomcat:/usr/share/tomcat6:/sbin/nlogin
webizer:x:67:67:Webalizer:/var/www/usage:/sbin/nlogin
```

**示例输出**

```
mysql, 27, MySQL Server /var/lib/mysql
pulse, 497, PulseAudio Daemon /var/run/pulse
sshd, 74, Privilege-separated SSH /var/empty/sshd
tomcat, 91, Apache Tomcat /usr/share/tomcat6
webizer, 67, Webalizer /var/www/usage
```

要逐行读取并将整行赋值给变量，以下是示例的修改版本。注意这里只有一个命名的变量。

```bash
#!/bin/bash

FILENAME=/etc/passwd

while IFS= read -r line; do
    echo "$line"
done < $FILENAME
```

**示例输入**

```
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
pulse:x:497:495:PulseAudio Daemon:/var/run/pulse:/sbin/nlogin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nlogin
tomcat:x:91:91:Apache Tomcat:/usr/share/tomcat6:/sbin/nlogin
webalizer:x:67:67:Webalizer:/var/www/usage:/sbin/nlogin
```

**示例输出**

```
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
pulse:x:497:495:PulseAudio Daemon:/var/run/pulse:/sbin/nlogin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nlogin
tomcat:x:91:91:Apache Tomcat:/usr/share/tomcat6:/sbin/nlogin
webalizer:x:67:67:Webalizer:/var/www/usage:/sbin/nlogin
```

## 第 40 章：文件执行顺序

`.bash_profile`, `.bash_login`, `.bashrc` 和 `.profile` 的作用几乎完全相同：设置和定义函数、变量等。

主要区别在于，`.bashrc` 在打开非登录但交互式的窗口时被调用，而 `.bash_profile` 和其他文件在登录 shell 时被调用。尽管如此，许多人也会让他们的 `.bash_profile` 或类似文件调用 `.bashrc`。

### 第 40.1 节：.profile vs .bash_profile (以及 .bash_login)

`.profile` 在大多数 shell 启动时被读取，包括 bash。然而，`.bash_profile` 用于特定 bash 的配置。对于通用初始化代码，请将其放在 `.profile` 中。如果是 bash 特有的，请使用 `.bash_profile`。

## 第 41 章：分割文件

有时，将一个文件分割成多个独立的文件是有用的。如果你有大文件，将其拆分成较小的块可能是一个好主意。

### 第 41.1 节：分割文件

运行不带任何选项的 `split` 命令会将文件分割为 1 或多个包含最多 1000 行的独立文件。

```bash
split file
```

这将创建名为 `xaa`、`xab`、`xac` 等的文件，每个文件包含最多 1000 行。如你所见，默认情况下所有文件的前缀都是 `x`。如果初始文件少于 1000 行，则只会创建一个这样的文件。

若要更改前缀，请在命令行末尾添加你所需的前缀：

```bash
split customprefix
```

现在将创建名为 `customprefixaa`、`customprefixab`、`customprefixac` 等的文件。

要指定每个文件的输出行数，请使用 `-l` 选项。以下命令将文件分割为最多 5000 行：

```bash
split -l 5000 file
```

或者

```bash
split --lines=5000 file
```

或者，你也可以指定最大字节数而不是行数。这通过使用 `-b` 或 `--bytes` 选项来实现。例如，允许最大 1MB：

```bash
split --bytes=1MB file
```

## 第 42 章：使用 scp 传输文件

### 第 42.1 节：scp 传输文件

要安全地传输文件到另一台机器——输入：

```bash
scp file1.txt tom@server2:$HOME
```

此示例演示了将 `file1.txt` 从我们的主机传输到 `server2` 用户 `tom` 的家目录。

### 第 42.2 节：scp 传输多个文件

`scp` 也可以用于将 `my_folder` 目录下所有扩展名为 `.txt` 文件从一个服务器传输到另一个服务器。在示例中，所有文件将传输到用户家目录。

```bash
scp /my_folder/*.txt tom@server2:$HOME
```

### 第 42.3 节：使用 scp 下载文件

要从远程服务器下载文件到本地机器——输入：

```bash
scp tom@server2:$HOME/file.txt /local/machine/path/
```

此示例显示了如何将用户 `tom` 家目录下的文件 `file.txt` 下载到我们本地机器的当前目录。

## 第 43 章：管道

### 第 43.1 节：使用 |

`|` 将第一个命令的标准输出和标准错误连接到第二个命令，而 `||` 仅将第一个命令的标准输出连接到第二个命令。

在示例中，页面通过 `curl` 下载，当带有 `-v` 选项时，`curl` 会向 `stderr` 写入一些信息，包括下载的页面被写入 `stdout`。页面标题位于 `<title>` 和 `</title>` 之间。

```bash
curl -vs `http://www.google.com/` | awk '/^Host:/{print}/<title>/{match($0,/<title>(.*)<\title>/,a);print a[1]}'
```

输出为：

```
> Host: www.google.com
Google
```

但使用 `|` 时会打印更多信息，即那些发送到 `stderr` 的信息，因为 `stdout` 被管道到了下一个命令。在示例中，除了最后一行（Google）外，所有内容都通过以下方式发送到了 `stderr`：

```
* Hostname NOT found in dns cache
* Trying 172.217.20.228...
* Connected to www.google.com (172.217.20.228) port 80 (#0)
> GET / HTTP/1.1
> User-Agent: curl/735.0
> Host: www.google.com
> Accept: */
* HTTP 1.0 close after body
< HTTP 200 OK
< Date: Sun, 24 Jul 2016 19:04:59 GMT
< Cache-Control: private, max-age=0
< Content-Type: text/html; charset=ISO-8859-1
< P3: CP(This is not a P3 policy!) See
https://www.google.com/support/accounts/151657?hl=en 获取更多信息。
> Server:
< XSS-Protection: 1; mode=block
< X-Frames: SAMEORIGIN
< Set-Cookie: ID-v8e2X0Y8ZLPLPEut73lkKNNeVUCcdgB9Ze_C030oIM-
EoG5QL0MTEAEg16651L1vRYTO00khq4ApFvYfWaoF-
AEI80088333D3508Aglnc33JnTRBQQelMcUs90qQA;expires=Mon, 23-Jan-2017 19:04:59 GMT;
path=/; domain=google.com; HttpOnly
< Accept-Ranges: none
< Vary: Accept-Encoding
< X-Cache: MISS from jetbis appliance
< X-Loop-Control: 5.202.190.187E4F9836653D50812995BA3992F8065
< Connection: close
<
```

```
{data not shown}
* Closing 0
Google
```

### 第 43.2 节：显示所有进程

在示例中，`ps` 会显示所有进程。

### 第 43.3 节：修改输出

在示例中，`|` 会修改 `stdout` 的内容。

## 第 44 章：单词拆分

```bash
bash: too many arguments
```

> `grep` 命令返回一个带有空格的多行字符串，所以你可以想象一下这里有多少个参数……

查看基础知识的查看、何时以及为什么。

### 第 44.1 节：单词拆分的用处

在某些情况下，单词拆分是非常有用的：

填充数组：

```bash
arr=$(grep -o '[0-9]\+' file)
```

> 这将把文件中找到的所有数值填充到 `arr` 中

遍历空格分隔的单词：

```bash
words='foo bar baz'
for w in $words; do
    echo "W: $w"
done
```

输出：

```
W: foo
W: bar
W: baz
```

传递不包含空白字符的空格分隔参数：

```bash
packs='apache2 php php-mbstring php-mysql'
sudo apt-get install $packs
```

或者

```bash
packs=
apache2
php
php-mbstring
php-mysql
sudo apt-get install $packs
```
