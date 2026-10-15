
# 自动化

## 第19章

当你看到以下内容时，可以认为你正处于正确的轨道上：

`abcoPqOPQ`
`FFPPab`

这就是依赖壳进行自动化的魅力之处：它很容易在交互和自动化之间切换，这塑造形成了一个强大的教学视角和对理解程度的检查。

列表 19.1 中的示例产品目录脚本是为 `sh` (Bourne) 处理编写的。我们强烈建议将其作为脚本的目标，而不是 `ksh`、`csh` 或 `bash`。我们倾向于将后者用于交互式命令行使用。然而，在自动化过程中，由于我们经常连接到不同类型的主机，可用性和隐晦的安全问题促使我们编写 `sh`——以及因此是所有壳——都能识别的构造结构。（默认的红帽 Linux 使用指向 `/bin/bash` 的链接 `/bin/sh`。）本章中的所有工作在编写时都确保无论你的主机的配置细节如何，脚本都能正常运行。在我们最初编写列表 19.1 中的脚本时，我们真的包含了那些以 `#` 开头的行吗？是的。我们已经将这种代码注释变成了一种习惯，这也是我们建议使用的习惯。如果你的生活和我们一样，电话会响，同事会离开，电源会故障；我们发现，在思考时就写下这些细节，比在中断后重新回忆这些想法要容易得多。在几天或几周后重新开始工作也会容易得多。为了人类可读性编写代码，在你将工作交给他人时会更加顺利。

列表 19.1 从第三行开始为变量 `DIR` 赋值。这种赋值是一种良好的做法，即使该变量（显然）只使用一次。它与自定义有关，并通常增强了可维护性；人们很容易查看脚本开头，立即看到外部环境中的哪些魔术词或配置（在本例中见第三行——`/particular/directory/for/my/client`）。

## 列表 19.2 继续

```bash
# 此实现对复杂的转义序列
# 处理并不良好。在现实世界中，这只是一个微小的问题。
######
```

```bash
usage() {
 echo \ 
"chstr BEFORE AFTER filenames"
 将 <filenames> 中每行出现的第一个 BEFORE 实例 替换为 AFTER，
 并报告差异。
示例:
chstr TX Texas */addresses.*
chstr ii counter2 *.c"
exit 0
}
```

```bash
case $1 in
 -h|-help) usage;
esac
```

```bash
if test $$ -lt 3
then
 usage
fi
```

```bash
TMPDIR=/tmp
# 同时运行多个 chstr 实例是没问题的。
# TMPFILE 名称对每个调用都是唯一的，因此不会
# 冲突。
TMPFILE=$TMPDIR/chstr.$
```

```bash
BEFORE=$1
AFTER=$2
# 将 BEFORE 和 AFTER 参数从参数列表中移除。
shift;shift
```

```bash
for FILE in *
do
 sed -e "s/$BEFORE/$AFTER/" $FILE >TMPFILE
 echo "$FILE:"
 diff $FILE $TMPFILE
 echo "*"
 mv $TMPFILE $FILE
done
```

上述 `chr` 脚本将其前两个参数分别作为要查找的字符串和要替换的字符串。在脚本中，它们对应于 `BEFORE` 和 `AFTER` 变量。两个 `shift` 命令将这些字符串从参数列表中移除，其余参数被视为文件。每个文件都通过 `sed` 处理，将 `$BEFORE` 替换为 `$AFTER` 并存放在临时文件中。然后将该文件移回原处。

大多数交互式编辑器都允许某种形式的全局搜索替换，有些甚至可以轻松处理多个文件。对于你的需求，这也许是一个更优越的自动化策略。如果不是，`chr` 是一个极简的命令行替代方案，使用起来极其简单。

> 注意
> 当然，经验丰富的 Perl 黑客会认为列表 19.2 稍微长了一点，因为通过命令行可以完成几乎相同的更改，例如：
>
> ```bash
> # perl -i.tmp -e s/before(after)/g file(s)
> ```

有关关于 Perl 的更多信息，请参阅系统中的 Perl 手册页。一个很好的起点是 `perltoc(1)`（目录）手册页。

## 示例：网页内容检索

经常出现的问题是如何自动化地从万维网检索页面。本节展示了许多技术中最简单的一种。

