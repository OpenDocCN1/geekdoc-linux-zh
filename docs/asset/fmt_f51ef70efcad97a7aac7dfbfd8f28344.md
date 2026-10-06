
| `-k file` | Yes | 文件设置了粘位权限 (Sticky)。 |

| `-s file` | Yes | 文件大小大于。 |

| `-L file` | Yes | 文件是符号链接。 |

| `-o file` | Yes | 文件是旧的。 |

| `-G file` | Yes | 文件是特殊的设备。 |

| `-S file` | Yes | 文件是套接字。 |

| `-t file` | Yes | 文件是终端。 |

| `-z string` | Yes | 字符串为空。 |

| `-n string` | Yes | 字符串不为空。 |

| `string = pat` | Yes | 字符串匹配模式。 |

| `string != pat` | Yes | 字符串不匹配模式。 |

| `s1 < s2` | Yes | s1 小于 s2。 |

| `s1 > s2` | Yes | s1 大于 s2。 |

| `file1 nt file2` | Yes | file1 新于 file2。 |

| `file1 ot file2` | Yes | file1 优于 file2。 |

| `file1 ef file2` | Yes | file1 等于 file2。 |

| `e1 eq file2` | Yes | 表达式 e1 等于 file2。 |

| `e1 ne file2` | Yes | 表达式 e1 不等于 file2。 |

| `e1 gt file2` | Yes | 表达式 e1 大于 file2。 |

| `e1 ge file2` | Yes | 表达式 e1 大于或等于 file2。 |

| `e1 lt file2` | Yes | 表达式 e1 小于 file2。 |

| `e1 le file2` | Yes | 表达式 e1 小于或等于 file2。 |

# 函数

Korn shell 完全支持函数，并提供了一些扩展。

## 定义函数

除了 Bourne shell 的语法外，Korn shell 支持以下替代语法来定义函数：

```
function 标识
{
  command-list
}
```

### 在函数中使用变量

Korn shell 允许函数具有局部变量。局部变量只在函数执行期间存在，并在函数返回时销毁。局部变量可以与调用环境中的变量同名。使用 `typeset` 命令定义局部变量。例如：

```
function square
{
  typeset product
  let product=$1*$1
  print $product
  return
}
```

### 在函数中使用陷阱

在 Bourne shell 中，用 `trap` 设置的陷阱在函数返回后仍然有效。在 Korn shell 中，环境中的陷阱会被保存并恢复。

你可以使用 `typeset` 命令配合 `-f` 选项来管理函数。`-f` 选项有四种形式，如表 11.15 所示。

## 表 11.15.-f 选项。

| 形式 | 描述 |
| --- | --- |
| `typeset -f` | 列出当前定义的函数及其定义。`alias functions` 执行相同的功能。 |
| `typeset -ft name` | 每当调用函数名时激活 `xtrace` 选项。函数返回时追踪恢复到原有状态。 |
| `typeset -fx name` | 将函数导出。导出的函数会被 shell 脚本继承。函数无法导出到另一个 ksh 实例。然而，没有像传递变量那样的方法来传递函数定义。 |
| `typeset -fu name` | 将函数定义为自动加载。`autoll` 在函数被调用时定义，在用 `typeset` 声明时被识别为函数。Korn shell 在 `FPATH` 变量指定的目录中搜索与函数同名的文件。如果 Korn shell 找到了文件，则加载并执行函数，其定义就像在这一点读取了内联定义一样。 |

### 使用自动加载函数

自动加载函数的性能优于传统的 shell 脚本，因为它们在首次调用后会被保留在内存中；然而，除了处理 `typeset -fu` 命令外没有其他开销。创建自动加载函数的方法与 shell 脚本相同，只是函数定义应该在函数中；它应该以 `function name` 开头。要使用自动加载，必须将 `FPATH` 环境变量设置为目录或目录到

搜索方式（与你设置 `PATH` 环境变量的方式相同），你必须提前使用 `typeset -fu` 命令声明函数。

