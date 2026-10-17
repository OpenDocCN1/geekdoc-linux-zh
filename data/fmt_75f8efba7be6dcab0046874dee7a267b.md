
```awk
BEGIN { pageno = 0;
  pageno = print_header(pageno);
  printf("the page number is now %d\n", pageno);
}

# 报告的生成代码在这里
END { close("report.txt");
  system("lpr -Pprinter report.txt");
}

function print_header(page) {
  page++;
  printf("this is the header for page %d\n", page) > "report.txt";
  printf("this is a second line of the header\n") > "report.txt";
}
```

这是第 1 页的标题

这是标题的第二行

现在的页码是 0

输出与 26.6 相同，不同之处输出显示在打印机而不是屏幕上。

# 总结

本章介绍了 `awk` 语言——`awk`，这是一种强大且实用的语言，它让你能够搜索数据、即时执行命令，甚至创建报告。在你完成这些之后，当你意识到自己懒得输入一个机器应该知道的数字，或者不耐烦等到午夜才开始备份时，当你对自己的创造力足够的信心去教机器更好的方法时，技术细节就会迎刃而解。

> 注意
>
> 如果你想尝试使用 `awk`-转-`C`，可以尝试 Eric S. Raymond 的程序。虽然它不支持 `awk` 的所有功能，但你可能会发现它有用且有趣。

# 自动化任务 第 27 章 635

```bash
# BASE 将拥有值 (137-13p, 201-942f, ...)
BASE=$(basename "$F" .jpg) 
# 我遇到的唯一后缀是 'p' 和 'f'，所以我将
# 简单地转换这两个。
# PRODUCT 的示例值：{137-13P, 201-942f, ...}
PRODUCT=$(echo $BASE | tr pf F)
# one_command 是一个将行 SQL 传递给数据库管理系统的 shell 脚本
one_command update catalog set Picture = '$DIR/$BASE.jpg' \ continuouswhere Product = '$PRODUCT'
done
```

事实证明，团队在几天后决定图片需要放在不同的目录中，因此只需几秒钟就能更新脚本的倒数第二行并添加一条注释，例如：

```bash
# “不要”在 Picture 中包含目录指定；这 
# 只有在检索数据时才会知道。
one_command update catalog set Picture = '$BASE.jpg' where Product = '$PRODUCT'
done
```

然后重新运行。不可避免的是，总有一天我们将向数据库添加更多图片，或者想要关于孤立图片（那些尚未连接到任何产品的图片）的报告，此时这个脚本或其密切的派生版本将再次发挥作用。

# 实现分析

让我们详细分析列表 27.1 中的示例，以练习自动化思维。

你理解列表 27.1 中的 shell 脚本是如何运行的吗？第 25 章“Shell 编程”解释了 shell 处理，附录 B“重要的 Linux 命令和 Shell 算符”介绍了你可能需要的、关于最常用 UNIX 实用程序的所有内容。你可以通过阅读相应的 `man` 页（帮助文档）或网上现有的任何关于 shell 编程的好书来学习更多知识。当然，最可靠的方法是自己进行实验。例如，如果你对 `tr` 的“...translation...”含义有任何疑问，实验是很容易的，比如：

```bash
tr pf PF <<HERE
abcopopQQ
FfpPab
HERE
```

当你看到以下内容时，就知道你正处于正确的道路上：

```
abcPqQOPQ
FFPPab
```

这就是依赖 shell 进行自动化的魅力之一；很容易在交互和自动化之间切换，这塑造了一个强大的教学视角并作为对理解的检查。

