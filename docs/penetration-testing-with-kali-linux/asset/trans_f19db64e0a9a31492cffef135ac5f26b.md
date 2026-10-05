

```bash
kali@kali:~/passwordattacks$ sed -i '^/1/d' demo.txt
```

```bash
kali@kali:~/passwordattacks$ cat demo.txt
password
iloveyou
princess
rockyou
abc123
```

列表 266 - demo.txt 的内容和位置

我们现在 demo.txt 字典列表中有了五个密码。让我们对这些密码进行变异，以符合密码策略，该策略必须包含一个数字值、一个特殊字符和一个大写字母。

[Hashcat Wiki<sup>229</sup>] 提供了所有可能的规则函数列表。如果我们想添加一个字符，最简单的方法是在其前面或后面添加它。我们可以使用 `$` 函数来添加字符，或者使用 `^` 在前面添加字符。这两种方式都要求在函数选择符后紧跟一个字符。例如，如果我们想在文件的每个密码末尾添加 "3"，对应的规则函数将是 `*3`。

在生成带有数值的密码时，许多用户简单地在现有密码末尾添加“1”。因此，让我们创建一个包含 `$1` 的规则文件，将其添加到字典列表中的所有密码中。我们将创建一个带有此函数规则的 demo.rule。我们需要转义特殊字符 `\$` 以正确将其回到文件中。

```bash
kali@kali:~/passwordattacks$ echo \$1 > demo.rule
```

列表 267 - 为所有密码添加 '1' 的规则函数

现在，我们可以使用 hashcat 配合字典列表，通过 `-r` 提供规则文件，并使用 `-stdout` 在调试模式下启动 Hashcat。在此模式下，Hashcat 将不会尝试破解任何哈希值，但可能会显示变异后的密码。

```bash
kali@kali:~/passwordattacks$ hashcat -r demo.rule --stdout demo.txt
password1
iloveyou
princess1
rockyou
abc123
```

列表 268 - 使用调试模式下的 Hashcat 显示所有变异密码

列表显示规则 `$1` 在每个密码末尾添加了一个 "1"。

> 如果你收到错误 "Not enough allocatable device memory for this attack"（此攻击没有足够的可用设备内存），请关闭你的 Kali 虚拟机并为其添加更多内存。4GB 对于示例和练习是足够的。

## OffSec

现在，让我们处理密码策略中的大写字母。当被强制在密码中使用大写字母时，许多用户倾向于将首字母大写。因此，我们将向规则文件添加 `c` 函数，它会将首字母大写，并将其余部分转换为小写。

让我们尝试一个使用两个相同文件的示例：demo1.rule 和 demo2.rule。我们将以不同的格式化这些文件。

在 demo1.rule 中，规则函数通过空格在同一行内。Hashcat 将对字典列表中的每个密码连续使用这些函数。结果是每个密码的首字母都大写了，并且每个密码末尾都添加了 "1"。

在 demo2.rule 中，规则函数分行编写。Hashcat 将第二个函数（在第二行上）解释为新的。在这种情况下，每个规则被单独使用，导致字典列表中的每个密码产生两个变异后的密码。

```bash
kali@kali:~/passwordattacks$ cat demo1.rule
$1 c

kali@kali:~/passwordattacks$ hashcat -r demo1.rule --stdout demo.txt
Password1
iloveyou1
Princess1
Rocky1
Abc231

kali@kali:~/passwordattacks$ cat demo2.rule
$1
c

kali@kali:~/passwordattacks$ hashcat -r demo2.rule --stdout demo.txt
password1
Password
iloveyou1
iloveyou
princess1
Princess
```

列表 269 - 使用空格和换行符分隔两个规则函数

很好！我们已经将 demo1.rule 文件适应了三个密码策略中的两个。让我们处理第三个并添加一个特殊字符。`!` 是一个非常常见的特殊字符。

基于此假设，我们将向规则文件添加 `$1`。由于我们希望将所有函数应用到每个密码，我们需要在同一行上指定这些函数。再次，我们将通过不同的规则文件来演示这一点，以强调组合规则函数的效果。在第一个规则中，我们在第一条规则的末尾添加 `$1`。在第二个规则中，我们将其添加到规则的开头。

```bash
kali@kali:~/passwordattacks$ cat demo1.rule
$1 c!

kali@kali:~/passwordattacks$ hashcat -r demo1.rule --stdout demo.txt
Password1!
```

## OffSec

Iloveyou1!
Princess1!
Rockyou1!
Abc231!

```bash
kali@kali:~/passwordattacks$ cat demo2.rule
$ $ c
```

```bash
kali@kali:~/passwordattacks$ hashcat -r demo2.rule --stdout demo.txt
Password1!
Iloveyou1!
Princess1!
Rockyou1!
Abc231
```

列表 270 - 在开头和末尾添加规则

输出显示 demo1.rule 通过在末尾添加 "1" 来处理密码。另一个文件 demo2.rule 则在开头添加了 "1"。这表明规则是从左到右应用的。

demo1.rule 包含的规则变异了我们的字典列表以符合密码策略的要求。

现在我们理解了规则以及如何创建它们，让我们对基于规则的攻击进行破解。在本演示中，我们假设从 MD5 哈希 "f6216c92eb95ab53ae2ef4c7fe4cb60" 获取 rockyou.txt。这适用于需要大写字母、数值值和特殊字符的密码策略。

让我们创建一个规则文件来访问此策略。在此，我们将使用 `c` 函数进行首字母大写。此外，我们再次使用 `!` 作为特殊字符。对于数值值，我们将紧随特殊字符添加 "1"、2" 和 "123"。

```bash
kali@kali:~/passwordattacks$ cat crackme.txt
f6216c92eb95ab53ae2ef4c7fe4cb60
```

```bash
kali@kali:~/passwordattacks$ cat demo3.rule
$1 c $
$2 c $

```

列表 271 - MD5 哈希和规则文件

接下来，我们运行 Hashcat。我们将通过移除 --stdout 来禁用调试。相反，我们将使用 `-m` 来指定哈希类型。在本演示中，我们要破解 MD5，哈希类型为 0，这是从 Hashcat 页面获取的。在哈希类型之后，我们将提供哈希文件（crackme.txt）和 rockyou.txt 字典。然后通过 `-r` 指定我们的 demo.rule 文件。由于我们的 Kali 虚拟机无法访问 GPU，我们将使用 `-force` 来忽略 Hashcat 的相关警告。

```bash
kali@kali:~/passwordattacks$ hashcat -m 0 crackme.txt /usr/share/wordlists/rockyou.txt
-r demo3.rule --force
hashcat (v6.2) starting
```

## OffSec Penetration Testing with Kali Linux

字典缓存命中：

- Filename: /usr/share/wordlists/rocky.txt
- Passwords: 14344
- Bytes: 139921

