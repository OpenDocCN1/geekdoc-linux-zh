
我计划在夏季继续在美国境内进行我的旅行环游。我下一个要去的州是佐治亚州

每次 `for` 命令遍历对象列表时，它都会将 `mytest` 变量分配给列表中的下一个项。`$mytest` 变量在 `for` 命令语句中的用法与其他脚本变量相同。在最终迭代之后，`$test` 变量在 shell 脚本的剩余部分中保持有效。除非你更改它，否则它将保留最终迭代的值。

```bash
v=$ cat testing111
#!/bin/bash
# This is the basic for command in Linux
```

```bash
for mytest in Alabama Texas Alaska Virginia Arizona Ohio Arkansas South Dakota California North Dakota Colorado New Jersey Florida Michigan Georgia
do
    echo "I am planning to continue my travel circle across the United States in the summer. The next state I will visit is $mytest"
done
echo "The last US state I traveled to was $mytest"
mytest=Connecticut
echo "Now I am going to visit $mytest"
```

```bash
$ bash -f main.sh
```

我计划在夏季继续在美国境内进行我的旅行环游。我下一个要去的州是阿拉巴马州

我计划在夏季继续在美国境内进行我的旅行环游。我下一个要去的州是德克萨斯州

以此类推，直到最后一行：

我计划在夏季继续在美国境内进行我的旅行环游。我下一个要去的州是佐治亚州

我最后去过的美国州是佐治亚州

现在我要去康涅狄格州

可以看到，`$mytest` 变量保留了其原始值，并允许我们在 `for` 循环之外对其进行修改。让我们再看看另一个 `for` 循环示例：

```bash
v=$ cat testing111
#!/bin/bash
# This is the basic for command in Linux
for mytest in pumpkin potato tomato spinach ginger garlic cauliflower cabbage pepper beet ladyfinger broccoli
do
    echo "I am planning to make a shift to the cooking schedule as the summer sets in. I have bought lots of vegetables. However, today I plan to cook $mytest."
done
echo "The last vegetable I cooked was $mytest"
mytest=onion
echo "Now I am going to cook $mytest"
```

```bash
$ bash -f main.sh
```

随着夏季的到来，我计划调整烹饪日程。我买了很多蔬菜。不过，今天我打算做南瓜。

随着夏季的到来，我计划调整烹饪日程。我买了很多蔬菜。不过，今天我打算做土豆。

这会一直持续遍历每种蔬菜，最后以：

随着夏季的到来，我计划调整烹饪日程。我买了很多蔬菜。不过，今天我打算做西兰花。

我最后做的蔬菜是西兰花

现在我要做大葱

在处理 `for` 命令时，你可能遇到的最大问题是如何使用包含多个单词的值。`for` 循环假定每个值之间应由空格分隔。如果你的数据值包含空格，你可能会遇到另一个问题。你可以在美国州名的示例中看到这一点。`bash` 编辑器将 `South` 和 `Dakota` 视为两个不同的值。

`for` 命令为我们提供了引号来分隔包含多个单词的值。你可以使用双引号来分隔 `for` 命令中的不同值。请参见以下示例。

```bash
v=$ cat testing111
#!/bin/bash
# This is the basic for command in Linux
```

```bash
for mytest in Alabama Texas "New York" Alaska Virginia Arizona Ohio Arkansas "South Dakota" California "North Dakota" Colorado "New Jersey" Florida Michigan Georgia "North Carolina" "South Carolina" "New Mexico" "Rhode Island" "West Virginia" "New Hampshire" Vermont
do
    echo "I am planning to continue my travel circle across the United States in the summer. The next state I will visit is $mytest"
done
echo "The last US state I traveled to was $mytest"
mytest=Connecticut
echo "Now I am going to visit $mytest"
```

```bash
$ bash -f main.sh
```

我计划在夏季继续在美国境内进行我的旅行环游。我下一个要去的州是阿拉巴马州。

我计划在夏季继续在美国境内进行我的旅行环游。我下一个要去的州是德克萨斯州。

继续遍历各个州，直到最后一个：

我计划在夏季继续在美国境内进行我的旅行环游。我下一个要去的州是佛蒙特州

我最后去过的美国州是佛蒙特州

现在我要去康涅狄格州

现在 `for` 命令可以区分单字词和多字词的值。另外，最好的是，当你使用双引号时，`shell` 会去掉引号本身（即引号不作为值的一部分）。

## 通过变量读取列表

在 `shell` 脚本中经常发生的情况是，你积累了一组存储在变量中的值列表。然后需要遍历该列表。你可以借助 `for` 命令来完成此操作。

```bash
$ cat testing111
#!/bin/bash
# This is the basic for command in Linux

list="Alabama Texas New York Alaska Virginia Arizona Ohio Arkansas
South Dakota California North Dakota Colorado New Jersey Florida
Michigan Georgia North Carolina South Carolina New Mexico Rhode Island
West Virginia New Hampshire Vermont"

list="$list" Idaho"
for state in $list
do
    echo "I am planning to continue my travel circle across the United States in the summer. The next state I will visit is $state"
done
```

```bash
$ bash -f main.sh
```

我计划在夏季继续在美国境内进行我的旅行环游。我下一个要去的州是阿拉巴马州

我计划在夏季继续在美国境内进行我的旅行环游。我下一个要去的州是德克萨斯州

一直到最后一个州：

我计划在夏季继续在美国境内进行我的旅行环游。我下一个要去的州是爱达荷州

`$list` 变量包含用于迭代的值列表。需要注意的是，代码使用另一个赋值语句来将项连接到现有列表。即使你忘记在列表中添加项，之后也可以通过连接方法将它们添加上去。我将在下一个示例中向列表中再添加五项。

```bash
$ cat testing111
#!/bin/bash
# This is the basic for command in Linux
list="Alabama Texas Alaska Virginia Arizona Ohio Arkansas California Colorado Florida
Michigan Georgia Vermont Iowa Nebraska Arkansas Kansas Kentucky Tennessee Utah
Maine Missouri Minnesota"
list=$list" Idaho"
list=$list" Oregon"
list=$list" Montana"
list=$list" Delaware"

for state in $list
do
    echo "I am planning to continue my travel circle across the United States in the summer. The next state I will visit is $state"
done
```
