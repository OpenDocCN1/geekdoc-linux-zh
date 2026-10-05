

## 第 8 章理解重写规则

rule. 初看之下，人们可能认为此处不需要流控制，因为它是规则集中的最后一条规则，因此规则集将在该规则执行后结束。仔细观察可以发现其原理显而易见：第三条规则将永远不会执行完毕，因为它是一个无限循环。`*$` 模式匹配零或多个标记，意味着它将匹配任何内容，字符串 `Wrong format`，此时该模式将匹配规则的输出。由于该规则递归地对其输出与模式 `$` 进行处理，而 `$` 匹配任何内容，这将导致循环。Sendmail 会检测到循环并在发现循环时发出警告（给出投诉），如列表 8.6 所示。

### 列表 8.6 Sendmail 配置中紧密循环的结果

```
[root]# sendmail -bt -Ctest.cf
ADDRESS TEST TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> =ClassTest
R$ = $*                        @ Found it
R$ = $w                        @ Not in class w
R$                               Wrong format
> ClassTest craig
ClassTest input: craig
Infinite loop in ruleset ClassTest, rule 3
ClassTest returns: Wrong format
> ^D
```

在列表 8.6 中，sendmail 再次使用 `-bt -S` 命令运行（该命令在第 10 章与其他测试命令一起描述），用于显示 `ClassTest` 规则集的内容。在此示例中，规则集第三条规则中的模板不以 `$` 开头。在这种情况下，当输入 `craig` 运行 `ClassTest` 时，会产生无限循环。Sendmail 显示一条错误消息，说明遇到了无限循环并精确指出了循环发生的位置。

循环不需要像列表 8.6 所示那样紧密。一个循环可以涉及多条规则，因为规则可以通过 `$>name` 语法调用另一个规则集。当被调用的规则集处理完成后，它会向调用规则返回一个重写后的地址。然后，返回的电子邮件地址将与调用规则中的模式进行比较。如果仍然匹配，则再次调用该规则集。在可能发生循环的地方，使用 `:$ 和 `$@` 来防止循环。

## 重写规则 237

`$>name` 符号调用规则集 `name`，并将模板剩余部分定义的地址传递过去进行处理。例如，下面所示名为 `CallRulesets` 的规则集中的两条规则都调用了其他规则集：

```
SCallRulesets
R$* @ $- $: $> canonify $1 @ $2
R$* $: $> final $1
```

第一条规则中的模板调用 `canonify($canonify)`，并传递 `$1` 的内容、一个字面量 `@` 以及 `$2` 的内容。模板以 `:$ 符号开头，因此只有在模式匹配时，第一条规则才会执行。第二条规则中的模板调用 `final($final)` 并传递 `$1` 的内容。（由于第二条规则中的模式仅包含一个符号，`$1` 包含了整个输入地址）。第二条规则也只会执行一次，因为它的模板以 `:$ 开头。列表 8.7 显示了 `CallRulesets` 规则的实际运行。

### 8.7 从规则调用另一个规则集

```
[root]# sendmail -Ctest.cf
ADDRESS TEST MODE <address>
-ter <ruleset> <address>
> CallRulesets julieredbreast
CallRulesets input: julie redbreast
canonify input: julie <: breast>
Canonify2 input: julie <: breast>
canonify returns: julie @robin . foobirds .org . > returns: julie @robin . foobirds .org . >
final input: julie @robin . foobirds .org . >
final returns: julie @robin . foobirds .org
CallRulesets returns: julie @robin . foobirds .org
> ^
```

在 8.7 中，`CallRulesets` 被传递了地址 `julieredbreast`，该地址匹配规则集中第一条规则的 `$@` 模式。该规则调用规则集 `canonify` 并传递三个标记：`julie`、`@` 和 `redbreast`。`canonify` 通过在主机名周围加上角括号来“聚焦”地址，反过来，它调用规则集 `Canonify2`，后者将地址转换为 `julie@robin.foobirds.org>`，这是 `canonify` 返回给 `CallRulesets` 的值。随后执行 `CallRulesets` 中的第二条规则。值 `julie@robin.foobirds.org>` 匹配规则中的 `$@` 模式，因此调用了规则集 `final` 并传递了地址值。`final` “去聚焦”地址并返回值 `julie@robin.foobirds.org`。`CallRulesets` 返回 `julie@robin.foobirds.org`。

