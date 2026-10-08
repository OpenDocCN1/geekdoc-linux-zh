

# 高级 Bash 脚本指南

```bash
echo
echo ' - 范围之后 -'
echo $(VarSomething:4:3)
```

```bash
# 字符后的三个字符
# character[3]
```

```bash
echo ' - 稀疏数组陷阱'
echo $(Array[@]:1:2)
# 四 - 唯一包含内容的元素。
# 两个元素（如果存在那么多的话）。
# 第一个包含内容的元素
# + （第一个包含内容的元素被
# + 考虑，就像
# + - 下标为零一样）。
```

```bash
# 执行时，Bash 仅考虑有内容**的数组元素
printf "%s" ${Array[@]:0:3} # 尝试这一行
```

```bash
# 在 2.004、2.05a 和 2.05b 版本中，
# Bash 不以预期的方式使用这种符号处理稀疏数组。
```

```bash
# 当前的 Bash 维护者 Chet Ramey 修复了这个问题。
```

```bash
echo ' - 非稀疏数组'
echo ${2:2}
# 参数[1] 之后的两个参数
```

```bash
# 字符串向量示例的新受害者：
string2=abcABC123ABC
array2=(abc abcABC 123 ABCABC abc abc)
sparse2(1)=['abc'] [3]='ABC' [4]='' [5]='123123'
```

```bash
echo
echo ' - 目标字符串 -${string2}'
echo ' - 目标数组 -${array2[@]}'
echo ' - 稀疏数组 -${sparse2[@]}'
echo ' - [0]=空引用, [2]=空引用, [4]=空内容'
echo ' - [1]=abc [3]=ABC [5]=123'
echo ' - 非空引用计数: ${sparse2[@]} 元素
```

```bash
echo
echo ' - 前缀子元素 -'
echo ' - Glob 通配匹配必须包含第一个字符。 -'
echo ' - Glob 通配模式可以是字面量或函数执行结果。 -'
```

```bash
# 返回简单、字面量 Glob 通配模式的函数
_abc() {
    echo -n 'abc'
}
```

```bash
echo -n ' - 最短前缀 - # 未更改（不是前缀）。
echo ${string2#*}
echo ${string2#_abc} # ABC123ABCabc
echo ${array2[@]} # 应用于每个元素。
```

```bash
# ${sparse2[@]} # 版本-2.05b 核心转储。
# 已由 Chet Ramey 修复。
```

```bash
# - 如果有“第一个下标”就就好了
echo ${sparse2[@][*]} # 这是不有效的。
```

附录 A. 脚本

# 高级 Bash 脚本指南

```bash
echo '- 最长前缀 -'
echo ${stringZ##1*3}               # 未更改（不是前缀）
echo ${stringZ##*A}                # abc
echo ${array[@]}##*c}             # ABCABC 123123 ABCABC

echo ${sparseZ[@]}##*c}             # 版本-2.05b 核心转储。
echo # 已由 Chet Ramey 修复。

echo '- 后缀子元素删除 -'
echo ' - Glob 通配匹配可以包含最后一个字符。 -'
echo ' - Glob 通配模式可以是字面量或函数执行结果。 -'

echo '- 最短后缀 -'
echo ${stringZ1*3}                   # 未更改（不是后缀）。
echo ${stringZ$*_abc}              # abcABC123ABC
echo ${array[@]}%abc}             # 应用于每个元素。

echo ${sparseZ[@]}%abc}            # 版本-2.05b 核心转储。
echo # 已由 Chet Ramey 修复。

echo - 如果有“最后一个脚本的”就就好了
echo ${#sparseZ[@]}%               # 这不是有效的 Bash 语法。

echo '- 最长后缀 -'
echo ${stringZ1*3}                   # 未更改（不是后缀）
echo ${stringZ$*b*c}                # a
echo ${array[@]}%abc}             # ABCABC 123123 ABCABC A

echo ${sparseZ[@]}*abc}            # 版本-2.05b 核心转储。
echo # 已由 Chet Ramey 修复。

```

echo
echo '- 子元素替换 -'
echo ' - 字符串中任意位置的子元素。 -'
echo ' - 第一个规范是 Glob 通配模式 -'
echo ' - Glob 通配模式可以是字面量或 Glob 模式结果。 -'
echo ' - 第二个规范可以省略。读作'
echo ' 如下： 替换为空（删除） -'
```

```bash
# 返回简单、字面量 Glob 通配模式的函数
_123() {
    echo -n '123'
}

echo '- 替换第一次出现 -'
echo ${stringZ/$_{123}/999}         # 已更改 (123 是一个组件)
echo ${stringZ[@}/ABC/xyz}         # xyzABC123ABCabc
echo ${array[@]}/ABC/xyz}       # 应用于每个元素。
echo ${sparseZ[@]}/ABC/xyz}     # 按预期工作。

echo '- 删除第一次出现 -'
echo ${stringZ$#_{123}/}
echo ${stringZ[@}/ABC/}
echo ${array[@]}/ABC/}
echo ${sparseZ[@]}/ABC/}
```

附录 A. 贡献脚本

# 高级 Bash 脚本指南

```bash
# 替换内容不需要是字面量，
# 因为允许使用函数的结果。
# 这适用于所有形式的替换。
```

