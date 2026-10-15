

## Listing 9-4: 使用 time 工具运行 checkLinks 脚本以了解其耗时

注意，在一个耗时的命令前加上 time 调用是一个明智的做法，可以看到运行脚本花费了多长时间。在这里可以看到，检查 http://www.daveonfilm.com/ 上的全部 982 个页面花费了 50 分钟的实际时间，而实际处理时间仅为 42 秒。这可不少！

## Hacking the Script

数据文件 traverse.dat 包含遇到的所有 URL 列表，而 reject.dat 则是遇到但未检查的所有 URL 列表，通常是因为它们是外部链接。我们将在下一个脚本中处理这些。实际的错误可以在 Listing 9-1 中的 traverse.errors 文件中找到。

要让此脚本报告图像引用错误，请使用 grep 在 traverse.errors 文件中查找以 .gif、.jpg 或 .png 为后缀的文件名，然后再将结果输入到 sed 语句中（该语句只是清理输出以使其美观）。

## 70 Reporting Broken External Links

此伴随脚本（Listing 9-5）基于脚本 #69 的输出构建，用于识别从分析的站点或站点子目录中引用的所有外部链接，并测试每个链接以确保没有“404 Not Found”错误。为了方便，它假定之前的脚本刚刚运行过，因此可以利用 rejects 文件获取 URL 列表。

## The Code

```
#!/bin/bash

# checkexternal--Tests all URLs on a website to build a list of external
# references, then check each one to ascertain which might be dead or
# otherwise broken. The -a flag forces the script to list all matches,
# whether they're accessible or not; by default, only unreachable links
# are shown.

listall=0; errors=0; checked=0

if [ "$1" = "-a" ] ; then
  listall=1; shift
fi

if [ -z "$1" ] ; then
  echo "Usage: $(basename $0) [-a] URL" >&2
  exit 1
fi
```

```
trap "$(which rm) -f traverse*.errors reject*.dat traverse*.dat" 0

outfile="$(echo "$1" | cut -d/ -f3).errors.ext"
URLlist="$(echo $1 | cut -d/ -f3 | sed 's/\\/\\//').rejects"

rm -f $outfile   # Ready for new output

if [ ! -e "$URLlist" ] ; then
  echo "File $URLlist not found. Please run checklinks first." >&2
  exit 1
fi

if [ ! -s "$URLlist" ] ; then
  echo "There don’t appear to be any external links ($URLlist is empty)." >&2
  exit 1
fi

#### Now, finally, we’re ready to begin...

for URL in $(cat $URLlist | sort | uniq)
do
  curl -s "$URL" > /dev/null 2>&1; return=$?
  if [ $return -eq 0 ] ; then
    if [ $listall -eq 1 ] ; then
      echo "$URL is fine."
    fi
  else
    echo "$URL fails with error code $return"
    errors=$(($errors + 1))
  fi
  checked=$(($checked + 1))
done

echo ""
echo "Done. Checked $checked URLs and found $errors errors."
exit 0
```

Listing 9-5: The checkexternal script

## How It Works

这本书中这并不是最优雅的脚本。它更像是一种暴力检查外部链接的方法。对于找到的每个外部链接，curl 命令通过尝试抓取其 URL 的内容然后立即丢弃，测试链接的有效性，代码块在 ① 处完成

这里值得一提的是 2>&1 的记法：它会导致输出设备 #2 被重定向到输出设备 #1 当前设置的目标。在 shell 中，输出 #2 是 stderr（错误信息），输出 #1 是 stdout（常规输出）。单独使用时，2>&1 会导致 stderr 转到 stdout。然而在此实例中，注意

在此重定向之前，stdout 已经重定向到 /dev/null。这是一个虚拟设备，可以被喂入无限量的数据而永远不会变大。把它想象成一个黑洞，你就走对了方向。因此，此记法确保 stderr 也被重定向到 /dev/null。我们丢弃这些信息，因为我们真正关心的只是 curl 从此命令返回零还是非零的返回码。零表示成功；非零表示错误。

遍历的内部页面数量只是文件 traverse.dat 的行数，外部链接的数量可以通过查看 reject.dat 找到。如果指定了 -a 标志，输出会列出所有外部链接，无论是否可达。否则，只显示失败的 URL。

## Running the Script

要运行此脚本，只需将要检查的站点的 URL 指定为脚本的参数即可。

## The Results

让我们检查 http://intuitive.com/ 是否存在坏链接，如 Listing 9-6 所示。

```
$ checkexternal -a http://intuitive.com/
http://chemgod.slp.umd.edu/~kidwell/weather.html fails with error code 6
http://epoch.oreilly.com/shop/cart.asp fails with error code 7
http://e-zone.org/1080ez/ fails with error code 7
http://fx.crewtags.com/blog/ fails with error code 6
http://linc.homeunix.org:8080/reviews/wicked.html fails with error code 6
http://links.browser.org/ fails with error code 6
http://nell.boulder.lib.co.us/ fails with error code 6
http://rpms.arvin.dk/slocate fails with error code 6
http://rss.intuitive.com/ fails with error code 6
http://techweb.cmp.com/cw/webcommerce fails with error code 6
http://tenbrooks11.laminds.com/ fails with error code 6
http://www.101publicrelations.com/blog/ fails with error code 6
http://www.badlink/somewhere.html fails with error code 6
http://www.bloghop.com/ fails with error code 6
http://www.bloghop.com/ratemyblog.htm fails with error code 6
http://www.bloghiles.com/web ring.shtml fails with error code 56
http://www.blogstreet.com/blogs/qbin/home.cgi fails with error code 56
http://www.builder.cnet.com/ fails with error code 6
http://www.buzz.builder.com/ fails with error code 6
http://www.chem.emory.edu/html/html.html fails with error code 6
http://www.cogsci.princeton.edu/~wn/ fails with error code 6
http://www.ourecopass.org/ fails with error code 6
http://www.portfolio.intuitive.com/portfolio/ fails with error code 6

Done. Checked 156 URLs and found 23 errors.
```

Listing 9-6: Running the checkexternal script on http://intuitive.com/

看起来是时候做一些清理工作了！