列表 27.1 中的示例产品目录脚本是为 `sh` 处理编写的。我强烈建议将其作为你的 shell 目标，而不是 `ksh`、`csh` 或 `bash`。我更倾向于将后者任何一种用于交互式、命令行使用。然而，在自动化过程中，由于我经常连接到不使用 Red Hat Linux 的主机，可用性和某些晦涩的安全问题迫使我使用 `sh` 编写代码结构，因此所有的 shell 都能识别。默认的 Red Hat 安装将 `/bin/sh` 链接到 `/bin/bash`。本章中的所有工作都编写得当无论你主机的配置细节如何，都能正常运行。第 25 章提供了更多关于 shell 之间差异的细节。

当我第一次编写列表 27.1 中的脚本时，我包含行内注释（以 `#` 开头的行）吗？是的。我已经将这种程度的源代码文档工作变成了一种习惯，我也向你推荐这样做。如果你的生活像我一样，电话响不断、同事打扰、电源故障；我发现自己在思考时把这些细节记录下来比较容易，而不是在受到中断后重新回忆我的想法。此外，在几天或几周后重新开始工作容易得多。为了人类的可读性而编写代码也可以在你将工作交给他人时减轻过渡。

列表 27.1 从第一行开始分配 shell 变量 `DIR`。我强烈建议将这种赋值养成良好的习惯，即使变量只使用一次。这有助于自文档化并通常能增强可维护性；在脚本顶部可以看到。

许多你想要完成的任务都涉及处理。像其他实用程序一样，你需要输入标准输入。如果你对 `tr` 的“...translation...”含义有任何疑问，实验是很容易的，比如标准输入：

```bash
tr pf PF <<HERE
abcopopQQ
FfpPab
HERE
```

当你看到以下内容时，就知道你处于正确的道路上：

```
abcPqQOPQ
FFPPab
```

这就是依赖 shell 进行自动化的魅力之一；很容易在交互和自动化之间切换，这塑造了一个强大的教学视角并作为对理解的检查。

# 自动化、编程与系统修改

# 提高自动化技巧的技巧

你对自己的职业负责。除了本章建议的所有内容，如果你这样做将走得更远：

- 提高你的自动化技术。
- 阅读工具的文档。

# 持续教育

提高自动化技能有很多重要方法，无论你是使用 Perl、Expect 还是其他机制：

- 扫描文档。
- 阅读良好的脚本。
- 编写脚本。

文档有枯燥和难读的声誉。学会如何享受它很重要。这里介绍的所有工具都有 `man` 页，你需要熟练使用它们。阅读这些文档并反复阅读。工具的作者面临过你面临的挑战。通常，通过阅读选项或关键词列表，你会发现某些功能适用于你的情况。带着这种心态学习文档；寻找你可以使用的想法。特别关注那些你不认识的命令。如果其中任何一个——比如 `cu` 或 `od`——大部分已经过时，你会在阅读其他命令（如 `tput`、`limit`、`bc`、`nice` 或 `wait`）时意识到，早期的用户面临着与你相同的情况。站在他们的肩膀上看得更远。

> 注意
>
> 想了解更多关于某个命令的信息？除了 `man` 页之外，还有其他两个信息来源吗？Red Hat Linux 用户还应该检查 `/usr/doc` 目录，那里超过 230 个程序有额外的信息目录。如果 `man` 页表明该程序是 GNU 软件发行版的一部分，你还可以找到关于该命令更详细的信息。按这样使用 `info` 命令：`info <command>`。

阅读良好的编程很重要。有志的文学作家从普希金和普丁中寻找灵感，而不是从语法老师；同样，当你阅读优秀程序员的作品时，你将走得更远。关注计算机杂志的专栏，最重要的是开源软件存档。良好的代码示例偶尔出现在 Usenetor中。珍惜这些；阅读它们并向大师们学习。

# 自动化任务

## 第 27 章

本章中的所有示例都设计得易于使用。它们通常只完整地完成一个微小任务；这是演示新概念的最佳方法之一。异常处理（特别是参数验证）很重要，但它超出了本章的范围。

通过编写你自己的脚本来巩固你的学习。当你通过自己的经验将知识落实后，你所读的所有文档都会变得更有意义。

