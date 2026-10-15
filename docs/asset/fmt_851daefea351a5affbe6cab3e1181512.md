
最后一步可能有点难以理解，因为 `eval` 命令被频繁使用。第五章“控制 Shell”有一个关于“Eval 命令”的章节讨论了它。但让我简要介绍一下命令。`eval` 命令展开其参数并执行它们。如果你使用以下行运行 `replace.sh` 命令：

```
% replace.sh -d=dir -e=ext oldText newText
```

那么在完成第四步后，`$oldVar` 的值为“`$4`”。如果你只使用类似这样的命令行：

```
old=`eval echo $oldVar`
```

Bash 会尝试执行一个名为 `oldText` 的命令。这不是我们需要的结果。相反，我们需要将 `oldText` 发送到 STDOUT，以便将其赋值给 `$old` 变量。这就是 `echo` 命令发挥作用的地方：

```
old=`eval echo $oldVar`
```

在执行反引号字符串后，该行变成了 `old=oldText`。

最后，对 `replace.sh` 脚本的解释结束。列表 12.16 包含了完整的脚本。

# 下一段代码设置了默认值
# 以防没有使用命令行选项。
`dir=""`
`extext=""`
`pattern="*"`

# 从命令行参数中提取选项字母（如果有的话）。
`option1=${1%%*}`
`option2=${2%%*}`

# 检查命令行选项是否存在。
# 如果它们存在，其值将存储在 `$dir`
# 和 `$ext` 中。选项的顺序应该是无关的，
# 意味着用户可以指定 `-d e` 或 `-e`。
# 因此，需要对每个选项对 `$1` 和 `$2` 进行测试。

# 测试 `-d` 选项。
```
[ "$option1" = "-d" ] && (
dir=${1#-d}
)
```

```
[ "$option2" = "-d" ] && (
dir=${2#-d}
)
```

# 测试 `-e` 选项。注意
# 扩展名将与 `*.` 结合，以
# 创建一个 `find` 命令
# 使用的模式。
```
[ "$option1" = "-e" ] && (
pattern="*.${1#-e}"
)
```

```
[ "$option2" = "-e" ] && (
pattern="*.${2#-e}"
)
```

# 请看上文以获取下段
# 代码的解释。基本上，它确定了
# `oldText` 和 `newText` 参数的位置
# 并将它们存储在 `old` 和 `new` 变量中。
`newPos=$#`

```
let oldPos=newPos-1
newVar=`echo $newPos`
oldVar=`echo $oldPos`
old-=`eval $oldVar`
new=`eval $newVar`
```

## 第 12 章 / 自定义工具

# 检查指定的目录是否存在（
# 如果有的话）。
```
[ -d $dir ] || {
  echo "`basename $0\` $dir is not a directory!"
  exit 1
}
```

# 使用文件生成一个文件列表。
# 然后，使用 `for` 命令遍历该列表。
# 在循环内部，`sed` 命令执行
# 替换，并将输出保存到临时
# 文件中。然后，覆盖旧文件并
# 删除临时文件。
```
for File in `sed "s/$old/$new/g" $File.zzzzz`
  cat $File.zzzzz > $File.zzzzz && rm $File.zzzzz
done
```

现在是时候看看 Perl 如何处理文件内部替换的任务了。在从一种语言迁移到另一种语言时，我将程序视为一系列的步骤。实际上，最后那句话是一句老话。我总是认为程序是在执行一个过程中的步骤。然而，在迁移时，你可以决定每个步骤涵盖多少活动内容。例如，替换 shell 脚本的开头可以看作：

- # 1. 如果参数数量少于 2，则显示错误消息。
- # 1. 确定参数数量。如果数量少于 2，则显示错误。

虽然这两个选项看起来相似，但更详细的第二个选项对于迁移目的来说更好。它之所以更好，是因为迁移简单的代码块比迁移集成的（整体的）代码块要容易得多。一个代码块执行的操作越少，目标语言拥有可用类比的概率就越大。

