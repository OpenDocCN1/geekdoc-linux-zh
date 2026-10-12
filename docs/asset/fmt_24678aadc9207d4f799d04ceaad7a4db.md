
我将仅支付`每 6 期 £25.15（节省 30%）`。包含`免费书杂志`！

![](img/628186dda7facdc011bf39c938de3975_26_0.png)

### 付款详情

你的专属读者价格，1 年（13 期 + 免费书杂志）

英国 `£62.40（节省 20%）` | 欧洲 - `£70` | 世界 - `£80` | 美国 - `£80`

- [ ] 支票：我附一张支票，金额为 `£` （受款人为 `Imagine Publishing Ltd`）

- [ ] 信用卡/借记卡：

  - 卡号

  - 有效期

  - 发行号（如果是 `Maestro`）

  - 签名

  - 日期

- [ ] 如果您不希望收到 `Imagine Publishing Ltd` 通过邮寄、电话或电子邮件发送的任何促销材料，请勾选此框。

- [ ] 如果您不希望收到其他公司通过邮寄或电话发送的任何促销材料，请勾选此框。

- [ ] 如果您希望通过电子邮件接收此类信息，请勾选此框。

### 条款与条件

此优惠不包括新订阅者获得一本价值 `£7.99` 的 `Raspberry Pi: The Complete Manual` 第七版免费副本。库存情况以实际情况为准。如果库存售罄，`Imagine Publishing` 保留以价值相同的礼品替代该赠品的权利。新订阅将从下一期可用刊号开始。

此优惠将于 2016 年 10 月 31 日截止。直接借记保证的详情可按需提供。

![](img/628186dda7facdc011bf39c938de3975_27_0.png)

# Tam Hanna

曾被善意地比作詹姆斯·邦德反派佐林博士。这位先生的英俊外表催生了一家现实中的控制系统公司——这是作者你也曾分享的热情。让 `Tam` 成为你在 `Bash` 领域追求纪律性的向导。

## 资源

- 装有 `Bash` shell 的工作站

### Bash 大师课

掌控你的 `Bash` 脚本执行

线性执行脚本很无聊。幸运的是，`Bash` 提供了一组可以修改执行序列的结构。

基于 `DOS` 的 `Bash` 文件造就了一代被宠坏的程序员：他们线性为主的执行方式使 shell 脚本被视为无趣的简单程序。

事实并非如此：`Bash` 为脚本编写者提供了一组控制结构，这些结构理应可与 `JavaScript` 或 `C` 等编程语言中的控制结构相提并论。当智能地使用这些结构时，脚本可以实时定制；通过分析执行环境，可以取代手动重写。

使用 `Bash` 的输入处理功能还开启了更高级的可能性。在完成本教程的全部内容后，你的脚本将能够轮询用户以获取输入。这可以进一步提高脚本的易用性——如果操作得当，你的脚本甚至能够实时拒绝无效输入，从而保护那些笨拙或对技术一无所知的用户安全。

简而言之：学习更多 `Bash` 脚本知识总是值得的。所以——请跟随我们深入高级 `Bash` 程序的兔子洞吧——别担心，我们会支持你...

### 教程文件可下载

`filesilo.co.uk`

![](img/628186dda7facdc011bf39c938de3975_28_0.png)

![](img/628186dda7facdc011bf39c938de3975_28_1.png)

在上一个教程（第 166 期）结束时，我们的脚本已经能够询问用户要发送的邮件主题。让我们通过查看一个小例子来回顾一下：

```bash
#!/bin/bash

echo "Enter title!"

read emailTitle
echo $emailTitle
```

```bash
if [ $emailShorty == "a" ]; then
	echo "Alert, electronics head detected!"
	emailTitle="Analogue electronics tutorial!"

elif [ $emailShorty == "g" ]; then
	emailTitle="Review of gadget"

elif [ $emailShorty == "r" ]; then
	emailTitle="Review of book"

else
	echo "Error"
	exit
fi
```

