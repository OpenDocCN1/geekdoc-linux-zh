
在列表 8.3 中，`$` 符号被用于控制 `ClassTest` 规则内部的流。每个以 `$` 符号开头的规则模板中，如果找到了模式，则应用模板并退出规则。假设在列表第一个规则上没有使用 `$`。在这种情况下，对 `christopher@robin` 地址的测试将产生响应 `"Wrong"`，而不是我们预期的 `"Found"`。原因如下：`christopher@robin` 地址匹配第一个规则的模式 `$*w`。因此，地址被重写为 `Found`。如果没有使用 `$` 符号，地址将再次与第一个规则中的模式 `$*w` 进行比较。它不匹配。地址由行中的下一个规则处理。它不匹配第二个规则的模式 `$*w`。因此，地址被传递给行中的第三个规则。这次它匹配了模式 `$*$`，该模式本质上匹配任何未被前两个规则捕获的内容。第三个规则将 `Found it` 重写为地址 `Wrong format`——当然，这不是我们想要的。为了得到我们的结果，`ClassTest` 规则集中的每个规则都需要流控制符号，即使是第三个规则也是。

当模板以 `$:` 符号开头时，该规则只执行一次。在列表 8.3 的 `ClassTest` 规则集中，这正是我们想要对第三个规则做的。

`rule`。乍看之下，人们可能认为规则不需要流程控制，因为它是规则集中的最后一个规则，并且在该规则执行后就会结束。仔细观察，问题就一目易见了：第三条规则永远不会执行完毕，因为它是一个死循环。`$*$` 模式匹配零个或多个标记，它可以匹配任何内容，即字符串 `Wrong format`。因此，该模式将匹配规则的输出。由于规则递归地处理自身的输出并匹配模式 `$*$`（它可以匹配任何内容），将会导致循环。`Sendmail` 会检测循环并在发现循环时报错，如列表 8.6 所示。

### 列表 8.6 Sendmail 配置中紧密循环的结果

```
[root]# sendmail -bt -Ctest.cf
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enterter <ruleset> <address>
 >=ClassTest
R$* @ $~w $@$ Found it
R$* @ $^w $@$ Not in class w
R$* 
    Wrong format
> ClassTest input: craig
ClassTest
Infinite loop in ruleset ClassTest, rule 3
ClassTest
returns: Wrong format
> ^D
```

在列表 8.6 中，`sendmail` 再次使用 `-bt` 参数运行。在第 10 章中与其他测试命令一起描述的 `=S` 命令用于显示规则集 `ClassTest` 的内容。在这个示例中，规则集中第三条规则的模板不以 `$` 开头。在这种情况下，当 `ClassTest` 以输入地址 `craig` 运行时，就会产生无限循环。`Sendmail` 显示一条错误消息，说明遇到了无限循环，并准确指出了循环发生的具体位置。

循环不需要像列表 8.6 所示那样紧密。一个循环可以涉及多个规则，因为规则可以通过 `$name` 语法被另一个规则调用。被调用的规则完成处理后，它会向调用规则返回一个重写后的地址。然后，将返回的电子邮件地址与调用规则中的模式进行比较。如果它仍然匹配，则会再次调用该规则集。在任何可能发生循环的地方使用 `::$` 和 `$$` 来防止循环。

## 重写规则 237

符号 `$>name` 会调用规则集 `name`，并将模板剩余部分定义的地址传递给该规则集进行处理。例如，下面所示名为 `CallRulesets` 的规则集中的两条规则都调用了其他规则集：

```
CallRulesets
R$* @-            $: $: canonify $1 @ $2
R$* @-            $: final $1
```

第一条规则中的模板调用规则集 `canonify` (`$canonify`)，并传递 `$1` 的内容、字面量 `@` 以及 `$2` 的内容。模板以 `::$` 符号开头，因此当模式匹配时，第一条规则只执行一次。第二条规则中的模板调用规则集 `final` (`$final`)，并传递 `$1` 的内容（由于第二个规则集中的模式仅包含一个符号，`$1` 包含了整个输入地址）。第二条规则也会执行一次，因为它的模板以 `::$` 开头。列表 8.7 显示了 `CallRulesets` 规则集的运行情况。

### 列表 8.7 从规则调用另一个规则集

```
[root] sendmail -bt -Ctest.cx
ADDRESS TEST MODE (ruleset 3 NOT AUTOMATICALLY INVOKED)
Enter<ruleset> <address>
> CallRulesets julie@red
CallRulesets      input: julie @ broadest
canonify          input: julie @ broadest
canonify2         input: julie < @ broadest
canonify2         returns: julie < robin foobirds .org >
canonify          returns: julie . robin foobirds .org >
final             input: julie < robin foobirds .org >
final             returns: julie . robin foobirds .org
CallRulesets      returns: julie . robin foobirds .org
^ ^D
```

在列表 8.7 中，`CallRulesets` 接收了地址 `julie@breast`，它匹配了规则集中第一条规则的 `$*@$-` 模式。该规则调用了 `canonify` 并传递了 `@` 和 `breast` 这三个标记。`canonify` 通过在主机部分周围加上角括号来“聚焦”（focus）地址，反过来调用了 `canonify2`。`canonify2` 将地址转换为 `julie@robin.foobirds.org>`，这是 `canonify` 返回给 `CallRulesets` 的值。执行 `CallRulesets` 中的第二条规则。值 `julie@robin.foobirds.org>` 匹配规则中的 `$@` 模式，因此调用了规则 `final` 并传递了该地址值。`final` 对地址进行“去聚焦”（defocus）并返回值 `julie@robin.foobirds.org`，该值成为 `CallRulesets` 返回的值。

注意：“focus”和“defocus”用于描述 `Sendmail` 内部过程，即标记地址的某些部分以便处理。通常，这涉及到将地址括在角括号中。

## 使用外部信息转换地址

在列表 8.7 中，`CallRule` 仅匹配模式并调用其他规则集来完成所有的重写工作。也可以使用外部服务器（如 DNS）或外部数据库来转换输入地址。`Canary` 规则将主机名转换为 `hostname` 的标准 DNS 格式。这是通过查询 DNS 并使用返回的信息来实现的。

`[$hostname]` 语法通过将主机名传递给域名进行解析，将主机的 `nickname` 或其 IP 地址转换为标准名称。列表 8.8 显示了 `[$hostname]` 符号的用法。

### 列表 8.8 从 DNS 获取标准名称

```
[root]# mail -bt -Ctest.cf
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> CallRulesets julie@red
CallRulesets      input: julie @ broadest
canonify          input: julie @ broadest
canonify2         input: julie < @ broadest
canonify2         returns: julie < robin foobirds .org >
canonify          returns: julie . robin foobirds .org >
final             input: julie < robin foobirds .org >
final             returns: julie . robin foobirds .org
CallRulesets      returns: julie . robin foobirds .org
^ ^D
```

在列表 8.7 中，`CallRule` 仅匹配模式并调用其他规则集来完成所有的重写工作。也可以使用外部服务器（如 DNS）或外部数据库来转换输入地址。`Canary` 规则将主机名转换为 `hostname` 的标准 DNS 格式。这是通过查询 DNS 并使用返回的信息来实现的。

`[$hostname]` 语法通过将主机名传递给域名进行解析，将主机的 `nickname` 或其 IP 地址转换为标准名称。列表 8.8 显示了 `[$hostname]` 符号的用法。
