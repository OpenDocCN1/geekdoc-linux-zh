
这会将 `x` 的原始值加 10 并将结果赋值回 `x`。这种简写适用于上述列出的所有运算符：`+`、`-`、`*`、`/`、`%`、`<<`、`>>`、和 `>>>`。

# 控制结构

控制结构是一个通用术语，用于描述条件判断、循环、函数以及相关的命令（如 `return` 和 `break`）。这些命令允许你控制 NASL 脚本内部的执行流。NASL 支持经典的 `if-then-else` 语句，但不支持 `case` 或 `switch` 语句。NASL 中的循环包括 `for`、`foreach`、`while` 和 `repeat-until`。`break` 语句可以防止循环继续迭代，即使循环条件仍然为真。NASL 同样使用内置函数和用户定义函数，两者都使用 `return` 语句将数据传回调用者。

# if 语句

NASL 支持 `if` 和 `else` 结构，但不支持 `elseif`。你可以通过链式 `if` 语句在 NASL 中重实现 `elseif` 或 `elif` 的功能。

```
if (x == "10") {
    display("x is 10");
} else if (x > 10) {
    display("x is greater than 10");
} else {
    display("x is less than 10");
}
```

# for 循环

循环语法与 C 语言中使用的语法几乎相同。该语法是：

```
for (InitializationExpression; LoopCondition; LoopExpression) {
    # 重复代码
}
```

这是一个打印 1 到 100 的数字（每行一个）的示例：

```
for (i=1; i<=100; i++) {
    display(i, '\n');
}
```

注意，在这个循环执行完毕后，`i` 的值为 101。这是因为 `LoopExpression` 会评估每次迭代，直到 `LoopCondition` 变为 FALSE。在这种情况下，一旦 `i` 被赋值为 101，`LoopCondition` (`i <= 100`) 就会变为 FALSE。

# foreach 循环

`foreach` 循环可以用于遍历数组中的每个元素。要遍历数组中的所有项，请使用此语法，它会将数组中的值赋值给变量 `x`：

```
foreach x (array) {
    display(x, '\n');
}
```

你也可以使用 `foreach` 循环和 `keys` 函数将数组索引放入数组或哈希表中：

```
foreach k (keys(array)) {
    display("array", k, " ", array[k], '\n');
}
```

# while 循环

`while` 循环只要条件为真就会持续迭代。如果条件初始为假，则代码块将永远不会执行。

```
i = 1;
while (i <= 10) {
    display(i, '\n');
    i++;
}
```

# repeat-until 循环

`repeat-until` 循环类似于 `while` 循环，但它们不是在每次迭代之前评估条件，而是在每次迭代之后评估条件，从而确保 `repeat-until` 循环至少会执行一次。这里有一个简单的示例：

```
x = 0;
repeat {
    display (++x, '\n');
} until (x >= 10);
```

# break 语句

`break` 语句可以用于循环条件变为 FALSE 之前停止循环迭代。以下示例展示了如何使用 `break` 统计字符串 (`str`) 中第一个非零值之前的零的个数。请记住，如果 `str` 的长度为 20 个字符，那么数组的最后一个元素是 `str[19]`。

```
x = 0;
len = strlen(str);
while (x < len) {
    if (str[x] != "0") {
        break;
    }
    x++;
}
if (x == len) {
    display("str contains only zeros");
} else {
    display("There are %s before");
}
```

# 用户定义函数

除了许多内置函数，你还可以创建自己的函数。用户定义函数的语法如下：

```
function_name (argument1, argument2, ...) {
    # 代码
}
```

例如，一个接收字符串并返回数组的函数可能如下：

```
function my_function(str) {
    # 代码
    return result;
}
```

## 字符串处理函数

类似于高级脚本语言，NASL 提供了用于分割字符串、搜索正则表达式、删除末尾空格、计算字符串长度以及将字符串转换为大写或小写的函数。NASL 还有一些对漏洞分析非常有用的函数，最著名的是用于测试缓冲区溢出的 `crap` 函数，它会根据需要返回字母 X 或任意输入，直到填满请求大小的缓冲区。

