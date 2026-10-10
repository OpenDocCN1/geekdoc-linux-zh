
因为页眉必须是免费。仅仅依靠 LPD 生成的每一页来确定用户和主机是不够的。有关打印机统计的更多信息，请参阅“统计使用”。

`echo "Usage: 'basename $0' <user> <host> <job> 1>&2`

`fi`

# 保存这些内容，主要为了在下方的 PostScript 中可读性。

```
user=$1
host=$2
job=$3
date=`date`
```

# 将 PostScript 代码发送到标准输出。

```
exec cat <<EOF
%PS
EOF
```

# 确保我们不会干扰用户接下来的作业

```
save
```

# 在纸张边缘画一个粗粗且难看的边框。

```
$border $border moveto
$page_width $border 2 mul sub 0 rinetlo
0 $page_height 3 -1 roll pop 100 3 1 roll setscreen
currentscript 3 mul $page_width sub 0 rinetlo closepath
$border 2 mul 0.8 setgray 10 linewidth stroke setgray
```

# 显示用户的登录名，字体大且显目

```
/Helvetica-Bold findfont 64 scalefont set
$page_width($user) stringwidth pop 2 div $page_height 200 moveto
($user) show
```

# 现在显示那些无聊的细节

```
/Helvetica-Bold findfont 14 scalefont set
/200 def
[(Job:) (Host): (Date): ] {
200 moveto show /y y 18 sub def
forall
```

```
/Helvetica-Bold findfont 14 scalefont set
/200 def
[($job) ($host) ($date) ] {
270 moveto show /y y 18 sub def
```

## 第 9 章 打印

```
) forall
%
% 就这些
%
restore
showpage
EOP
```

现在，每个转换过滤器和文本过滤器都可以调用此脚本首先生成页眉，然后打印用户的作业。通过本文早些提到的 DVI 转换过滤器，并对其进行修改以生成页眉：

```bash
#!/bin/sh
# psdf - DVI 到 PostScript 的打印机过滤器
# 安装在 /usr/local/libexec/psdf
# 当用户运行 lpr -d # 时由 lpd 
```

```bash
orig_args="$@"

fail() {
  echo "$@" 1>&2
  exit 2
}

while getopts "x:y:n:h" option; do
  case $option in
    x|y) ;; 忽略
    n) login=$OPTARG;;
    h) host=$OPTARG;;
    *) echo "LPD started 'basename $0' 错误。" 1>&2
      exit 2
  esac
done
```

```bash
[ "$login" ] || fail "没有登录名"
[ "$host" ] || fail "没有主机名"
```

```bash
(/usr/local/libexec/make-ps-header $login $host DVI File)
/usr/local/bin/dvips -f ) | eval /usr/local/libexec/lprs $orig_args
```

注意过滤器是如何解析参数以确定用户和主机名的。其他转换过滤器的解析方式是相同的。不过，文本过滤器使用的参数组略有不同（请参见“过滤器如何工作”章节）。

正如我们之前提到的，上述方案虽然简单地禁用了 `lpr` 的“抑制页眉”选项（`-h` 选项），但如果用户想要省点钱（如果你对页眉收费的话），他们可能无法做到这一点，因为每个过滤器都会在每个作业执行时打印一个页眉。

## 第 9 章 打印

为了允许用户按作业关闭页眉，你需要使用在“页眉计数”章节中引入的技巧：编写一个输出过滤器，该过滤器解析 LPD 生成的页眉并生成 PostScript 版本。如果用户使用 `lpr -h` 提交作业，那么 LPD 将不会生成页眉，你的输出过滤器也不会生成。否则，你的输出过滤器将从 LPD 读取文本，并向打印机发送适当的页眉 PostScript 代码。

如果你在串行链上有一个 PostScript 打印机，你可以利用 `lrps`，它附带了一个输出过滤器 `psof`，该过滤器对页眉不会发生变化。

### 9.4.3 网络打印

