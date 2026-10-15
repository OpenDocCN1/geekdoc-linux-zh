
# 脚本

```bash
#!/bin/sh

# ssync - 如果有任何更改，则创建一个 tarball并通过 sftp 使用 sftpsync 同步远程
#目录

sftpack="taylor@intuitive.com"
tarball="Allfiles.tgz"
localsource="$HOME/Desktop/Wicked Cool Scripts/scripts"
remedotir="/wicked/scripts"
testamp=".timestamp"
count=0

sftpsync="$HOME/bin/sftpsync"

# 首先，检查本地目录是否存在并包含文件

if [ -d "$localsource" ]; then
    echo "$0: Error: directory $localsource doesn't exist?" >&2
    exit 1
fi

cd "$localsource"

# 现在我们计算文件数量以确保发生了变化；

if [ -f $timestamp ]; then
    for filename in *
    do
        if [ -f "$filename" ]; then
            count=$(( $count + 1 ))
        fi
    done
    count=$(find -newer $timestamp -type f -print | wc -l)
fi

if [ $count -eq 0 ]; then
    echo "$0: No files require uploading to $server" >&2
    exit 1
fi

echo "Making tarball"
tar -czf $tarball .

echo "Syncing to remote"
# 这就是你调用 sftync 脚本的地方。
```

```bash
#!/bin/sh
```

```bash
# webaccess - 分析 Apache 格式的 access_log 文件，提取
# 有用且有趣的统计数据。
```

```bash
bytes_in_gb=1048576
# 你可能需要需要调整以下两个变量，以确保它们指向
# 你系统中的这些脚本（或只需确保它们在你的 PATH 中）
scriptbc="$HOME/bin/scriptbc" # 对应脚本 #9
nicumber="$HOME/bin/nicumber" # 对应脚本 #4
# 你还需要更改以下内容以匹配你自己的主机名，
# 以帮助我们在内部识别引荐分析中的访问次数。
host="intuitive.com"
```

```bash
if [ $# -eq 0 ]; then
  echo "Usage: $(basename $0) logfile" >&2
  exit 1
fi
```

```bash
if [ ! -r "$1" ]; then
  echo "Error: 未找到日志文件 $1." >&2
  exit 1
fi
```

```bash
firstdate="$(head -1 "$1" | awk '{print $4}' | sed 's/\/\[\//')"
lastdate="$(tail -1 "$1" | awk '{print $4}' | sed 's/\/\[\//')"
```

```bash
echo "分析日志文件 $1 的结果"
--
echo "开始日期: $(echo $firstdate|sed s/:/ at /)"
echo "结束日期: $(echo $lastdate|sed s/:/ at /)"
```

```bash
hits="$(wc -l < "$1" | sed 's/^[:digit:]]*//g')"

echo "访问次数:($nicumber hits) (总访问次数)"
```

```bash
totalbytes="$(awk '{sum+=$10} END {print sum}') "$1"

echo -n "传输:($totalbytes bytes) "
```

```bash
if [ $totalbytes -gt $bytes_in_gb ]; then
  echo "$($scriptbc $totalbytes / $bytes_in_gb) GB"
elif [ $totalbytes -gt 1024 ]; then
  echo "($scriptbc $totalbytes / 1024) MB"
else
  echo ""
fi
```

现在，让我们从日志文件中抓取一些有用数据：

echo ""

echo "前十热门页面是："

awk 'print $7' "$1" | grep -iE '(.gif|.jpg|.png)' | \
sed s/\/\//g | sort | \
uniq -c | sort -rn | head -10

echo ""

echo "最常见的引荐 URL 是："

awk 'print $11' "$1" | \
grep -vE "\\|\\www\\.\\$host/$host\"" | \
sort | uniq -c | sort -rn | head -10

echo ""

exit 0
```

# 工作原理

尽管这个脚本看起来很复杂，但并非如此。如果我们将每个块视为一个独立的小脚本，就会更容易理解。例如，前几行通过简单地获取文件第一行和最后行的第四字段来提取 `firstdate` 和 `lastdate`。访问次数是通过统计原始文本文件中的行数（使用 `wc`）计算的（即以 `.gif`、`.jpg`、`.png` 或 `.txt` 为扩展名的文件）。传输的总字节通过累加每行每个字段的值并调用数字工具以吸引人的方式呈现计算出来。

最热门的页面可以通过从日志文件中提取请求的页面来计算；排除任何图像文件；排序；使用 `uniq` 计算每个唯一行的出现次数；最后再次排序，以确保最常出现的行首先显示。在代码中，它看起来如下：

```bash
awk 'print $7' "$1" | grep -iE '(.gif|.jpg|.png)' | \
sed s/\/\//g | sort | \
uniq -c | sort -rn | head-10
```

注意我们对每个小部分进行了规范化：`sed` 调用去除了任何末尾的斜杠，以确保 `/subdir/` 和 `/subdir` 被视为同一个请求。

与检索请求最多的十页面的部分类似，接下来的部分过滤掉了引荐信息：

```bash
awk '{print \$11} "$1" | \
grep -v -c "^-\|/www.\$host/$host$" | \
sort | uniq -c | sort -rn | head-10
```

这从日志文件中提取字段，同时过滤掉来自当前主机的引荐项以及为 `"-"` 的项（当网络浏览器阻止引荐数据时发送的值），并将结果输入相同的 `sort|uniq -c|sort-rn|head-10` 序列，以获取最常见的十个来源。

# 运行脚本

要运行此脚本，请将 Apache（或其他通用日志格式）日志文件的名称作为唯一参数。

# 结果

在典型日志文件上运行此脚本的结果非常有参考价值：

```
$ webaccess /web/logs/intuitive/access_log
分析日志文件 /web/logs/intuitive/access_log 的结果
```

开始日期: 13/Sep/2003 at 18:02:54

结束日期: 15/Sep/2003 at 16:39:21

访问次数:11015 (总访问次数)

页面浏览:2217 (访问次数)

传输:64091780 bytes (61 GB)