# 良好的工程实践

对于追求自动化的人来说，最重要的建议是实践良好的工程方法。这始终始于一个清晰且定义良好的目标。自动化并不是绝对的好事；它只是实现人类目标的方法。在学习本章的过程中，你将学到多程度上需要自动化，以及哪些地方不需要。

一旦设定了目标，尽可能使用已经编写好的组件来接近它。使用小型、易于理解的脚本模块将现有程序“粘合”在一起。选择有意义的变量名。仔细定义接口。编写注释。

# Shell 脚本

虽然第 25 章涵盖了 shell 编程的基本语法和语言，但让我们来看几个在日常操作中经常有用的脚本示例。

# chstr

维护源代码、客户列表和其他记录的用户通常想要从命令行启动查找并替换操作。在 UNIX 主机上有一个 `chstr` 的变体是有用的。列表 27.2 提供了一个示例。

列表 27.2 `chstr`——简单的查找与替换操作

```
######
# 更多细节请参见下文的 usage() 定义。
# 此实现对复杂的转义序列处理不佳。
# 在现实世界中，这只是一个微小的问题。
######
usage() (
  echo \
```

# 自动化、编程与系统修改

第四部分

# 列表 27.2 继续

```
'chstr BEFORE AFTER <filenames>
将 <filenames> 中每行的第一个第一个 BEFORE 实例替换为 AFTER，
并报告差异。
示例：
chstr TX Texas */addresses.*
chstr ii counter2 *.c"
exit 0

case $1 in
-h| -help) usage;
esac
```

```

if test $# -lt 3
then
  usage
fi

TMPDIR=/tmp
# 同时运行多个一个 chstr 实例是没问题的。
# TMPFILE 名称对于每次调用都是特定的，所以
# 没有冲突。
TMPFILE=$TMPDIR/chstr.$$
```

```
BEFORE=$1
AFTER=$2

# 从参数列表中移除 BEFORE 和 AFTER 参数。
shift;shift

for FILE in $*
do
  sed -e "s/$BEFORE/$AFTER/" $FILE >TMPFILE
  echo "$FILE"
  diff $FILE $TMPFILE
  echo ""
  mv $TMPFILE $FILE
done
done (等等，原文写的是 "done")
```

大多数交互式编辑器都执行某种形式的全局查找-替换，有些甚至可以方便地操作多个文件。也许这对于你的需求来说是更优的自动化。如果不是，`chstr` 是一个使用极其简单的最小命令行替代方案。

# WWW 检索

经常出现的问题是，在许多从万网检索网页的技术中，哪种是最简单的。本节展示了许多技术。

# FTP 检索

创建一个 shell 脚本 `retrieve_one`，内容见列表 27.3，并启用执行权限（即命令 `chmod +x retrieve_one`）。

- 列表 27.3 `retrieve_one`——自动化 FTP 检索

```
# 用法："retrieve_one HOST:FILE" 使用匿名 FTP 连接
# 到 HOST并将 FILE 检索到本地目录。

MY_account=account@myhost
HOST=$(echo $1 | sed -e "s/.*://"
FILE=$(echo $2 | sed -e "s/.*://"
LOCAL_FILE=$(basename $FILE)

ftp -v -n $HOST << SCRIPT
user anonymous $MY_ACCOUNT
get $FILE $LOCAL_FILE
quit
```

`retrieve_one` 可用于将 FAQ 的当前副本下载到本地目录等目的；通过运行以下请求开始尝试：

# `retrieve_one rtfm.mit.edu:/pub/usenet-faq/hierarchy/comp/os/linux/answers/linux/faq/part1`

# HTTP 检索

对于 HTTP 交互，让 Lynx 浏览器完成大部分工作。红帽发行版自带的 Lynx 浏览器足以满足所有最专门的。在这些情况下，从 http://www.crl.com/~subir/linux/bin 获取最新版本的 Lynx 二进制执行文件和简单的安装说明。尽管大多数 Lynx 用户将 Lynx 认为一种交互式浏览器，但它也方便将带有实时链接的最新标题副本拖到朋友的邮箱中：