FreeBSD 支持网络打印：将作业发送到远程打印机。远程打印通常指两件事：

- 访问连接到远程主机的打印机。你在一个主机上安装了一个具有传统串行或并行接口的打印机。然后，你使用 **LPD** 允许网络上的其他主机访问该打印机。“远程主机上安装的打印机”章节说明了如何操作。

- 访问直接连接到网络的打印机。该打印机除了（或代替）传统的串行或并行接口之外的网络接口。此类打印机的工作方式如下：

    - 它可能理解 **LPD** 协议并可以缓存来自远程主机的作业。在这种情况下，它的作用就像一个普通的运行 **LPD**。按照“远程主机上安装的打印机”中的相同步骤来设置此类打印机。

    - 它可能支持数据流连接。在这种情况下，你通过让该主机负责缓存作业并将其发送到远程，从而将打印机“连接”到网络上的一个主机上。“具有网络数据流接口的打印机”章节为安装此类打印机提供了一些建议。

#### 9.4.3.1 远程主机上安装的打印机

`LPD` 打印系统内置支持将作业发送到同样运行 **LPD** 的其他主机。此功能允许你在一个主机上安装打印机，并让其他主机访问。它也适用于具有 **LPD** 接口的打印机。

要启用这种打印方式，首先按照“简单打印机设置”中的描述在主机上安装打印机。在“高级打印机设置”中使用你需要的设置。测试打印机并确保它适用于你启用的功能。确保本地主机有权限使用 LPD 服务（参见“远程主机的作业限制”）。

如果你使用具有兼容 **LPD** 网络接口的打印机，那么下文中的打印机主机就是打印机本身，而打印机名就是为打印机配置的名称。查看打印机和/或网络接口附带的文档。

**提示**：如果你使用的是惠普激光打印机，打印机名 `text` 会为你执行 LF 到 CRLF 的转换。

## 第 9 章 打印

# diablo-if-net - 为监听端口 5100 的 Diablo 打印机 'scrivener' 的文本过滤器

# 安装在 /usr/local/libexec/diablo-if-net

# exec /usr/lib/libexec/lpr/lpf "$$ " | /usr/local/libexec/netprint scrivener 5100

### 9.4.4 限制打印机的使用

本节提供了有关限制打印机使用的相关信息。`LPD` 系统允许你控制谁可以本地或远程访问打印机、他们是否可以打印多份副本、作业大小有多大以及打印机队列如何处理。

#### 9.4.4.1 限制多份副本

`LPD` 系统让用户能够轻松打印文件的多个副本。用户可以使用 `lpr -5`（例如）打印作业，并在打印机中获得每个作业的五份。这是否可行取决于你。

如果你认为制作副本会导致打印机产生不必要的磨损，可以通过向 `/etc/printcap` 文件中添加 `sc` 属性来禁用 `lpr(1)` 的 `-o` 选项。当用户使用 `-#` 选项提交作业时，他们会看到：

```
lpr: multiple copies not allowed
```

注意，如果你设置了远程打印机（参见“安装在远程主机上的打印机”章节），你仍然需要在远程的 `/etc/printcap` 文件中设置 `sc` 属性，否则用户仍然能够通过另一个主机实现作业的多份打印。

这是一个示例。这是主机 `rose` 的 `/etc/printcap` 文件。打印机 `bamboo` 稍微娇贵，因此我们通过添加 `sc` 属性来禁用多份副本：

```
# /etc/printcap for host rose - restrict multiple copies on bamboo
rattan|line|diablo|lp|diablo 630 Line Printer:\n# sh:sd=/var/spool/lpd/rattan:\n# lp=/dev/lpt0
# if=/usr/local/libexec/if-simple:
bamboo|ps|P|S|panasonic|Panasonic KX-4455 PostScript v51.4:
# sh:sd=/var/spool/lpd/bamboo:
# lp=/dev/ttyds5-parenb cs8 crtsopts:rw:
# if=/usr/local/libexec/psif:
```
