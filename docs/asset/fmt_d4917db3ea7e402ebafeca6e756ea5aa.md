
```perl
print "Output file:\t",
$outfile,
"\n";
#print "Folder number:\t",
$folder_num,
"\n";
#print "Number msg:\t", $number_messages,
"\n";
open(OUTPUT, ">$outfile") or die "$0: could not open [$outfile] for output\n";
$num_output = 0;
for ($i = 1; $i <= $number_messages; $i++) {
    $file = sprintf("%s/f%dm%d.txt",
    $srcdir, $folder_num,
    $i);
    # print $file,
    "\n";
    # print "Processing message ", $i, "\n";
    open(INPUT, $file) or die "$0: could not open [$file] for input\n";
    # 解析消息头信息
    &parse_header;
    if ($valid_header == 1) {
        # 输出消息正文
        while (<INPUT>) {
            if (/^From\s.*/*/) {
                print OUTPUT ..., $__; #  l bug 的 workaround
            } else {
                print OUTPUT $__;
            }
        }
        print OUTPUT "\n";
        $num_output++;
    } else {
        print "File ", $file, ": Invalid message header section\n";
    }
    close(INPUT);
    # 关闭输入文件
}
close(OUTPUT);
# 关闭输出文件
if ($number_messages == $i) {
    print "Wrote ", $num_output, " of 1 message\n\n";
} else {
    print "Wrote ", $num_output, " of ", $number_messages, " messages\n\n";
}
exit;
```

输入文件的前四行包含邮件头信息。

## 附录 D

![](img/e259ba2750941fa3d146eda78c65e89d_495_0.png)

### D.2 转换过程

第1行是“From”信息，第2行是“To”字段，第3行是“CC”字段，第4行是“Subject”字段。

```perl
sub parse_header
local($tl);
local($time, $hours, $minute, $sec, $mday, $wday, $month, $year) = "";
local(%moy) = ('Jan',0,'Feb',1,'Mar',2,'Apr',3,'May',4,
'Jun',5, 'Jul',6,'Aug',7,'Sep',8,'Oct',9,'Nov',10,'Dec',11);
local($from, $to, $cc, $subject) = "";

# 将全局有效头标志初始化为假
$valid_header = 0;

# 从输入文件中读取头行
# 将 from 行拆分为发送者、日期和时间。
# from 行的格式为：

# From: sender dd-MMM-yyyy hh:mm

# sender 是一个由电子邮件地址和个人姓名组成的字符串
# dd-MMM-yyyy 是日期、月份和年份（例如: 22-DEC-1997）
# hh:mm 是小时和分钟（例如: 14:22）

$_ = <INPUT>;
if (($from, $mday, $month, $year, $hours, $minute, $sec) = $_ :- /^From:\t(.*)(\d{1,2})-([a-zA-Z]{3,3})-(\d{4,4})(\d\d) : (\d\d) (.*)/) {
    if ($sec =~ /^: (\d\d).*/) {
        $sec = $1;
    } else {
        $sec = 0;
    }
    $month = ucfirst(lc($month)); # 首字母大写，其余部分小写

# 使用 timelocal 和 ctime 获取日期的星期几
$tl = &timelocal($sec, $minute, $hours,$mday, $moy{$month}, $year);
$time = &ctime($tl);
```

![](img/e259ba2750941fa3d146eda78c65e89d_496_0.png)

```perl
} else {
    return;
}
# "To:" 字段可能跨多行
$_ = <INPUT>;
if ($_ =~ /^To:\t(.*)/) {
    $to = $_;
    while (<INPUT>) {
        if (/^CC:/) {
            last;
        } else {
            s/^\s+//; # 去除领先空格
            $to .= $_; # 追加到 Sto 字符串
        }
    }
} else {
    return;
}
# "CC-" 字段可能跨多行
$_ = <INPUT>;
if ($_ =~ /^CC:\t(.*)/) {
    $cc = $_;
    while (<INPUT>) {
        if (/^Subject:/) {
            last;
        } else {
            s/^\s+//; # 去除领先空格
            $cc .= $_; # 追加到 $cc 字符串
        }
    }
} else {
    return;
}
if ($_ =~ /^Subject:\t(.*)/) {
    $subject = $_;
} else {
    return;
}

# 以 "From - " 字符串开始消息。如果输入文件中包含了日期
# 时间，则添加。
if ($time != "\n") {
    ($wday, $month, $mday, $hours, $year) = split(' ', $time);
    if (substr($hours,1,1) eq ":") {
        $hours = "0"$hours; # 添加领先的 0
    }
    printf "From - %s %s %s %s\n", $wday, $month, $mday, $hours, $year;
    printf "Date: %s, %s %s %s\n", $wday, $mday, $month, $hours;
} else {
    print "From - \n";
    print "From: %s\n", $from;
    print "To: %s\n", $to;
    print "Cc: %s\n", $cc;
    print "Subject: %s\n", $subject;
    $valid_header = 1;
    return;
}
```

![](img/e259ba2750941fa3d146eda78c65e89d_497_0.png)

## 进一步查找之处

除了 OpenMS 官方文档外，还有一些关于 OpenMS 的书籍由 Digital 出版。此外，还有关于 Linux 的书籍。你可以查看当地书店，或使用你喜欢的搜索引擎来查找。几乎所有支持 UNIX 和 Linux 的硬件供应商都提供了文档。我们建议参考以下网站获取更多信息。

该网站是关于 Emacs 的入门站点。

http://www.unh.edu/cis/vms-to-unix/index.html

该网站由新汉布什大学的计算与信息服务部门维护，提供了 OpenMS 与 UNIX 的对比。

http://www.tru64unix.paq.com/products/interop/openvms.html

该网站提供了仿真产品的链接。

![](img/e259ba2750941fa3d146eda78c65e89d_500_0.png)

## 术语表

-   (dot) 当前目录。
-   .. (dot-dot) 当前目录的父目录。
-   绝对路径 从根目录（即 `/`）开始的路径名。
