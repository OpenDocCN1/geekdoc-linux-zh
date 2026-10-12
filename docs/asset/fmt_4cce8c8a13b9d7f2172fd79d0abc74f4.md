
```bash
bb@nandy:$$ diffoscope --list debian ../draft1/../draft2/
../draft1/
../draft2/
file list
ls -ld *
ls -ldR *
draft1.odt
draft2.odt
stat ()
Size: 4096 Blocks: 8 ID Block: 4096 directory
Links: 
Access: (0755)/drwxr-xr-x) UID: (1000/ bb) Gid: (1000/ bb)
Modify: 2020-08-20 19:54:16.000000000 -0000
Modify: 2020-08-20 19:54:25.171105000 -0000
Birth:
```

`bb@nandy:$$ diffoscope --list debian`

External-Tools-Required: `Rscript`, `aboorting`, `uptool`, `bdtay`, `brip2`, `bfstool`, `cd-ircdump`, `cmp`, `c`

`bquare`, `dwm`, `diffutils`, `patch`, `enjarify`, `ftdump`, `ffprobe`, `gettextl`, `hf`, `hbc`, `gif`

`build`, `gpg`, `gzip`, `identify`, `img2txt`, `isoinfo`, `isojavo`, `js-beautify`, `lipo`, `llvm-analyzer`, `llvm-di`

`s`, `lsatric`, `myperl`, `node`, `perl`, `python`, `python3-gettext`

`pedump`, `ppgdump`, `ppudump`, `procyon`, `ps2asclii`, `readelf`, `showfmt`, `sg`, `sqlite3`, `ssconvert`, `ssh-ke`

`vi`, `xxdtar`, `zip`

Available-in-packages: `aboorting`, `acl`, `aoptool`, `brip2`, `builtin-multiuarch`, `c-utils`, `col`

`dev`, `devscripts`, `decompress`, `dectify`, `diffutils`, `dpatch`, `file`, `file-lists`, `gzip`, `git`, `hex`

`ffutils`, `docxt2`, `e2fsprog`, `enjarify`, `ffmpeg`, `forge-extras`, `fp-utils`, `genoisimage`, `gettext`

`hint`, `info`, `libz4`, `libz4-tool`, `mono-utils`, `mntools`, `mono-utils`, `ocaml-nox`, `odt2txt`, `oggvideotools`, `openssh-client`, `gp`

`pdump`, `popper-utils`, `procyon-compiler`, `r-base-core`, `sng`, `sqlite3`, `squash-utils`, `tcpdump`, `un`

`rip`, `emboss`, `xid`, `vim-common`, `xr-utils`, `zip`

# 深度

命令行 – `diffscope`

所需或仅推荐的依赖。所有三个选项都列出了实现完整功能所需的包。

取决于你如何使用 `diffscope`，它可能在没有所有列出的包的情况下运行（图 3）。

## 进行中的工作

在我写下这些内容时，`diffoscope` 仍在快速开发中。因此，某些功能仍然缺失。与 `diff` 不同，`diffscope` 尚未支持双列视图，这是一个让比较变得非常方便的功能。

图 2：Diffscope 还可以比较目录的内容和结构。

此外，虽然支持的格式列表已经令人印象深刻，但如果能支持 `GLOB_PATTERN` 和 `--exclude-command` 就完美了。使用 `--max-diff-input-lines LINES` 来比较行数（最大行数的选项相同，可以与 `im` 配合使用，为 4,194,304）。你也可以设置清晰的。然而，似乎 `diffos` 不同的文件或目录。由于 `work-scope` 的范围已迅速扩展到其最初的目的。特别是在与目录配合时，你可以设置 `--max-diff-block-lines-saved LINES` 来决定权限和其他文件属性是否与 `--exclude-direc-` 使用。作为一名作者，我很高兴发现 `diffo` 非常适合比较。

## 信息选项

对于那些不从发行版安装的人，在编写虚构或长篇非虚构作品时，`diffoscope` 包含了 `--list-tools` 自动，是，或递归。此外，你可以选择启用 `DISTRO`，它列出了 `--list-missing-tools` 依赖，以及模糊逻辑，控制如何处理微小差异。设置为 0 意味着所有匹配必须精确；在使用几周后，我已经在想没有它之前我是怎么用过的。它已经成为我系统上不可或缺的工具。不过，你可以感受到我每天使用并已经依赖的某些发行版的默认设置的含义。Q Q Q 60 或 400 的最大值必须通过尝试来发现，因为目前还没有文档说明。到 `diffoscope` 的某些选项。在两个命令中，发行版必须指定为 `Arch`、`Debian` 或 `FreeBSD`。对于 `Debian`，`op-itself` 设置行数到。

## 信息

`[1]` `diffoscope`: `https://diffoscope.org/`

`[2]` `Reproducible Builds`: `https://wiki.reproducible-builds.org/`

图 3：对于从零构建 `diffscope` 的人，该命令包含了实现完整功能所需的包列表。

Q Q Q

32

2020年11月

第 240 期

`LINUX-MAGAZINE.COM` | `LINUXPROMAGAZINE.COM`

## 带有数字存档的书架

通过我们的数字版完成你的 Linux Magazine 和 Security Collections。获取一整年的 PDF 格式期刊，可在任何设备上访问。

2019 存档现已上线！

`/2019-Archives`

(`img/d147ca893bd12a47e8f50b16_181.png`)

(`img/d147ca893bd12a47e8f50b16_182.png`)

## 开放数据

#

## 使用开放数据绘制疫情图

## 可视化

大量的 `COVID-19` 数据可以通过在线 API 获取。通过一些技巧和源工具，你可以自己提取并分析数据。

```
curl https://covidapi.info/api/v1/Ucountry/USA/2020-06-15

{
"count": 1,
"result": {
"confirmed": 211426,
"deaths": 11627,
"recovered": 576334
}
"confirmed": 1,
"deaths": 11627,
"recovered": 576334
}
```

脚本中一个可能不太明显是我如何计算日期的。当你第一次运行脚本时，你会得到所有数据，以及数据集中的每一天。然而，在解析特定的日期时我遇到了问题。

```bash
DATE= `date --date="12:00 today U`

-$IDX" + %Y-%m-%d`
```

新数据。

由于日期中包含了连字符。作为一种替代方案，我选择编写了一个小的 `Bash` 脚本来按州获取数据，即检索整个国家的 `COVID-19` 数据。`date` 命令从当前日期记录的计数中减去给定的天数，然后遍历日期列表以检索，并将输出格式化为 `YYYY-MM-DD` 字符串。这对于比较不同国家之间的数据很有用，但如果你想了解当地发生的情况，这种方法就作用有限。

当然，如果我只想查看某部分数据，每次都下载数百天的真实数据将是低效的。大多数步骤都是本地执行的。如果你熟悉 `Bash`，`[Tracking Project](5]` 项目提供了提供了每天的 `COVID-19` 信息。

## 列表 1: covid19.sh

```bash
#!/bin/bash

get_count()
{
  GATHERCOUNTRY=$1
  positive=0
  hospitalized=0
  deaths=0

  # 获取自开始以来的天数
  CNT=`curl https://covidapi.info/api/v1/country/$GATHERCOUNTRY 2>/dev/null | jq 'count'`

  positive=`echo $SINGLE | jq ".positive"`

  deaths=`echo $SINGLE | jq ".death"`

  hospitalized=`echo $SINGLE | jq ".hospitalizedCurrently"`
}

gather_state()
{
  GATHERSTATE=$1
  if [ $positive == "null" ]; then positive=0; fi 
  if [ $deaths == "null" ]; then deaths=0; fi
```