较小的代码块减少了迁移过程中任何时刻所需的信息量，有助于加快进度。此外，将你的代码划分为逻辑步骤有助于你关注新语言如何处理任务，而不是一直停留在原始语言的思维模式中。

尽管如此，我不认为我们需要纠结于如何从可移植性的角度来分析问题。我确定有整本书专门探讨这个主题。

相反，让我们来看看你创建 `replace.pl` 所需的一些 Perl 技术（完整内容请见列表 12.17）。

Perl 将命令行选项存储在一个名为 `ARGV` 的数组中。`ARGV` 的第一个元素（索引为0）持有第一个命令行。`ARGV` 数组对应于 shell 的 `$n` 位置变量。

`replace.pl` 脚本的初始步骤之一是确定参数数量。通过使用 `@arrayName` 符号，你可以确定数组中有多少元素。然而，因为 Perl 通常从 0 开始索引，为了保持 Bash 和 Perl 之间的条件表达式一致，你需要加上 `@ARGV`。

检查命令行参数的数量是直的。然而，判断命令行是否使用了选项则有点复杂。第一个命令行选项存储在 `$ARGV[0]` 中。使用下面的正则表达式可以直接提取选项字母和选项参数。选项字母存储在 `$1` 变量中，选项参数存储在 `$2` 变量中。如果参数不包含选项，则 `$1` 和 `$2` 为空。

你可能在第 8 章“模式匹配”中记得，Perl 使用 `$@n` 变量来存储与括号中的子模式匹配的文本。例如，下面的代码显示 BBB：

```
$line = "aaaBBBaaa";
$line =~ m/a+(B)+a+;
print "$1\n";
```

我喜欢把 `$@n` 变量视为……

`readFile` 和 `writeFile` 例程执行了一些清理工作，但并不多。

`readFile` 例程看起来如下：

```
sub readFile (
    my($filename) = shift;
    my($buffer);
    local($/) = undef;
    open(FILE, "$filename")
    or die "Couldn't open $filename for reading: $!";
    $buffer = <FILE>;
    close(FILE);
    return($buffer);
);
```

注意 `shift` 函数用于将第一个参数（`@array` 数组的第一个元素）存储到变量 `$filename` 中。然后，将持有记录分隔符的变量 `$/` 设置为定义。一旦 `$/` 变量被未定义，Perl 就不再理解记录的概念，因此整个文件会被一次性地读取。

`$buffer = <FILE>;` 这行代码从磁盘读取文件。`return($buffer);` 这行代码告诉 Perl 函数的返回值。

读取文件并进行更改后，该将文件写回磁盘了。`writeFile` 例程执行了此操作：

```
sub writefile (
    my($filename, $buffer) = @_;
    local($/) = undef;
    open(FILE, "$filename")
    or die "Couldn't open $filename for writing: $!";
    print $buffer;
    close(FILE);
);
```

`writeFile` 例程没有引入任何新概念。你可能不熟悉 `print` 的用法。默认情况下，`print` 函数将输出发送到 STDOUT。然而，如果第一个参数指定文件句柄，输出将发送到此处。

列表 12.17 显示了完整的 `replace.pl` 脚本。

## replace 命令

### 列表 12.17 replace.pl—使用 Perl 在多个文件上替换文本

```
#!/usr/bin/perl
# Perl 的数组索引从零开始。因此，为了
# 让 if 语句的条件测试与 Bash 脚本相同，
# 需要在 ARGV 数组的元素数量加 1。
$numParameters = $$ARGV + 1;
if ($numParameters < 2) {
    print "Usage: $0";
    print "[-d-directory] [-e-extension] oldtext newtext\n";
    exit(1);
}
# 因为下一节在 foreach 循环中使用了
#确定参数的方法，所以 dir、ext 和 pattern
# 变量的默认值现在需要设置。
$dir = '-. 
$pattern = '*';
# 这部分代码在列表上方的文中进行了解释。
# 快速解释是，代码循环遍历
# 前两个参数。如果参数中任何一个
# 是有效选项，就会设置 $dir 或
# $pattern。
```
