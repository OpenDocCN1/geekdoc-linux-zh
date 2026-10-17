
引用计数被标记为递减，但不会立即递减，直到一短时间之后才会执行。通常，“短时间之后”指的是一个 Perl 语句，例如对 XSUB 函数的调用。凡生（mortal）SV 引用计数的决定因素取决于两个宏：`SVAVMETPS` 和 `FREETMPS`。有关这些宏的更多细节，请参考 `Perclcall` 和 `Perlxs`。

“死亡化（Mortalization）”的最简单的 `SVREFCNT_dec`。然而，如果你对一个变量进行两次死亡化，引用计数将递减两次。

“凡生（Mortal）”SV 主要用于位于 Perl 栈上的 SV。一个示例是为被调用的子程序传递名称而创建的 SV，被标记为凡生态，以便在它从栈中弹出时自动清理。同样，由 XSUBS 返回的结果（它们被推入栈中）通常也会标记为凡生态。

要创建一个凡生变量，请使用以下函数：

`SV* sv_newmortal()`
`sv_mortal(SV*)`
`sv_mortalcopy(SV*)`

第一次调用创建一个凡生的 sv（无值），第二次调用将现有 sv 转换为凡生 sv（从而延迟 `SVREFCNT_dec`），第三次创建一个现有 sv 的凡生副本。由于 `sv_newmortal` 没有给新 sv 赋值，因此通常需要通过 `sv_setpv`、`sv_setiv` 等函数为其赋值：

```
SV* tmp = sv_newmortal(); sv_setiv(tmp, an_integer);
```

就像在多个 C 语句中一样，通常显示如下形式：

```
SV* tmp = sv_newmortal(newSiv(an_integer));
```

你应该在使用小心创建凡生变量。如果你在多个上下文中创建了同一个凡生值，或者多次创建凡生态，就会发生某些问题。将“死亡化”考虑为延迟的 `SVREFCNT_dec` 有助于减少此类问题。例如，如果你传递的是栈上的 sv，则不需要任何死亡化。如果你不确定，那么使用 `SVREFCNT_inc` 和 `sv_mortal`，或者创建一个 `sv_mortalcopy` 会更安全。

凡生程序不仅适用于 SV；通过将它们的地址（强制转换为 SV）传递给 `sv_mortal` 或 `sv_mortalcopy` 程序，`AV` 和 `HV` 也可以变为凡生态。

## 存储区（Stashes）与全局变量（Globs）

stash 是一个包含包内定义的所有变量的哈表。stash 的每个键都是符号名称（由所有具有相同名称的不同类型共享），哈表中的每个值都是一个 GV（全局值）。该 GV 反而包含对以下各种对象的引用（但不限于此内容）：

| 标量值 | 数组 | 哈希值 | I/O 句柄 | 格式 | 子程序 |
| :--- | :--- | :--- | :--- | :--- | :--- |

名为 `PL_defstash` 的单一 stash 持有主包中存在的项。要获取其他包中的项，请在包名后附加字符串“::”。Foo 包中的项是 `PL_defstash` 中的 stash `Foo::`。stash 中 `Baz :: Baz ::` 包的项是 `Baz ::` 的 stash 中的 `Baz ::`。

要获取某个特定包的 stash 指针，请使用函数：

`HV* g_stashpv(const char* name, i32 flags)`
`hv* g_stashsv(SV*, i32 flags)`

第一个函数接受一个字面量，第二个使用存储在 sv 中的字符串。记住，stash 是一个哈表，第二个返回的是一个 `hv*`。如果 `flags` 设置为 `GV_ADD`，将创建一个新包。

`g_stash*v` 的名称是你想要的包符号的类型名称。默认包名为 `main`。如果你有多个嵌套包，将它们的名称传递给 `g_stash*v`，并像 Perl 语言本身那样用 `::` 分隔。

或者，如果你有一个祝福（blessed）引用的 sv，可以使用查找 stash 指针：

```
HV* SVSTASH(SVRV(SV*));
```

然后使用以下函数获取包名本身：

`char* HVNAME(HV* stash);`

如果你需要对对象进行祝福或重新祝福，可以使用以下函数：

`SV* sv_bless(SV*, HV* stash)`

