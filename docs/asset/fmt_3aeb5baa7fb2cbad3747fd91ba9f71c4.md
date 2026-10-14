
如果上述操作成功，则 `isint` 将被设为 `true`：`isint=True`

到目前为止，用户已经放弃，或者我们有一个装满整数的列表。我们可以用几种方式遍历这些列表。第一种是使用 `for` 循环

```#!/usr/bin/env python2

# We're going to write a program that will ask the user to input an arbitrary
# number of integers, store them in a collection, and then demonstrate how the
# collection would be used with various control structures.

import sys # Used for the sys.exit function

target_int = raw_input("How many integers?")

# By now, the variable target_int contains a string representation of
# whatever the user typed. We need to try and convert that to an integer but
# be ready to deal with the error if it's not. Otherwise the program will
# crash.
try:
    target_int = int(target_int)
except ValueError:
    sys.exit("You must enter an integer")

ints = list()
count = 0

# Keep asking for an integer until we have the required number
while count < target_int:
    new_int = raw_input("Please enter integer {}:".format(count + 1))
    isint = False
    try:
        new_int = int(new_int)
    except:
        print("You must enter an integer")

    # Only carry on if we have an integer. If not, we'll loop again
    # Notice below I use ==, which is different from =. The single equals is an
    # assignment operator whereas the double equals is a comparison operator.
    if isint == True:
        # Add the integer to the collection
        ints.append(new_int)
        # Increment the count by 1
        count += 1

print("Using a for loop")
for value in ints:
    print(str(value))
```

# 开始学习 Python

## 提示

如果你想能够在不传递任何变量的情况下调用函数，你可以为变量定义默认值。你可以通过在变量名后加上等号来实现。例如，你可以这样做：

`def modify_string(original: "Default string")`

```# Or with a while loop:
print("Using a while loop")
# We already have the total above, but knowing the len function is very useful
total = len(ints)
count = 0
while count < total:
    print(str(ints[count]))
    count += 1
```

## 函数和变量作用域

函数在编程中用于将流程分解为更小的块。这通常使代码更易于阅读。如果设计得当，函数也可以重复使用。函数可以接收传递给它们的变量。Python 中的变量始终按值传递，这意味着变量的副本被传递给函数，该副本仅在函数的作用域内有效。对函数内部原始变量所做的任何更改都将被丢弃。但是，函数也可以返回值，因此这不是问题。函数使用关键字 `def` 定义，后跟函数名。可以在函数名后加上括号中的变量来传递。多个变量用逗号分隔。在这些括号中给变量起的名字是在函数作用域中使用的名字，而不管传递给函数的变量叫什么。让我们看看实际效果。

相反程序的输出如下：

> “Functions are used in programming to break processes down in”

```#!/usr/bin/env python2

# Below is a function called modify_string, which accepts a variable
# that will be called original in the scope of the function. Anything
# indented with 4 spaces under the function definition is in the
# scope.
def modify_string(original):
    original += " that has been modified."
    # At the moment, only the local copy of this string has been modified

def modify_string_return(original):
    original += " that has been modified."
    # However, we can return our local copy to the caller. The function
    # ends as soon as the return statement is used, regardless of where it
    # is in the function.
    return original

test_string = "This is a test string"
modify_string(test_string)
print(test_string)

test_string = modify_string_return(test_string)
print(test_string)

# The function's return value is stored in the variable test string,
# overwriting the original and therefore changing the value that is
# printed.
```

我们现在已超出 `modify_string` 函数的作用域，因为我们已减少了缩进级别

在此代码中，测试字符串不会被更改

但是，我们可以这样调用函数

# 开始学习 Python

```
[liam@liam-laptop Python]$ ./functions_and_scope.py
This is a test string
This is a test string that has been modified.
```

作用域是需要掌握的重要概念，否则会养成一些坏习惯。让我们写一个快速程序来演示这一点。它将有一个名为 `cont` 的布尔变量，它将决定一个数字是否会在 `if` 语句中被赋给一个变量。然而，该变量除了在 `if` 语句的作用域内之外，在任何地方都没有被定义。我们最后会尝试打印该变量。

```#!/usr/bin/env python2
cont = False
if cont:
    var = 1234
print(var)
```

在上面的代码段中，Python 会在打印前将整数转换为字符串。然而，显式地将事物转换为字符串始终是一个好主意——尤其是在拼接字符串时。如果你尝试对字符串和整数使用 `+` 运算符，会出现错误，因为它并不明确需要发生什么。`+` 运算符通常会把两个整数相加。话虽如此，我们之前演示的 Python 字符串格式化器是更干净的做法。你能看出问题吗？`Var` 只在 `if` 语句的作用域内被定义。这意味着当我们尝试访问 `var` 时会得到一个非常糟糕的错误。
