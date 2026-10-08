

## 高级 Bash 脚本指南

```bash
# t=${path_name%/}; t=${####*/} is a more general solution,
+# but still fails sometimes.
# If $path_name has a newline, then `basename $path_name` will not work,
+# but the expression.
# (Thanks, S.C.)

t=$(path_name/*)
# Same effect as
echo "$path_name", stripped of suffixes = "$"
# This will fail in some cases, such as "../", "/foo///", "/foo/", ""
# Removing suffixes, especially when the basename has no suffix,
# but the dirname does, also complicates matters.
# (Thanks, S.C.)

echo
t=$(path_name:11)
echo "$path_name", with 11 chars stripped off = "$"
t=$(path_name:11:5)
echo "$path_name", with first 11 chars stripped off, length 5 = "$"

echo
t=$(path_name/bozo/clown)
echo "$path_name with \"clone\" replaced by \"clown\" = "$"
t=$(path_name/today/)
echo "with \"today\" deleted = "$"
t=$(path_name/o)
echo "$path_name with all o's capitalized = "$"
t=$(path_name/o/)
echo "$path_name with all o's deleted = "$"

exit 0
```

**$(var/%Pattern#Replacement)**
*如果 var 的前缀匹配 Pattern，则将 Pattern 替换为 Replacement。*

**$(var/%Pattern#Replacement)**
*如果 var 的后缀匹配 Pattern，则将 Pattern 替换为 Replacement。*

## 示例 10.13. 匹配字符串的前缀或后缀

```bash
#!/bin/bash
# var-match.sh
# 字符串前缀/后缀模式替换演示。

v0=abc1234zip123abc      # 原始变量。
echo "$v0 = $v0" # abc1234zip123abc
echo

# 匹配字符串的前缀（开头）。
v1=${v0#ABC/ABCDEF}      # abc1234zip123abc
                                 |--|-
echo "$v1 = $v1"         # ABCDEF1234zip123abc

# 匹配字符串的后缀（结尾）。
v2=${v0%*ABC/ABCDEF}      # abc1234zip123abc
                                 |-
echo "$v2 = $v2"         # abc1234zip123ABCDEF
                                 |-----
```

第 10 章 操作变量

## 高级 Bash 脚本指南

```bash
echo
----------------------------------------------------------------------
# 必须匹配字符串的开头/结尾，
# 否则不会产生替换结果。
# 匹配了，但不在开头。
v3=$(v0/123/000)  # abc1234zip1234abc
echo "v3 = $v3"      # 无替换。

v4=$(v0/123/000) # 匹配了，但不在结尾。
echo "v4 = $v4"      # abc1234zip1234abc
                               # 无替换。

exit 0
```

${!varprefix*}, ${!(varprefix@)}

匹配所有之前声明的带有 varprefix 的变量名

+   # 这是间接引用的一种变体，但使用了 " * 或 @。
# Bash 版本 2.04 添加了此功能。

xyz=whatever
xyz24=

```bash
a=${!xyz*}      # 展开为声明变量的 "name*"
# ^ ^               + 以 "xyz" 开头。
echo "a = $a"      # a = xyz23 xyz24
a=${!xyz0}       # 与上述相同。
echo "a = $a"      # a = xyz23 xyz24
```

---

```bash
echo
abc23=something_else
b=${!abc*}
echo "b = $b"      # b = abc23
c=$(!b)             # 现在是更熟悉的间接引用类型。
echo $c              # something_else
```

第 10 章 操作变量

137

## 第 11 章 循环与分支

你需要这种迭代吗，姑娘？

-- 莎士比亚，《奥杰罗》

对代码块的操作是构建结构化和组织化 shell 脚本的关键。循环和分支结构提供了实现这些工具。

### 11.1. 循环

*循环* 是一个代码块，只要*循环控制条件*满足，它就会*迭代*命令列表。

**for 循环**

*   **for arg in [list]**
    - 这是基本的循环结构。它与其 C 语言对应的显著不同。

```bash
for arg in [list]
do
  command(s)...
done
```

> 在循环的每次通过中，`arg` 获得列表中每个后续变量的值。

```bash
for arg in "var1" "var2" "var3" ... "$varN"
# 在循环第 1 次通过中，arg = $var1
# 在循环第 2 次通过中，arg = $var2
# 在循环第 3 次通过中，arg = $var3
# ...
# 在循环第 N 次通过中，arg = $varN
```

# [list] 中的参数引号以防止可能的单词拆分。
参数 `list` 可能包含`通配符`。

如果 *do* 与 *for* 在同一行，则 list 后面需要一个分号。

`for arg in [list];do`

#### 示例 11-1   for 循环

```bash
#!/bin/bash
# 列出行星。
for planet in Mercury Venus Earth Mars Saturn Uranus Neptune
do
  echo $planet  # 每个行星单独占一行。
```

```bash
done

echo; echo
for planet in "Mercury Venus Earth Mars Saturn Uranus Neptune"
# 所有行星在同一行。
# 整个 'list' 被引号包裹创建了一个变量。
# 为什么？空格被包含在了变量中。
done
echo $planet
done

echo; "Whoops! Pluto 不再是一个行星了!"

exit 0
```

[list] 元素可能包含多个参数。这在处理参数组时很有用。在这种情况下，使用 set 命令（参见示例 15-16）强制对每个 [list] 元素进行解析并对每个 [list] 元素进行赋值。