其中第一个参数 `sv*` 必须是一个引用，第二个参数是 stash。返回的 `sv*` 现在可以像任何其他 sv 一样使用。

有关引用和祝福的更多信息，请参阅 `perlref`。

## 双类型 SV

标量变量通常只包含一种类型的值：整数、双精度浮点、指针或引用。Perl 会自动将实际标量数据从存储类型转换为请求的类型。

某些标量变量包含多一种类型的标量数据。例如，变量 `$@` 包含 `errno` 的数值值，或者包含来自 `strerror` 或 `sys_errlist[]` 的字符串等效值。

要将多个数据值强制放入 sv 中，你必须做两件事：使用 `sv_set*v` 程序添加额外的标量类型，然后设置一个标志，以便 Perl 认为它包含多于一种类型的数据。用于设置这些标志的四个宏是：

```
SVOK_on SVOK_on SVOK_on SVOK_on
```

特定的宏取决于你先调用了哪个 `sv_set*v` 程序。这是因为每个 `sv_set*v` 程序只开启正在设置的特定类型的数据位，并关闭其余位。

例如，要创建一个同时包含数值和描述性字符串值的新 Perl 变量，可以使用以下代码：

```
extern int SVOK_on SVOK_on SVOK_on SVOK_on
```

特定的宏取决于你先调用了哪个 `sv_set*v` 程序。这是因为每个 `sv_set*v` 程序只开启正在设置的特定类型的数据位，并关闭其余位。

例如，要创建一个同时包含数值和描述性字符串值的新 Perl 变量，可以使用以下代码：

```

（此处原文存在重复内容，已按要求翻译）

（此处原文存在重复内容）

特定的宏取决于你先调用了哪个 `sv_set*v` 程序。这是因为每个 `sv_set*v` 程序只开启正在设置的特定类型的数据位，并关闭其余位。

（此处原文存在重复内容）

就像在多个 C 语句中一样，通常显示如下形式：

```

SV* tmp = sv_newmortal(newSiv(an_integer));

```

你应该在使用小心创建凡生变量。如果你在多个上下文中创建了同一个凡生值，或者多次创建凡生态，就会发生某些问题。将“死亡化”考虑为延迟的 `SVREFCNT_dec` 有助于减少此类问题。例如，如果你传递的是栈上的 sv，则不需要任何死亡化。如果你不确定，那么使用 `SVREFCNT_inc` 和 `sv_mortal`，或者创建一个 `sv_mortalcopy` 会更安全。

凡生程序不仅适用于 SV；通过将它们的地址（强制转换为 SV）传递给 `sv_mortal` 或 `sv_mortalcopy` 程序，`AV` 和 `HV` 也可以变为凡生态。

## 存储区（Stashes）与全局变量（Globs）

stash 是一个包含包内定义的所有变量的哈表。stash 的每个键都是符号名称（由所有具有相同名称的不同类型对象共享），哈表中的每个值都是一个 GV（全局值）。该 GV 反而包含对以下各种对象的引用（但不限于此内容）：

| 标量值 | 数组 | 哈希值 | I/O 句柄 | 格式 | 子程序 |
| :--- | :--- | :--- | :--- | :--- | :--- |

名为 `PL_defstash` 的单一 stash 持有主包中存在的项。要获取其他包中的项，请在包名后附加字符串“::”。Foo 包中的项是 `PL_defstash` 中的 stash `Foo::`。stash 中 `Baz :: Baz ::` 包的项是 `Baz ::` 的 stash 中的 `Baz ::`。

要获取某个特定包的 stash 指针，请使用函数：
`HV* g_stashpv(const char* name, i32 flags)`
`hv* g_stashsv(SV*, i32 flags)`

第一个函数接受一个字面量，第二个使用存储在 sv 中的字符串。记住，stash 是一个哈表，第二个返回的是一个 `hv*`。如果 `flags` 设置为 `GV_ADD`，将创建一个新包。

`g_stash*v` 的名称是你想要的包符号类型名称。默认包名为 `main`。如果你有多个嵌套包，将它们的名称传递给 `g_stash*v`，并像 Perl 语言本身那样用 `::` 分隔。

或者，如果你有一个祝福（blessed）引用的 sv，可以使用查找 stash 指针：

```
HV* SVSTASH(SVRV(SV*));
```