在指定该文件为 `Bash` 脚本的 shebang（`#!/bin/bash`）之后，我们现在可以调用 `read` 命令从命令行获取数据。然后，它通过 `echo` 函数再次被输出。

`Bash` 要求必须存在 `if` 子句；`elif` 和 `else` 子句是可选的，但保持 shell 脚本更紧凑时很有用。

强制用户输入长文本是移动端的一个经典缺陷：在使用桌面应用程序时，为了可用性，仍应避免这种做法。改善程序行为的一种有效方法是引导用户达到他们的目标。

`if` 子句的实际语法非常实用。选择器用花括号括起来，并以分号终止；`then` 子句开始要执行的命令列表（如果匹配器命中）。

> “脚本将能够实时拒绝无效输入，保护笨拙或对技术一无所知的用户安全”

```bash
#!/bin/bash

echo "Choose the material!"
echo "a...Analogue electronics tutorial!"
echo "g...Review of gadget"
echo "r...Review of book!"

read -n 1 emailShorty
```

然而，对于 unsuspecting 用户来说，还有一个小问题潜伏着。请注意，`[` 必须有一个尾部空格，而 `]` 需要一个头部空格——如果缺失，就会出现类似图中所示的错误。此外，`==` 运算符的左侧和右侧也需要空格。

`read` 可以提供一个或多个参数来修改其行为。传入 `-n 1` 告知命令我们正在寻找单个字符——用户无需按回车键。请注意，这可能会导致控制台输出看起来很别扭——在 `read` 之后添加一个空的 `echo ""` 可以修复此问题。

### 简写表达式

由于从特定集合收集输入是一个极其常见的操作，`Bash` 为其提供了一个简写表达式。它的使用可以简化我们的程序，如下所示：

```bash
echo "Choose the material!"

select emailTitle in "a...Analogue electronics tutorial!" "g...Review of gadget" "r...Review of book"; do
	echo $emailTitle
	break
done
```

### 如果这样，那就那样！

运行上述代码片段后，你会得到一个变量，其中——理想情况下——包含单个字符的输入。将其转换为可用的电子邮件标题需要使用一种通常被称为选择（selection）的结构。它的名字源于其根据变量改变程序执行的习惯。最原始的形式是 `if` 选择，可以这样部署：

```bash
...
read -n 1 emailShorty
echo ""
```

你应该意识到 `break` 命令是强制性的；如果你忘记包含它，脚本将无限循环，这完全不是你想要的。通过 `Ctrl + C` 序列跳出此循环效果最佳，这将导致图中所示的结果。

## 教程

### Bash 大师课

![](img/628186dda7facdc011bf39c938de3975_29_0.png)

### 这是一个旋转木马！

发送多个文件要求我们熟悉 `for` 循环；它执行其命令体，直到传入的参数列表耗尽：

```bash
for file in `ls *.mp3` ; do
    echo "\$emailTitle File \$fileNow of \$fileCount"
    echo "\$file"
    fileNow=$((fileNow+1))
done
```

`for` 也可用于处理数字和/或数字范围。这是通过修改 `$` 运算符或传入完整列表或声明来实现的 – 以下脚本输出两个数字序列：

```bash
for ((a=1; a<=10; a++)); do
    echo \$a;
done

for a in {1..10}; do
    echo \$a;
done
```

`for` 循环非常适合所有 shell 脚本需要处理一组预定义命令的情况。实际上，很少有程序享受在调用时已知任务集的特权 – 在大多数情况下，迭代必须进行直到任务完成。

遗憾的是，使用基于硬件的 `for` 循环示例并不吸引人，因为复用它们很困难。因此，我们将坚持混合示例 – 第一个示例计算一组输入数字的总和：

```bash
myval=22
accu=0
while [ \$myval != "q" ]; do
    read myval
    if [ \$myval != "q" ]; then
        let accu=accu+myval
    fi
done

echo \$accu
```

`while` 是头控循环的实现：如果这样的循环需要至少执行一次，开发者必须相应地设置参数。尾控循环在这种情况下提供了有吸引力的替代方案 – 该程序的另一种实现可以像这样：
