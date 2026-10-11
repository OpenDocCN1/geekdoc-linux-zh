
```bash
$ bash -f main.sh
You are seeing the operations of the until command. The next digit in the loop is 1:

Now you are seeing what is going on inside loop: 1

Now you are seeing what is going on inside loop: 2

And so on, finishing with

Now you are seeing what is going on inside loop: 7

You are seeing the operations of the until command. The next digit in the loop is 2:

Now you are seeing what is going on inside loop: 1

Now you are seeing what is going on inside loop: 2

Again, this will continue until it ends with

Now you are seeing what is going on inside loop: 7

You are seeing the operations of the until command. The next digit in the loop is 3:

Now you are seeing what is going on inside loop: 1

Now you are seeing what is going on inside loop: 2

Ending with:

Now you are seeing what is going on inside loop: 7

You are seeing the operations of the until command. The next digit in the loop is 4:

Now you are seeing what is going on inside loop: 1

Now you are seeing what is going on inside loop: 2

Ending with:

Now you are seeing what is going on inside loop: 7

The entire cycle continues through the loop, until it reaches:

Now you are seeing what is going on inside loop: 7
```

你可以尝试更改循环中的数字来收缩或扩展两个循环的大小。通过更改循环中的数字，你将能够改变循环的行为方式。

```bash
$ cat test1444
#!/bin/bash
# The following code block shows nesting for loops
for (( x = 1; x <= 3; x++ ))
do
    echo "You are seeing the operations of the until command. The next digit in the loop is $x:"
    for (( y = 1; y <= 5; y++ ))
    do
        echo " Now you are seeing what is going on inside loop: $y"
    done
done
```

```bash
$ bash -f main.sh
You are seeing the operations of the until command. The next digit in the loop is 1:

Now you are seeing what is going on inside loop: 1

Repeated to:

Now you are seeing what is going on inside loop: 5

You are seeing the operations of the until command. The next digit in the loop is 2:

Now you are seeing what is going on inside loop: 1

Repeated to:

Now you are seeing what is going on inside loop: 5

You are seeing the operations of the until command. The next digit in the loop is 3:

Now you are seeing what is going on inside loop: 1

And finishing on:

Now you are seeing what is going on inside loop: 5
```

嵌套循环遍历外层循环迭代的值。对于两个循环，`do` 和 `done` 命令之间没有区别。你可以通过配对 `for` 循环和 `while` 循环来创建嵌套循环。

```bash
$ cat test15
#!/bin/bash
# This is how we can place a for loop in a while loop
var15=15
while [ $var15 -ge 0 ]
do
    echo "You are seeing the operations of nesting loops. The next digit in the loop is $var15:"
    for (( var12 = 1; var12 < 3; var12++ ))
    do
        var13=$[ $var15 * $var12 ]
        echo " Now you are seeing what is going on inside loop: $var15 * $var12 = $var13"
    done
    var15=$[ $var15 - 1 ]
done
```

```bash
$ bash -f main.sh
You are seeing the operations of nesting loops. The next digit in the loop is 15:

Now you are seeing what is going on inside loop: 15 * 1 = 15

Now you are seeing what is going on inside loop: 15 * 2 = 30

This will continue down to the final line:

You are seeing the operations of nesting loops. The next digit in the loop is 0:

Now you are seeing what is going on inside loop: 0 * 1 = 0

Now you are seeing what is going on inside loop: 0 * 2 = 0
```

在下一个示例中，我将配对 `until` 和 `while` 循环来测试嵌套循环的限制。参见以下示例。

```bash
$ cat test16
#!/bin/bash
var15=10
until [ $var15 -eq 0 ]
do
    echo "You are seeing the operations of the nested until and while loops: $var15"
    var12=1
    while [ $var12 -lt 5 ]
    do
        var13=$(echo "scale=4; $var15 / $var12" | bc)
        echo " This is how the inner section of the nested loop functions: $var15 / $var12 = $var13"
        var12=$[ $var12 + 1 ]
    done
    var15=$[ $var15 - 1 ]
done
```
