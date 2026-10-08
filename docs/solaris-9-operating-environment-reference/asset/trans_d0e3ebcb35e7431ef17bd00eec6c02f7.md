

# 用法

以下列表详细描述了 `bc` 程序的语法：

- 字母 (Letter): a 到 z 之间的单个字母。
- 表达式 (Expression): 一个表达式：一个数学或逻辑值、一个接受值的的操作数，或者一组可以求值的操作数和运算符的组合。
- 语句 (Statement): 一个语句。

# 注释

注释封装在 `/*` 和 `*/` 之间。

# 名称（操作数）

- 字母 (Letter): 简单的单字母变量。
- 字母 [Expression]（最多 BC_DIM_MAX 维）：数组元素。
- ibase：输入基数。
- obase（受限制为 BC_BASE_MAX）：输出基数。
- scale（限制为 BC_SCALE_MAX）：bc 计算中保留的小数点后位数。

# 其他操作数

- 带有可选符号和小数点的任意长度数字。
- 双引号（""）之间少于 BC_STRING_MAX 个字符的字符串。
- ( Expression )。
- sqrt ( Expression ): 平方根。
- length ( Expression ): （有效小数位数）。
- scale ( Expression ): （小数点后的位数）。
- 字母 (Expression, ..., Expression )。

# 运算符

- +-* / % ^: (% 是取余数；^ 是幂)。
- --（前缀和后缀；应用于名称）。
- <= >= != = <
- += -= *= = /= % = ^

# 语句

- Expression
- [Statement;...;Statement]
- if (Expression) Statement
- while (Expression) Statement
- for (Expression; Expression; Expression) Statement
- 空语句 (null statement)。
- break
- quit
- string

# 函数定义

```
bc
define Letter ( Letter, ..., Letter ) (
auto Letter, ..., Letter
Statement; ... Statement
return ( Expression )
);
```

# - Math 库中的函数

- s(x): 正弦。
- c(x): 余弦。
- e(x): 指数函数。
- l(x): 对数函数。
- a(x): 反正切函数。
- j(n,x): 贝塞尔函数。

所有函数参数均按值传递。

除非主运算符在赋值语句中，否则作为表达式的语句的值将被打印出来。你可以使用分号或换行符分隔语句。对 `scale` 的赋值以 dc 的方式影响运算中保留的位数。对 `ibase` 或 `obase` 的赋值设置输入输出进制。

你可以同时将同一个字母作为数组和简单变量。所有变量在程序中都是全局的。`auto` 变量在用作函数调用时入栈。当数组作为函数参数或定义为自动变量时，数组名后必须跟随空方括号。

# 示例

你可以使用 `bc` 进行常规算术计算。输入 `bc` 并按回车。不会显示提示符。要退出，输入 `quit` 或按 `Control-D`。整个计算必须在同一行。一旦按下回车，`bc` 就会显示每次计算的结果。

```
castle% bc
2 + 2
4
Control-
caste%%
```

# bc 101

你可以使用负号表示负数。在以下示例中，减去一个负数等于加上它。加上一个负数等于减去它。

```
castle% bc
1 + 2 + 3 - -3.12195
9.12195
1 + 2 + 3 + -2.14197
3.85803
Control-D
castle%
```

你可以使用 `scale` 运算符来指定计算中保留小数点后多少位数字。`scale` 设置在当前会话中持续有效。

```
castle% bc
scale = 3
1.2345/.9876
1.250
Control-D
castle%
```

你可以通过给单个字母赋值来定义和使用变量。在接下来的示例中，`x` 被设置为 7 并在随后的计算中使用它。

```
castle% bc
x=7
5*7
35
Control-D
castle%
```

在 shell 中，以下命令将 `-?` 的前 10 位近似值赋值给变量 `x`。

```bash
x=5(printf "%s\n" 'scale = 10; 104348/33215' | bc);
```

接下来的示例定义了一个函数来计算指数函数的近似值，并打印前 10 个整数的指数近似值。

```bc
scale = 20
define e(x){
auto a, b, c, i, s
a = 1
b = 1
s = 1
for(i=1; i<=1; i++){
a = a*x
b = b*i
c = a/b
if (c == 0) return(s)
s = s+c
}
for(i=1; i<=10; i++) e(i);
```

# bc

将文件读入 `bc` 会产生以下结果。

```
castle% example.bc
2.718281824590423526
7.3890560983065022713
20.0553609231867767483
54.5981500331442390790
148.4135910257660342091
403.4287934273660342091
```