## 加密函数

作为 NASL 解释器，Nessus 提供了各种加密和校验哈值的函数，包括 MD2、MD4、MD5、RIPEMD160、SHA 以及 SHA1。还有几个函数可以根据任意数据和提供的密钥生成认证码。

## NASL 命令行

使用解释器非常简单。基本用法是：`nasl -t target_ip scriptname.nasl scriptname2.nasl ...`

如果你只想使用“安全检查”（safe checks），可以添加一个可选的 `-s` 参数。此外还有用于调试详细输出的选项。运行 `man nasl` 可查看更多详情。

## 示例

想象这样一个场景：你希望将所有的 Apache Web 服务器从 1.x 系列升级到新的 2.x 系列。你可以编写一个像示例这样的 NASL 脚本来扫描网络中的每台计算机，获取每个 banner（标识），并在每次发现旧版本 Apache 时显示通知。示例中的脚本并未假设 Apache 运行在默认的万维网（WWW）端口 (`80`) 上。此脚本可以轻松修改为打印发现的每个 banner，从而创建一个简单的 TCP 端口扫描器。如果将其保存为 `apache_find.nasl` 且你的网络使用的 IP 地址为 192.168.1.1 到 192.168.1.254，则使用 NASL 解释器针对该地址的命令如下：

`nasl -t 192.168.1.1-254 apache_find.nasl`

第 8 和第 9 行打开套接连接成功。在通过内联初始化 banner（第 11 行）获取 banner 并使用 `recv_line` 函数后，第 13 行使用正则表达式判断接收到的 banner 中是否包含 Apache。最后，脚本识别出返回 banner 的相应端口上发现了 Apache 1.0 版本。

尽管这个示例脚本在执行这项特定任务时效率尚可，但它并不适用于 Nessus。当运行带有完整检查库的 Nessus 时，每个脚本都会按顺序执行，并可以利用前一个脚本已完成的工作。在这个示例中，脚本手动扫描每个端口、获取每个 banner 并检查每个是否为 Apache。想象一下，如果每个脚本都做这么多工作，运行 Nessus 将是多么低效！下一节将讨论如何优化 NASL 脚本，以便它们在 Nessus 中更高效地运行。

## 在 Nessus 框架中编程

一旦你使用命令行解释器编写了 NASL 脚本，你只需要进行极少的修改即可从 Nessus 控制台运行。完成这些更改后，你就可以将脚本提交给 Nessus 管理员并与 Nessus 社区共享。

## 描述函数

为了与 Nessus 社区共享你的 NASL 脚本，你必须修改脚本以包含一个向 Nessus 引擎提供名称、摘要、详细描述和其他信息的头部。这些“描述函数”允许 Nessus 执行测试当前目标所需的脚本，它们还用于确保只运行来自适当类别（信息收集、扫描、攻击、DOS 等）的脚本。

## 知识库函数

共享脚本必须以尽可能高效的方式编写。为此，脚本不应重复其他脚本已经执行的工作。此外，脚本应该对发现的任何结果创建记录，以便后续脚本避免重复工作。跟踪当前运行期间收集信息的中心机制称为“知识库”（Knowledge Base）。

使用知识库之所以简单有两个原因：

- 使用知识库函数非常简单，比手动端口扫描、手动获取 banner 或重新实现知识库功能要容易得多。
- 当对知识库的请求返回多个结果时，Nessus 会自动分叉（fork）。

为了说明这两点，考虑一个必须对特定主机发现的每个 HTTP 服务进行分析的脚本。如果没有知识库，你可以编写一个脚本扫描整个主机、执行 banner 检查，并在发现合适目标后执行你想要的任何分析。运行由这类脚本组成的 Nessus 是极其低效的，因为每个脚本都在进行重复工作并浪费了大量的时间和带宽。有了知识库，脚本只需调用一次知识库 `get_kb_item("Services/www/")` 函数即可完成工作，该函数会返回发现的 HTTP 服务器的端口号，并根据实例的每个响应自动为脚本分叉。

## 报告函数