对于 HTTP 交互，让 `Lynx` 浏览器完成大部分工作。`Lynx` 对于除了最特殊用途以外的所有目的都足够了。你可以在 `http://lynx.browser.org` 获取最新版本。尽管大多数用户将 `Lynx` 视为交互式浏览器，但它也方便于将带有实时链接的最新头条副本发送到朋友的邮箱：

```bash
# lynx -source http://www.cnn.com | mail someone@somewhere.com
```

要创建一个原始的新闻更新服务，请编写以下脚本并在后台启动（使用符号 `&`）：

```bash
NEW=/tmp/news.new
OLD=/tmp/news.old
URL=http://www.cnn.com
while true
do
mv $NEW $OLD
lynx -dump -nolist $URL >NEW
diff $NEW $OLD
# 在开始下次比较之前等待十分钟。
sleep 60&
```

CNN 主页外观的任何变化将每 10 分钟出现在屏幕上。这种简单的方法比你最初预期的要不实用，因为 CNN 会定期打乱内容而不改变信息。然而，这是一个启发性的例子，你可以从这里开始编写你自己的脚本。

## 关于 Shell 编程的结语

Shell 是胶水；有一种方法可以从命令行访问应用程序来执行操作，几乎肯定有一种方法可以将其封装在 Shell 脚本中，让你对参数、验证和输入/输出重定向具有控制权。这些都是强大的技术，非常值得花几分钟时间学习和练习它们。

即使是微小的自动化也有回报。我们的个人准则是：每当我们预计在一个会话中两次使用某个序列时，就编写一个微小的单行脚本。例如，尽管我们有一套复杂的报告命令来分析万维网服务器日志，但我们也发现自己会费力编辑如 `/tmp/9` 这样的一次性脚本，以便对近期模式进行快速、临时的查询：

## 脚本回收

你可能会重用你编写的几乎每个脚本的部分。将它们保存在某个你以后可以查阅的地方（不要重复造轮子）。记住 `/tmp/9` 在每次重启后都会消失。

```bash
grep claird ls -t /usr/kern/log/* | head -1' | grep -v $1 | wc -l
```

此特定命令报告了在最新日志中包含 `claird` 字符串且排除 `/tmp/9` 第一个参数的页面请求数。

## 其他脚本语言：Expect、Perl 以及更多

你准备好超越 UNIX Shell 的限制了吗？有几种替代技术免费、易于安装、易于学习且更强大——也就是说，具有更丰富的功能和更有结构化的语法——相比于 `shell`。几个示例将说明它们能提供的内容。

### Expect

`Expect` 由 Don Libes 编写，是一种与许多不同程序协作的脚本语言，可以作为强大的软件自动化工具。为什么呢？`Expect` 预期交互，特别是涉及终端控制和时间延迟的交互。许多命令行应用程序有“不可脚本”的声名，因为它们涉及密码输入，并拒绝为了此目的重定向标准输入。`Expect` 的设计是为了解决自动化中的问题。在 Red Hat Linux 下，`Expect` 安装在 `/usr/bin` 下，你可以在它的手册页中找到文档。

创建一个包含列表 19.3 内容的脚本。

## 列表 19.3 `hold`：用 `Expect` 编写的“保持活动”

```expect
#!/usr/bin/expect

# 使用: hold HOST USER PASS。
# 操作: 以 USER 身份登录节点 HOST。为正常使用
# 提供 shell 提示符，同时每隔几秒在屏幕上打印单词 HELD，
# 以定期维持连接。
# 这对于测试和使用短超时 WAN（广域网）很有用。
# 你可以离开键盘，而不会因为超时丢失
# 连接。
# 警告：通过命令行传递密码的安全风险使得
# 此示例仅供说明。请根据特定的安全情况进行适当修改。

set hostname [lindex 0]
set username [lindex 1]
set password [lindex 2]

# 如果不同的主机没有设置用户名提示，则会出现问题。
set prompt_sequence ""

spawn telnet $hostname
expect "login: "
send "$username\r"
expect "Password:\r"
send "$password\r"
```

## 列表 19.3 继续

```expect
# 注意使用全局 [gl] 模式匹配来解析
# 通配符。
expect -gl 'TERM = (*)'
send \r
expect $prompt_sequence
```
