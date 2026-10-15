
## 25.1.7 for 循环

Ruby 的 `for` 比 C 语言的 `for` 循环稍微有趣一点。例如，下面的循环为集合中的每个元素运行一次（希望你还记得 shell 中的 `for` 循环）。

```
for var in collection
...
end
```

### 示例 15

集合可以是一个范围（这是大多数人谈论 `for` 循环时指的意思）。以下程序打印从 2 到 5 的数字。

```ruby
for x in (2..5)
  print x, "\n"
end
```

### 示例 16

集合可以是一个数组。例如，下面的程序在一行中打印 Hello 和 "How are you" 消息。

```ruby
for x in ["Hello", "How are you"]
  # 单引号也同样的方式工作
  print x, "\n"
end
```

### 示例 17

以下程序在 `for` 循环中使用了数组作为集合。注意，ruby 可以支持不同类型元素的数组。

```ruby
for x in ["Hello", 14, 13.44]
  print x, "\n"
end
```

像 perl 一样，shell 命令的输出可以在 ruby 中使用。例如，命令的输出被使用，并且它的每个单词都被打印出来。

```ruby
for i in `date`
  print i, "\n"
end
```

## 25.1.8 迭代器

迭代器通常可以替代传统的循环，一旦你习惯了它们，它们通常会更容易处理。例如，在下面的程序中，字符串长度是通过每个迭代器计算的。

### 示例 18

```ruby
str = gets
i = 0
str.chop_each_byte { i = i + 1 }
j = 0
k = i - 1
while j < k
  if (str[j] != str[k])
    print " Not Palindrome\n"
    break
  end
  j = j + 1
  k = k - 1
end
print "Palindrome"
```

### 示例 19

以下程序使用迭代器来查找字符串的长度。

```ruby
str = gets
i = 0
str.chop_each_byte { i = i + 1 }
print "Length of the string", i, "\n"
```

### 示例 20

以下示例用于解释迭代器。在每个迭代器的帮助下，元素被打印出来。数组使用 `sort` 函数排序，然后将被打印出来。

```ruby
arr = [1, 81, 21, 22, 22, 12, 13, 31]
print "Before Sorting the elements :\t"
arr.each { |i| print i, "\t" }
print "\n"
arr.sort
print "AfterSorting the elements :\t"
arr.each { |i| print i, "\t" }
print "\n"
```

迭代器不是 ruby 的原始概念。它们在面向对象的语言中被广泛使用。它们也被用于 Lisp，尽管在它们那里不被称为迭代器。然而，迭代器概念对许多人来说是一个陌生的概念，因此应该更详细地解释。

动词 `iterate` 的意思是多次做相同的事情，你知道的，所以迭代器就是一种多次做相同事情的东西。

Ruby 的 String 类型有非常有用的迭代器：

```ruby
"rama".each_byte { |c| printf "%c", c; print "\n" }
```

`each_byte` 是字符串中每个字符的迭代器。每个字符都被替换在局部变量中。

String 的另一个迭代器是 `each_line`。

## 25.1.8 函数/过程

Ruby 也支持像 C 和其他语言那样函数。例如，下面的示例打印给定的数字是否为素数。

### 示例 21

```ruby
$c = 0
def DIV(n, i)
  if n % i == 0
    $c = $c + 1
  end
end
n = gets.chop.to_i
2.upto(n - 1) { |i| DIV(n, i) }
if ($c == 0)
  print "Prime\n"
else
  print "Not Prime\n"
end
```

### 示例 22

以下程序定义了一个计算阶值的函数并使用了它。

```ruby
def fact(n)
  if n == 0
    1
  else
    n * fact(n - 1)
  end
end
print fact(ARGV[0].to_i), "\n"
```

## 25.1.9 模块

Ruby 拥有一套优秀的加载模块，例如数学相关的、窗口相关的等。模块可以通过 `include` 语句进行加载。

ruby 中的模块与类相似，区别在于：

- 模块可以没有实例。
- 模块可以没有子类。
- 模块由 `module ... end` 定义。

模块有两个典型的用途。其中一个是在中心位置收集相关方法和常量。ruby 标准库中的 `Math` 模块就扮演了这样的角色。

### 示例 23

例如，在下面的示例中，加载了 math 模块并使用了常量 `PI`。注意在执行操作时的作用域解析运算符。

```ruby
include Math
print "Enter Radius\n"
r = gets.chop.to_f
area = Math::PI * r * r
print "Area=", area, "\n"
```

记住模块不能被实例化或被子类化；但如果在类定义中包含一个模块，它的方法实际上将被“混入”（mixed in）到类中。Ruby 的方法实际上是追加到类中的。