任何函数都可以作为自动加载（autoload）函数，但优先选择频繁使用的函数。记住，在调用自动函数后，它的定义会保留在 shell 的内存中。除非程序被频繁使用，否则大型程序应该写成传统的 shell 脚本而不是自动函数。

## 未定义函数

要取消定义函数，使用 `unset` 命令：

```
unset -f name ...
```

命名的函数将从内存中清除，任何对命名函数的 `typeset -fu` 声明都将被删除。`unset -f` 命令并不经常使用，但在调试函数时非常有用。使用 `unset -f` 是强制 shell 重新读取自动函数文件的唯一方法。

## 何时使用函数

函数是创建新键盘命令的方便方法。由于函数是在当前 shell 环境中执行的，因此通过 `cd` 命令进行的目录更改在函数退出后仍然有效。这对于普通命令和 shell 脚本来说并非如此。由于我几乎喜欢在切换目录后快速查看一眼其内容，我创建了以下短函数定义并将其添加到我的登录配置文件中：

```
function go
  cd $1
  /usr/bin/ls -FC
```

`go` 函数用于形成 `go dirname`，它不仅切换目录，还会打印一个排序列表，让我看到目录里有什么。

将 `go` 函数添加到我的登录配置文件意味着它存在于 shell 内存中。由于 `go` 是一个很小的函数，考虑到我使用的频率，它并无害。对于较大的函数，最好将函数存储在单独的文件中并用 `typeset -fu` 声明替换配置文件中的函数定义，使该函数成为自动函数。

## 使用 getopts 扫描参数

Bourne 在处理命令行选项方面提供的帮助乎其微。因此，许多用户编写的 shell 脚本处理选项的方法多是笨拙；它们通常不使用通用的 UNIX 选项格式。`getopts` 命令作为 UNIX 命令集的标准部分，提供了一定的帮助。Korn 为脚本编写者提供了 C 程序员长期羡慕的灵活性。

`getopts` 内置命令的语法非常直观：

```
getopts options var [ arg ... ]
```

对于 `options`，提供一个字符串，定义可以作为命令行选项出现的字母。如果某个选项可以跟一个值字符串，通过在选项字符串中的字母后跟一个 `:` 来指示这一点。例如，`1:` 代表选项语法 `-string`。

如果 `options` 以 `:` 开头，Korn 提供了用户错误处理。无效的选项字母被放在 `OPTARG` 中，而 `var` 被设置为 `?`。如果没有 `:`，`getopts` 命令在遇到无效字母时会发出错误信息并将 `var` 设置为 `?`，以便你可以识别出发生了错误并跳过输入，但它不会标识无效的字母。

对于 `var`，写入接收选项的变量名。当 shell 识别出命令行中的选项时，它会将字母存储在 `var` 中。

对于 `arg`，写入从命令行获取的待扫描的参数列表。`arg` 列表通常以 `$*` 或 `"$"` 的形式编写。

出于实用考虑，`getopts` 命令无法在一次调用中扫描、识别并处理命令中的所有选项。每次你调用 `getopts`，你都会获取命令行上的下一个选项。当然，`getopts` 无法查看你的 shell 脚本调用的实际命令。它检查你通过 `getopts` 提供的 `arg`，每次调用时遍历列表。

当你调用 `getopts` 时，它首先确定其在 `arg` 列表中的当前位置。如果你当前的位置在一个单词内部且该单词以 `-` 开头，则单词中的下一个字符被视为选项。如果是第一次调用 `getopts`，或者上次调用完成了对一个单词的扫描，`getopts` 会检查下一个 `arg` 是否有连字符。

无论情况下，`getopts` 识别出一个选项并存储在 `var` 中。如果选项需要值字符串，该值将存储在预定义的变量 `OPTARG` 中。如果 `getopts` 开始处理新的 `arg`，它会增加预定义变量 `OPTIND`，以指示是哪个参数（1、2 等）。它会更新 `arg` 列表中的位置。

