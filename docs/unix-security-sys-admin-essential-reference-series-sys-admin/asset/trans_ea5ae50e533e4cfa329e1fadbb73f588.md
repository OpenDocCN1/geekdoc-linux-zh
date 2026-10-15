

# Listing 2.4 (continued)

```
weeknum ()
{
    echo $1 |
    awk '
    #
    for (i = 1; i <= length; i++) |
        i = length;
        do |
            sum += 64;
            sum += index(digits, substr($0, i, 1)) - 1;
        | while (--i);
    }
    END |
        print sum;
    |
    ' digits=$DIGITS
}
# Given a comma-separated number list (max,min,elapsed),
# output aging code
#
code_val ()
{
    echo $1 |
    awk -f '
    $1 < 0 || $1 >= length(digits) {
        print "Max out of range! 0 <= Max < ", length(digits);
        exit;
    }
    $2 < 0 || $2 >= length(digits) {
        print "Min out of range! 0 <= Min < ", length(digits);
        exit;
    }
    |
```

`code_val` 函数也需要修改以处理反向位值问题。值以逗号分隔的列表形式传递给此函数。因为 `/etc/passwd` 要求最大值和最小值是单字符值，尽管用户可以传递任意数量的测试值，awk 程序会对其进行范围检查。编码值显示为一组字符，例如 00AH，其中 o 是 MAX，0 是 MIN，AH 是已过去的周数。产生的代码可以简单地接收这些字符的连接。因为 MAX 和 MIN 是单字符，awk 的 `substr()` 函数就足够了。

已过去的时间值需要进行 base-64 分解。awk 没有布尔 AND 或位移运算符，因此需要使用除法和取余运算符。这些操作不会因反向位值顺序而改变，但连接顺序会改变。原始版本展示了在数学上正确的数字构造，将 base-64 数字附加到最新数字的值上，作为注释保留供感兴趣的读者参考。要获得反向位值顺序，请将最新数字附加到已构造的 base-64 数字上。最终的 base-64 数字，无论位值顺序如何，都与 MAX 和 MIN 代码连接，并在 `code_val` 函数中省略。

`aging_val` 将编码的 aging 值转换为其十进制形式。`aging_val` 使用 `expr()` 的冒号运算符提取 MAX、MIN 和 ELAPSED 子字符串代码，并使用 `weeknum` 函数显示其十进制等价物。一个关键问题是 HP-UX 的 `/etc/passwd` 规定缺少的 elapsed 代码等同于 0 值。为了使代码规范，`aging_val` 将 `..0` 值附加到代码上。最后，在显示上次更改以来经过的时间时，我选择显示密码更改已有多久。这个数字是动态的。随着时间的推移，每周运行 `chkaging` 程序时，同一账户会显示不同的值。

`show_aging` 是 `chkaging` 程序的默认操作函数。它从 `/etc/passwd` 文件中提取用户名及其加密的密码字段。`chkaging` 假定管理账户的登录将被显式禁用，并且会显示 `*` 而不是密码。它忽略此类账户。否则，每个名称都将与其 aging 信息一起回显。shell 的 `set` 命令解析机制将 aging 信息与加密密码分开。4 位加密字符列表中没有逗号。

最初，脚本简单地在每个登录名旁边输出 aging 不活跃的警告。很快，我遇到了一台几乎每个账户都没有 aging 的系统。为了简化识别这些账户以便修复，我决定将名称累积到 `NOAGING` 变量中。在显示活动用户列表后，我将 `NOAGING` 名称一次性以列格式显示。一旦 `NOAGING` 变量的处理和打印就位，我就注释掉了原来的两行。

主处理例程决定是调用 `show_aging` 来检查 `/etc/passwd` 文件，还是分析加密的 aging 值（`-a` 选项），或分析十进制周代码值（`-d` 选项）。

# Listing 2.4 (continued)

```
code = substr(digits, $1 + 1, 1);
code = code substr(digits, $2 + 1, 1);

elapsed = $3;
do
  quot = int(elapsed / 64);
  remn = elapsed % 64;
  base64 = substr(digits, remn + 1, 1) base64;
  base64 = base64 substr(digits, remn + 1, 1);
  elapsed = quot; while (elapsed >= 64);
  base64 = substr(digits, quot + 1, 1) base64;
  base64 = base64 substr(digits, quot + 1, 1);
  code = code base64;
  print code;
}

' digits=$DIGITS
|
#
# Given a full aging value (no comma), display its numeric values
#
aging_val ()
{
  code = $1
  if [ `expr length $code` -eq 2 ]
  then
    code=$[code]..
  else if [ `expr length $code` -lt 3 ]
  then
    echo Invalid aging code "$code"
    return
  fi
  fi

  MAX=`expr $code : '\(..)'`      # Grab max weeks
  MIN=`expr $code : ':\(..)'`    # Grab min weeks
  ELAPSED=`expr $code : ':\..\(*' ` # Grab weeks since epoch

echo "aging set to `weeknum $MAX` weeks max, \c"
echo "`weeknum $MIN` weeks min, \c"
echo "last changed `expr $NOW_WEEKS - \`weeknum $ELAPSED\`` weeks ago."
}
```

