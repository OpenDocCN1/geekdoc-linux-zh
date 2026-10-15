

## 示例 11.42
（使用临时默认值）

```
1 $ fruit=peach
2 $ print ${fruit:-plum}
peach
3 $ print ${newfruit:-apple}
apple
4 $ print ${newfruit}
5 $ print ${TERM:-vt120}
sun-cmd
```

### 解释

- 1 变量 fruit 被赋值为 peach。
- 2 特殊修饰符 :- 会检查变量 fruit 是否已设置。如果已设置，则打印值 peach；如果未设置，则打印 plum。
- 3 变量 newfruit 未被设置。值 apple 将被打印。
- 4 变量 newfruit 未被设置，因此什么也不打印。在步骤 3 中，表达式只是被替换为单词 apple 并打印。
- 5 如果 TERM 变量未被设置，默认值 vt120 将被显示。在此示例中，终端已被设置为 sun-cmd，即 Sun 工作站。

## 示例 11.43
（分配永久默认值）

```
1 $ name=
2 $ print ${name:=Patty}
Patty
3 $ print ${name}
Patty
4 $ print ${TERM:=vt120}
vt120
$TERM
vt120
```

### 解释

- 1 变量 name 被赋值为 null。
- 2 特殊修饰符 := 会检查变量 name 是否被设置为除 null 以外的某个值。如果已设置，则不会被更改；如果为 null 或未设置，则会被赋予等号右侧的值。因为变量被设置为 null，所以 Patty 被赋给 name。该设置是永久的。
- 3 变量 name 仍包含值 Patty。
- 4 如果变量 TERM 未设置，它将被永久赋予默认值 vt120。

## 11.9.8 子字符串的变量扩展

模式匹配参数用于从字符串的前端或末端剥离某些部分。最常见的用途是剥离路径头或尾的路径名元素。参见表 11.13。

**表 11.13 变量扩展子字符串**

| 表达式 | 功能 |
|---|---|
| `${variable#pattern}` | 匹配变量值的最小尾部部分与 pattern 并将其移除。 |
| `${variable##pattern}` | 匹配变量值的最大尾部部分与 pattern 并将其移除。 |
| `${variable%pattern}` | 匹配变量值的最小头部部分与 pattern 并将其移除。 |
| `${variable%%pattern}` | 匹配变量值的最大头部部分与 pattern 并将其移除。 |

**示例 11.47**

```sh
$ pathname='/usr/bin/local/bin'
$ print ${pathname%/bin}
/usr/bin/local
```

**解释**

1. 局部变量 `pathname` 被赋值为 `/usr/bin/local/bin`。
2. `%` 移除 `pathname` 的最小尾部部分，该部分包含模式 `/bin`，后跟零个或多个字符；也就是说，它剥离了 `/bin`。

**示例 11.48**

```sh
$ pathname='/usr/bin/local/bin'
$ print ${pathname%%/bin}
/usr
```

**解释**

1. 局部变量 `pathname` 被赋值为 `/usr/bin/local/bin`。
2. `%%` 移除 `pathname` 的最大尾部部分，该部分包含模式 `/bin`，后跟零个或多个字符；也就是说，它剥离了 `/bin/local/bin`。

## 11.9 变量

**示例 11.49**

```sh
1  $ pathname=/home/liliput/jake/.cshrc
2  $ print ${pathname#/home}
   /liliput/jake/.cshrc
```

**解释**

1. 局部变量 pathname 被赋值为 /home/liliput/jake/.cshrc。
2. # 移除 pathname 的最小头部部分，该部分包含模式 /home；也就是说，/home 被从路径变量的开头剥离。

**示例 11.50**

```sh
1  $ pathname=/home/liliput/jake/.cshrc
2  $ print ${pathname##*/}
   .cshrc
```

**解释**

1. 局部变量 pathname 被赋值为 /home/liliput/jake/.cshrc。
2. ## 移除 pathname 的最大头部部分，该部分包含零个或多个字符直到最后的斜杠；也就是说，它从路径变量中剥离了 /home/liliput/jake/。

## 11.9.9 变量属性：typeset 命令

变量的属性，例如其大小写、宽度以及左对齐或右对齐，可以通过 typeset 命令控制。当 typeset 命令更改变量的属性时，该更改是永久的。typeset 函数还有其他多个功能。参见表 11.14。

**示例 11.51**

```sh
1  $ typeset -u name="john doe"
   $ print "$name"
   JOHN DOE          # 将所有字符更改为大写。

2  $ typeset -l name
   $ print $name
   john doe          # 将所有字符更改为小写。

3  $ typeset -L4 name
   $ print $name
   john             # 左对齐的固定宽度 4 字符字段。
```
