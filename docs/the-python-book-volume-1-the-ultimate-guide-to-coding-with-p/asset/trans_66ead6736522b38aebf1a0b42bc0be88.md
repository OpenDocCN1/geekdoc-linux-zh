

我们想要在列表中的整数数量

用于存储整数的列表

这些用于跟踪我们当前拥有的整数数量

如果上述操作成功，则 isint 将被设为 true：isint=True

到目前为止，用户已经放弃，或者我们有一个装满整数的列表。我们可以用几种方式遍历这些列表。第一种是使用 for 循环

```
#!/usr/bin/env python2

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

## 开始学习 Python

### 提示

如果你想能够在不传递任何变量的情况下调用函数，你可以为变量定义默认值。你可以通过在变量名后加上等号来实现。例如，你可以这样做：
def modify_string(original: "Default string")

```
# Or with a while loop:
print("Using a while loop")
# We already have the total above, but knowing the len function is very useful
total = len(ints)
count = 0
while count < total:
    print(str(ints[count]))
    count += 1
```

## 函数和变量作用域

函数在编程中用于将流程分解为更小的块。这通常使代码更易于阅读。如果设计得当，函数也可以重复使用。函数可以接收传递给它们的变量。Python 中的变量始终按值传递，这意味着变量的副本被传递给函数，该副本仅在函数的作用域内有效。对函数内部原始变量所做的任何更改都将被丢弃。但是，函数也可以返回值，因此这不是问题。函数使用关键字 def 定义，后跟函数名。可以在函数名后加上括号中的变量来传递。多个变量用逗号分隔。在这些括号中给变量起的名字是在函数作用域中使用的名字，而不管传递给函数的变量叫什么。让我们看看实际效果。

相反程序的输出如下：

> “Functions are used in programming to break processes down in”

```
#!/usr/bin/env python2

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

我们现在已超出 modify_string 函数的作用域，因为我们已减少了缩进级别

在此代码中，测试字符串不会被更改

但是，我们可以这样调用函数