```
# lynx -source http://www.cnn.com | mail someone@somewhere.com
```

创建一个原始的新闻更新服务脚本：

```
NEW=/tmp/news.new
OLD=/tmp/news.old
URL=http://www.cnn.com
while true
  mv $NEW $OLD
  lynx -dump -nolockfile $URL > $NEW
  sleep 60
done
```

# 自动化、编程与系统修改

 第四部分

接下来，使用命令：

```bash
# crontab /tmp/entry
```

结果是每天早上 2:00，cron 都会启动搜索转储的任务并在完成后将结果通过电子邮件发送给你。这非常有用，因为 Linux 在某些错误条件下会创建文件。这些核心镜像（core images）体积很大，很容易占据磁盘上惊人的空间。通过前面的操作序列，你每天早上都会在邮箱中收到一份报告，准确列出那些可能对你毫无用处的文件位置和大小。

# 用户空间

假设你进行了一些实验，并累积了一系列用于监控系统健康的 cron 任务。现在，除了其他任务外，你希望系统在每个周一早上 2:10 告诉你哪些最大的主目录树（/home/*）。首先，输入：

```bash
# crontab -1 /tmp/entries
```

以捕获你调度的所有任务，并在 /tmp/entries 的末尾添加这一行：

```bash
10 2 * * du /home/* | sort -nr | head -10
```

执行请求：

```bash
# crontab /tmp/entries
```

cron 就会向你发送你所需要的报告。

# at：调度未来事件

假设你撰写一份关于物质世界循环的周刊专栏，并通过电子邮件发送。为了简化涉及金融市场的法律影响，你特意要求在周五下午 5:00 发送。现在是周三，你已经完成了分析，并且快要为今晚开始的假期收拾好行李了。你如何对你的订阅者负责呢？只需要三行脚本：

```bash
# at 17:00 Friday << COMMAND
mail -s 'This week's CYCLES report.' mailing_list <
analysis.already_written
COMMAND
```

这会调度 `mail` 命令在稍后处理。你可以注销会话，你的 Linux 主机仍会按照指令在周五 17:00 发送邮件。事实上，你可以在下达命令后关闭机器，只要它能及时重启，你的定时任务仍会按照你设定的计划启动。

# 其他机制：Expect、Perl 及更多

你准备好超越 UNIX shell 的限制了吗？有几种替代技术是免费、易安装、易学的，并且比 shell 更强大——也就是说，它们拥有更丰富的功能和更结构化的语法。几个示例可以说明它们能提供什么。

# 技术比较

我经常被问及比较不同的自动化技术；作为对读者的服务，我启动了 http://starbase.neoft.com/-claid/comp.lang.misc/portable_scripting.html 页面，回答了关于在不同脚本语言之间进行选择的问题。最重要的原则如下：

- 选择一种你的朋友（熟人、同事、通信伙伴等）正在使用的语言。
- 选择一种你觉得感觉良好的语言。

在极少数例外，不同语言的能力足够接近，社交和心理因素占据了主导地位。

# Expect

根据 *Expect*（其标准参考书）封底上的一个用户证言，“Expect 是系统管理员及许多其他人的必备工具”。为什么呢？Expect 自动化了交互，特别是那些涉及终端控制和时间延迟的交互，这是其他工具未曾尝试过的。命令行应用程序因其不可脚本化而闻名，因为它们涉及密码输入，并拒绝为了此目的重定向标准输入。然而，这对 Expect 来说不是问题。在安装 Expect (http://starbase.neoft.com/-claid/comp.lang.tl/expect.html) 后，创建一个包含列表 27.4 内容的脚本。

列表 27.4 `hold`——用 Expect 编写的“保持活跃”