在调用 `getopts` 后，你解析 `var` 以查看找到了哪个选项。如果选项需要值，你将在预定义的变量 `OPTARG` 中找到它的值。如果 `getopts` 找到选项，则返回值为 0；如果在命令-参数列表中找不到更多选项，则返回非零值。

使用 `getopts` 的代码是一段你需要记忆的固定内容。列表 11.1 是一个你在脚本文件中常见的扫描命令行选项的 shell。这里，示例仅展示了它识别的选项。

## 列表 11.1. 使用 getopts 扫描选项。

```bash
# 一个扫描选项的程序
# ... 允许的选项有 -a, -c, -C, -Aname, 或 -Inode。
while getopts :acRA:I KEY
do
  case $KEY in
    a) print Found option -a;
    c) print Found option -c;
    R) print Found option -R;
    A) print Found option -A, value = "$OPTARG";
    I) print Found option -I, value = "$OPTARG";
    *) print -u2 Illegal option: -$OPTARG
  esac
done
# 移除参数，留下位置参数
shift OPTIND-1
print args:$@
```

列表 11.1 中的代码将执行。它将参数设置到一个文件中并使用 `chmod` 使文件为可执行。（注：此处原文中存在大量重复和 OCR 错误，译文已根据核心逻辑进行清理和整合）。

重新显示列表并在不调用 `command-list` 的情况下发布提示。如果用户输入了变量，则名为 `identifier` 的变量将被设置为与之对应的单词。也就是说，通过为第一个单词输入 `1 identifier`，为第二个单词输入 `2 identifier` 等，以此类推。如果数字大于单词数，或者用户输入的不是有效的标识，则 `identifier` 为 `null`。在任何情况下，`select` 语句随后都会执行 `command-list`。

考虑以下示例，其中用户被要求选择颜色。`select` 语句将继续执行，直到用户选择一种可用的颜色。

```
PS3="Select color by number (e.g., 3):"
select color in Blue Green Red White Black Burnt-umber "Natural Wool"
do select color in
  Blue | Green | Red | White | Black |
  Burnt-umber | "Natural Wool") break;
  *) print "Please enter a number from 1-8. Try again";
esac
done
```

注意这里使用引号将 `Natural Wool` 指定为菜单选项之一。如果单词没有加引号，`select` 语句会将它们视为两个单独的项目，用户将可以选择 `Natural`（项目 8）或 `Wool`（项目 9）。

还要注意，该示例不会在用户输入有效选择之前反复执行菜单选择过程。`select` 的迭代是自动的。它会验证选择，必须满足某些条件才能跳出 `select` 循环——在这种情况下，通过执行 `break` 语句来实现。

没有什么可以阻止使用 `select` 实现一个原始的、菜单驱动系统。列表 11.2 使用 `select` 语句为用户提供操作选择。该示例将继续执行，直到用户选择 `Exit` 项目。然后，`select` 语句以及任何以 `exit` 内置命令终止的 shell 脚本都将退出。

## 列表 11.2. 使用 select 实现菜单系统。

```
PS3=Choice? 
select choice in "Enter Transactions" \
  "Print trial balance" \
  "Print invoices" \
  "Exit"
do case $choice in
  "Enter Transactions") daily-trans ;;
  "Print trial balance") trial-balance ;;
  "Print invoices") print "That's all, folks"; exit;
  *) print -u2 "Wrong choice. Enter a number (1-4)."
esac
done
```

## 使用协进程 (Coprocesses)

Bourne shell 提供了进程之间极少的通信——通常通过管道运算符 `|` 实现。你可以从 shell 脚本中调用行编辑器，通过如列表 11.3 所示的命令来实现特定的文本更改。

## 列表 11.3. 基础进程通信。

```
(echo "/Payroll
+1
i"
cat newlist
echo ".w"
echo "q"
)| ed paylist
```

如果你只需要向另一个命令传递一些数据或读取其输出，这种交互方法就足够了。因此，在列表 11.3 中，你希望考虑到 `paylist` 不包含以 `Payroll` 开头的行的情况，即跳过写入并退出。在 Bourne shell 中，你可以与 `ed` 命令保持交互会话，由你的程序向其提供指令并对其输出做出响应。

要使用协进程（两个相互读取的进程同时执行的专业术语），你必须首先通过特殊运算符 `&` 将你想要通信的程序作为后台进程启动。`|` 运算符用于建议 `&`（后台执行）和 `|`（管道运算符）的组合。当协进程启动时，它的标准输入和输出被分配到你进程的管道——一个用于写入，一个用于读取。向协进程发送一行的最简单的方法是使用 `print -p` 命令。`-p` 选项告诉 `print` 写入协进程的输入。要从协进程读取输出，使用 `read -p`。同样，`-p` 告诉 `read` 从协进程读取。使用这些设施，你可以将前面的过程重写为列表 11.4 所示的形式。

## 列表 11.4. 使用协进程进行进程通信

```
ed paylist &
exec 3&
exec 4&
read -u4
print -u3 #丢弃初始消息
print -u3 "/Payroll" # 搜索指示成功或失败的提示
case "$REPLY" in
*) # 搜索必须成功
print -u3 i
cat >&3 # 包含数据的文件
read -u4 # 读取结束提示符
print -u3 w;
*) # 未找到
print -u3 q
echo "invalid paylist"
exit
;;
esac
```

你应该在该示例中注意以下几点：

- `exec` 命令 `exec 3>&` 用于将协进程输入管道从其默认位置移动到编号的文件描述符。

- `exec` 命令 `exec 4<&` 再次用于将协进程输出管道移动到文件描述符 4。

- 后续的 `read` 和 `print` 命令使用 `-u` 选项指定文件描述符作为操作的源或目的。

- 普通的 UNIX 命令可以通过重定向到文件描述符 3 (`cat >&3`) 写入协进程。

注意：使用 `read -p 或 print` 从协进程读取或写入，直到你将协进程的输入或输出移动到文件描述符。然后对该文件描述符进行读写：`read -u4 或 print -u3`

诚然，程序 11.4 在协处理时比程序 11.3 更复杂，但它更安全。Bourne shell 版本在搜索 `Payroll` 失败时，会在第一行之后添加新行。Korn shell 则会优雅地失败，而不会损坏 `paylist` 文件。

`.profile` 脚本，会删除整个文件。这对 shell 来说没有关系。支持 `.profile` 仅是为了你的方便；在 Korn 操作中并不需要它。

实际上，你的 `.profile` 脚本是一个 shell 脚本。在 shell 脚本中有效的 shell 编程技术在 `.profile` 脚本中同样有效。如果你不是 shell 程序员，也不要畏。你可以编写一些实用的登录脚本，它们只包含简单的 UNIX 和 shell 命令，完全没有 `if` 或 `while` 语句。如果你知道如何使用 shell 条件判断和迭代语句，那就更好了。不要认为精通这些语句对于编写良好的 profile 脚本至关重要，事实并非。

你的 `.profile` 脚本是你放置常用物品的理想场所。你可能想对 `.profile` 文件执行以下操作。你还应该观察这些项目的列出顺序。将相似的内容有助于合并你的 `.profile`。

- 使用 `stty` 命令设置控制键。

- 设置环境变量。

- 设置用于 shell 控制的局部变量。

- 定义你喜欢的别名（aliases）。

- 定义你喜欢的函数，包括自动加载函数（autoload functions）。

- 设置你喜欢的选项。

- 执行你每次登录时都想运行的命令。

## 使用 stty 设置控制键

使用 `stty` 命令建立你喜使用的按键。默认的删除键（Erase）是 `#`，默认的终止键（Kill）是 `^`。两者都是糟糕的选择，因为它们的终端字符与你作为普通字符使用的字符冲突。你应该像这样重新定义这些键：

```
stty erase '^H kill '^U intr '^C
```
